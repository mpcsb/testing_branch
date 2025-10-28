---
layout: single
permalink: /src_noise_model/
title: "src_noise_models"
--- 


```

import numpy as np
import pandas as pd
from pathlib import Path

from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler, PolynomialFeatures
from sklearn.pipeline import Pipeline
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import RandomForestClassifier
from sklearn.calibration import CalibratedClassifierCV
from sklearn.metrics import (
    roc_auc_score,
    accuracy_score,
    log_loss,
    brier_score_loss,
)

from xgboost import XGBClassifier
import matplotlib
matplotlib.use("Agg")  # must come before `import matplotlib.pyplot as plt`
import matplotlib.pyplot as plt
from tqdm import tqdm

# output dirs
PLOTS_DIR = Path("plots");   PLOTS_DIR.mkdir(parents=True, exist_ok=True)
RESULTS_DIR = Path("results"); RESULTS_DIR.mkdir(parents=True, exist_ok=True)

# noise schedule: 0.0 .. 0.4 (5 steps)
NOISE_LEVELS = (
    0.00,
    0.05,
    0.10,
    0.15,
    0.20,
    0.25,
    0.30,
    0.35,
    0.40,
    0.45,
)


# deterministic RNG factory: each (experiment, noise level) gets its own seed
BASE_SEED = 12
N_DATA=3_000
def _rng_for(experiment_name: str, noise_level: float, base_seed: int = BASE_SEED):
    key = f"{experiment_name}:{noise_level}:{base_seed}"
    return np.random.default_rng(abs(hash(key)) % (2**32))


# %%
# %%
def generate_base_data(
    n_samples=N_DATA,
    n_features=10,
    n_informative=5,
    n_redundant=2,
    class_sep=1.2,
    random_state=0,
):
    """Synthetic binary dataset with controllable signal strength."""
    X, y = make_classification(
        n_samples=n_samples,
        n_features=n_features,
        n_informative=n_informative,
        n_redundant=n_redundant,
        n_classes=2,
        class_sep=class_sep,
        flip_y=0.0,
        random_state=random_state,
    )
    return X.astype(float), y.astype(int)


def flip_labels(y, flip_rate, rng):
    """Flip each label with probability flip_rate."""
    y_noisy = y.copy()
    mask = rng.random(size=y.shape[0]) < flip_rate
    y_noisy[mask] = 1 - y_noisy[mask]
    return y_noisy


def add_feature_noise(X, noise_level, mode="gaussian", rng=None):
    """Add Gaussian or Laplace noise to features, scaled per-feature."""
    if noise_level <= 0:
        return X.copy()

    rng = np.random.default_rng(None if rng is None else rng)
    Xn = X.copy()

    std = Xn.std(axis=0, ddof=1)
    std[std == 0] = 1.0  # avoid /0

    scale = noise_level * std  # noise ∝ feature scale

    if mode == "gaussian":
        noise = rng.normal(0.0, scale, size=Xn.shape)
    elif mode == "laplace":
        b = scale / np.sqrt(2.0)
        noise = rng.laplace(0.0, b, size=Xn.shape)
    else:
        raise ValueError("mode must be 'gaussian' or 'laplace'")

    return Xn + noise


# %%
# %%
def make_log_reg():
    return Pipeline([
        ("poly", PolynomialFeatures(degree=2, include_bias=False, interaction_only=True)),
        ("scaler", StandardScaler()),
        ("clf", LogisticRegression(max_iter=500, solver="lbfgs")),
    ])

def make_rf():
    return RandomForestClassifier(
        n_estimators=100,
        min_samples_split=4,
        min_samples_leaf=2,
        random_state=0,
        n_jobs=-1,
    )

def make_xgb():
    return XGBClassifier(
        n_estimators=150,
        max_depth=5,
        learning_rate=0.05,
        subsample=0.8,
        colsample_bytree=0.8,
        objective="binary:logistic",
        eval_metric="logloss",
        n_jobs=-1,
        random_state=0,
        verbosity=0,
    )

def calibrate_isotonic(model):
    # Isotonic, cv=3
    return CalibratedClassifierCV(estimator=model, method="isotonic", cv=3)


# %%
# %%
def expected_calibration_error(y_true, y_prob, n_bins=10):
    """ECE with equal-width probability bins."""
    y_true = np.asarray(y_true)
    y_prob = np.asarray(y_prob)

    bins = np.linspace(0.0, 1.0, n_bins + 1)
    which_bin = np.digitize(y_prob, bins) - 1

    ece = 0.0
    for b in range(n_bins):
        mask = which_bin == b
        if not np.any(mask):
            continue
        acc = y_true[mask].mean()
        conf = y_prob[mask].mean()
        ece += np.abs(acc - conf) * mask.mean()

    return ece


def fit_and_score_all_models(X_train, y_train, X_test, y_test):
    """Train base+calibrated models, return dict of metrics + prob vectors."""
    base_models = {
        "logistic": make_log_reg(),
        "rf":       make_rf(),
        "xgb":      make_xgb(),
    }

    models = {
        "logistic":     base_models["logistic"],
        "rf":           base_models["rf"],
        "xgb":          base_models["xgb"],
        "logistic_cal": calibrate_isotonic(make_log_reg()),
        "rf_cal":       calibrate_isotonic(make_rf()),
        "xgb_cal":      calibrate_isotonic(make_xgb()),
    }

    results = {}
    probs_cache = {}

    for name, model in models.items():
        model.fit(X_train, y_train)

        p = model.predict_proba(X_test)[:, 1]
        yhat = (p >= 0.5).astype(int)

        results[name] = dict(
            auc=roc_auc_score(y_test, p),
            accuracy=accuracy_score(y_test, yhat),
            logloss=log_loss(y_test, p),
            brier=brier_score_loss(y_test, p),
            ece=expected_calibration_error(y_test, p, n_bins=10),
        )

        probs_cache[name] = p

    return results, probs_cache


# %%
# %%
def reliability_diagram(y_true, y_prob, title, savepath, n_bins=10):
    y_true = np.asarray(y_true)
    y_prob = np.asarray(y_prob)

    bins = np.linspace(0.0, 1.0, n_bins + 1)
    which_bin = np.digitize(y_prob, bins) - 1

    xs, ys, ns = [], [], []
    for b in range(n_bins):
        mask = which_bin == b
        if not np.any(mask):
            continue
        xs.append(y_prob[mask].mean())
        ys.append(y_true[mask].mean())
        ns.append(mask.sum())

    plt.figure(figsize=(4,4), dpi=140)
    plt.plot([0,1],[0,1],"--",lw=1)
    plt.scatter(xs, ys, s=np.array(ns)*2.0, alpha=0.7)
    plt.xlim(0,1); plt.ylim(0,1)
    plt.gca().set_aspect("equal")
    plt.title(title)
    plt.xlabel("Predicted probability")
    plt.ylabel("Empirical accuracy")
    plt.grid(alpha=0.3)
    plt.tight_layout()
    plt.savefig(savepath, bbox_inches="tight")
    plt.close()


# %%
# %%
def run_label_noise_experiment(
    noise_levels=NOISE_LEVELS,
    n_samples=5000,
    random_state=0,
):
    """
    Flip labels with rate = nl, train models, collect metrics,
    and save reliability plots for EVERY noise level.
    """
    X, y = generate_base_data(n_samples=n_samples, random_state=random_state)

    rows = []
    reliability_paths = []

    for nl in tqdm(noise_levels, desc="Label noise levels"):
        y_noisy = flip_labels(y, nl, rng=_rng_for("label", nl))

        X_tr, X_te, y_tr, y_te = train_test_split(
            X,
            y_noisy,
            test_size=0.3,
            stratify=y_noisy,
            random_state=42,
        )

        metrics, probs = fit_and_score_all_models(X_tr, y_tr, X_te, y_te)

        for model_name, m in metrics.items():
            rec = {
                "experiment": "label_noise",
                "noise": nl,
                "model": model_name,
            }
            rec.update(m)
            rows.append(rec)

        # save reliability for EVERY nl, not just extremes
        for model_name, p in probs.items():
            fp = PLOTS_DIR / f"reliability_label_{nl:.1f}_{model_name}.png"
            reliability_diagram(
                y_te,
                p,
                f"{model_name} – reliability (label noise={nl:.1f})",
                fp,
            )
            reliability_paths.append(fp)

    df = pd.DataFrame(rows)
    return df, reliability_paths


# %%
# %%
def run_feature_noise_experiment(
    noise_levels=NOISE_LEVELS,
    n_samples=5000,
    mode="gaussian",
):
    """
    Add feature noise with strength = nl under the given mode,
    train models, collect metrics,
    and save reliability plots for EVERY noise level.
    """
    X, y = generate_base_data(n_samples=n_samples, random_state=0)

    rows = []
    reliability_paths = []

    for nl in tqdm(noise_levels, desc=f"{mode.capitalize()} noise levels"):
        Xn = add_feature_noise(X, nl, mode=mode, rng=_rng_for(mode, nl))

        X_tr, X_te, y_tr, y_te = train_test_split(
            Xn,
            y,
            test_size=0.3,
            stratify=y,
            random_state=42,
        )

        metrics, probs = fit_and_score_all_models(X_tr, y_tr, X_te, y_te)

        for model_name, m in metrics.items():
            rec = {
                "experiment": f"feature_noise_{mode}",
                "noise": nl,
                "model": model_name,
            }
            rec.update(m)
            rows.append(rec)

        # save reliability for EVERY nl
        for model_name, p in probs.items():
            fp = PLOTS_DIR / f"reliability_{mode}_{nl:.1f}_{model_name}.png"
            reliability_diagram(
                y_te,
                p,
                f"{model_name} – reliability ({mode} noise={nl:.1f})",
                fp,
            )
            reliability_paths.append(fp)

    df = pd.DataFrame(rows)
    return df, reliability_paths


# %%
# %%
def plot_metric_curve(df, experiment_name, metric, save_as):
    """
    Line plot of metric vs noise for each model (raw+calibrated).
    Calibrated variants end in _cal.
    """
    sub = df[df["experiment"] == experiment_name].copy()
    sub["is_cal"] = sub["model"].str.endswith("_cal")
    sub["base"] = sub["model"].str.replace("_cal$", "", regex=True)

    plt.figure(figsize=(6,4), dpi=140)
    for base_model in sorted(sub["base"].unique()):
        raw = sub[(sub["base"] == base_model) & (~sub["is_cal"])].sort_values("noise")
        cal = sub[(sub["base"] == base_model) & ( sub["is_cal"])].sort_values("noise")

        if not raw.empty:
            plt.plot(
                raw["noise"], raw[metric],
                "o-", lw=1.5,
                label=f"{base_model} (raw)"
            )
        if not cal.empty:
            plt.plot(
                cal["noise"], cal[metric],
                "o--", lw=1.2,
                label=f"{base_model} (cal)"
            )

    if metric in ("ece", "brier", "logloss"):
        ylabel = f"{metric.upper()} (lower is better)"
    else:
        ylabel = metric.upper()

    plt.xlabel("Noise level")
    plt.ylabel(ylabel)
    plt.title(experiment_name.replace("_", " ") + f" — {metric}")
    plt.grid(alpha=0.3)
    plt.legend(fontsize=8)
    plt.tight_layout()
    plt.savefig(save_as, bbox_inches="tight")
    plt.close()


# %%
# %%
print("Running experiments...")

df_label, rel_label = run_label_noise_experiment(
    noise_levels=NOISE_LEVELS,
    n_samples=N_DATA,
)

df_gauss, rel_gauss = run_feature_noise_experiment(
    noise_levels=NOISE_LEVELS,
    n_samples=N_DATA,
    mode="gaussian",
)

df_lap, rel_lap = run_feature_noise_experiment(
    noise_levels=NOISE_LEVELS,
    n_samples=N_DATA,
    mode="laplace",
)


print("Merging results...")
df_all = pd.concat([df_label, df_gauss, df_lap], ignore_index=True)

csv_path = RESULTS_DIR / f"noisy_experiments_results_{BASE_SEED}.csv"
df_all.to_csv(csv_path, index=False)
print("Results CSV ->", csv_path)

# metrics = ["auc","accuracy","logloss","brier","ece"]
# experiments = [
#     ("label_noise", df_label),
#     ("feature_noise_gaussian", df_gauss),
#     ("feature_noise_laplace", df_lap),
# ]

# print("Plotting metrics...")
# for exp_name, df_exp in experiments:
#     for metric in metrics:
#         out_path = PLOTS_DIR / f"{exp_name}_{metric}.png"
#         plot_metric_curve(df_exp, exp_name, metric, out_path)

# print("Done.")


# %%
# %%
import pandas as pd
import matplotlib.pyplot as plt
from pathlib import Path
import numpy as np

# -------------------------------------------------
# Load results
# -------------------------------------------------
df = pd.read_csv(f"results/noisy_experiments_results_{BASE_SEED}.csv")

# enforce numeric just in case pandas read something weird
df["noise"] = df["noise"].astype(float)

# palette: consistent, readable
COLOR_MAP = {
    "logistic": "#1f77b4",  # blue
    "rf":       "#ff7f0e",  # orange
    "xgb":      "#2ca02c",  # green
}

# which experiments, and pretty labels
EXPERIMENT_ORDER = [
    ("label_noise", "Label Noise"),
    ("feature_noise_gaussian", "Feature Noise (Gaussian)"),
    ("feature_noise_laplace",  "Feature Noise (Laplace)"),
]

PLOTS_DIR = Path("plots/analytics")
PLOTS_DIR.mkdir(exist_ok=True, parents=True)

def plot_panel(ax, subdf, metric, ylabel, xmin, xmax):
    """
    subdf: df filtered to one experiment
    metric: "auc" or "ece"
    ax: matplotlib Axes
    xmin/xmax: global x-range for this experiment (so 0.45 doesn't get clipped)
    """

    subdf = subdf.copy()
    subdf["is_cal"] = subdf["model"].str.endswith("_cal")
    subdf["base"] = subdf["model"].str.replace("_cal$", "", regex=True)

    for base_model in ["logistic", "rf", "xgb"]:
        color = COLOR_MAP[base_model]

        raw = (
            subdf[(subdf["base"] == base_model) & (~subdf["is_cal"])]
            .sort_values("noise")
        )
        cal = (
            subdf[(subdf["base"] == base_model) & ( subdf["is_cal"])]
            .sort_values("noise")
        )

        if not raw.empty:
            ax.plot(
                raw["noise"],
                raw[metric],
                marker="o",
                linestyle="-",
                linewidth=1.8,
                markersize=4.5,
                color=color,
                label=f"{base_model} (raw)",
            )
        if not cal.empty:
            ax.plot(
                cal["noise"],
                cal[metric],
                marker="o",
                linestyle="--",
                linewidth=1.4,
                markersize=4.5,
                color=color,
                label=f"{base_model} (cal)",
            )

    ax.set_xlabel("Noise level")
    ax.set_ylabel(ylabel)
    ax.grid(alpha=0.3)

    # pad y a bit
    ymin, ymax = ax.get_ylim()
    yrange = ymax - ymin
    ax.set_ylim(ymin - 0.05 * yrange, ymax + 0.05 * yrange)

    # *** hard clamp x-range so 0.45 shows up ***
    pad = 0.01
    ax.set_xlim(xmin - pad, xmax + pad)


# -------------------------------------------------
# build the 3x2 grid
# -------------------------------------------------
fig, axes = plt.subplots(
    nrows=3,
    ncols=2,
    figsize=(10, 10),
    dpi=150,
    sharex=False,   # important: each row can now have its own xlim including 0.45
)

for row_idx, (exp_key, exp_title) in enumerate(EXPERIMENT_ORDER):
    sub = df[df["experiment"] == exp_key].copy()

    # numeric sanity again just in case
    sub["noise"] = sub["noise"].astype(float)

    xmin = sub["noise"].min()
    xmax = sub["noise"].max()

    # left col: AUC
    ax_auc = axes[row_idx, 0]
    plot_panel(ax_auc, sub, "auc", f"{exp_title}\nAUC (↑ better)", xmin, xmax)
    if row_idx == 0:
        ax_auc.set_title("Discrimination")

    # right col: ECE
    ax_ece = axes[row_idx, 1]
    plot_panel(ax_ece, sub, "ece", f"{exp_title}\nECE (↓ better)", xmin, xmax)
    if row_idx == 0:
        ax_ece.set_title("Calibration Error")

# legend from all lines (dedup)
handles, labels = [], []
for ax in axes.flatten():
    for line in ax.get_lines():
        lbl = line.get_label()
        if lbl not in labels:
            labels.append(lbl)
            handles.append(line)

fig.legend(
    handles,
    labels,
    loc="lower center",
    ncol=3,
    frameon=False,
    fontsize=9,
    handlelength=2.5,
    columnspacing=1.5,
)

plt.tight_layout(rect=[0, 0.07, 1, 1])

out_path = PLOTS_DIR / f"summary_grid_{BASE_SEED}.png"
plt.savefig(out_path, bbox_inches="tight")
 

print(f"Saved grid figure to {out_path}")


```
