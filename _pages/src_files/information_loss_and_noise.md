---
layout: single
permalink: /src_noise_info_loss/
title: "src_noise_info_loss"
--- 


```
import numpy as np
from scipy.stats import laplace
from sklearn.metrics import mutual_info_score
import matplotlib.pyplot as plt
from pathlib import Path
import csv

# %%
def generate_base_data(n=100_000, low=0.0, high=100.0, rng=None):
    if rng is None:
        rng = np.random.default_rng()
    return rng.uniform(low, high, size=n)

# def generate_base_data(n=100_000, low=0.0, high=100.0, rng=None):
#     if rng is None:
#         rng = np.random.default_rng()
#     ages = rng.normal(loc=45, scale=18, size=n)
#     ages = np.clip(ages, 0, 100)
#     return ages


# %%
def apply_binning(X, width):
    return np.floor(X / width) * width

# %%
def apply_laplace_noise(X, b, rng=None):
    if rng is None:
        rng = np.random.default_rng()
    noise = rng.laplace(loc=0.0, scale=b, size=X.shape[0])
    return X + noise

# %%
def discretize(values, bin_width):
    return np.floor(values / bin_width).astype(int)

# %%
def shannon_entropy(discrete_values):
    vals, counts = np.unique(discrete_values, return_counts=True)
    p = counts / counts.sum()
    return -np.sum(p * np.log(p))

# %%
def mutual_information(discrete_x, discrete_y):
    return mutual_info_score(discrete_x, discrete_y)

# %%
def evaluate_mechanism(X, X_released, attacker_bin_width=1.0):
    X_disc = discretize(X, attacker_bin_width)
    Y_disc = discretize(X_released, attacker_bin_width)
    H_X = shannon_entropy(X_disc) / np.log(2)
    H_Y = shannon_entropy(Y_disc) / np.log(2)
    I_XY = mutual_information(X_disc, Y_disc) / np.log(2)
    return {"H_X_bits": H_X, "H_Y_bits": H_Y, "I_bits": I_XY}

# %%
def sweep_laplace(X, b_values, rng=None):
    if rng is None:
        rng = np.random.default_rng()
    out = []
    for b in b_values:
        X_noisy = apply_laplace_noise(X, b=b, rng=rng)
        metrics = evaluate_mechanism(X, X_noisy)
        metrics.update({"type": "laplace", "b": b})
        out.append(metrics)
    return out

# %%
def sweep_binning(X, bin_widths):
    out = []
    for w in bin_widths:
        X_binned = apply_binning(X, width=w)
        metrics = evaluate_mechanism(X, X_binned)
        metrics.update({"type": "bin", "w": w})
        out.append(metrics)
    return out

# %%
def make_pretty_plot(laplace_results, bin_results, out_path="plots/info_loss_vs_b_pretty.png"):
    # Prepare data
    b_list = np.array([r["b"] for r in laplace_results])
    I_list = np.array([r["I_bits"] for r in laplace_results])
    order = np.argsort(b_list)
    b_list, I_list = b_list[order], I_list[order]

    w_list = np.array([r["w"] for r in bin_results])
    Iw_list = np.array([r["I_bits"] for r in bin_results])

    # Match Laplace b to each bin's I
    b_match, I_match = [], []
    for Iw in Iw_list:
        idx = np.argmin(np.abs(I_list - Iw))
        b_match.append(b_list[idx])
        I_match.append(I_list[idx])

    # Plot
    fig, ax = plt.subplots(figsize=(7, 4))
    ax.plot(b_list, I_list, "o-", color="black", lw=2, label="Laplace noise") 
    colors = ["#7F3C1F", "#B55A30", "#DFA46A"]  # dark copper, mid, pale gold 


    styles = ["--", "-.", ":"]

    for (w, Iw, bm, Im, color, ls) in zip(w_list, Iw_list, b_match, I_match, colors, styles):
        ax.hlines(Iw, b_list.min(), b_list.max(), color=color, lw=2, linestyle=ls, alpha=0.9)
        ax.text(b_list.max() * 1.03, Iw, f"{int(w)}-year bins", color=color,
                va="center", ha="left", fontsize=9)
        ax.vlines(bm, min(Im, Iw), max(Im, Iw), color=color, linestyle=":", alpha=0.7)
        ax.scatter([bm], [Iw], s=45, color=color, edgecolor="k", zorder=5)
        ax.text(bm, Iw + 0.05, f"b≈{bm:.2f}", color=color, fontsize=8, ha="center")

    ax.set_xlabel("Laplace noise scale b")
    ax.set_ylabel("Mutual information I(X; released) [bits]")
    ax.set_title("Mapping Laplace noise to Information Loss and equivalent binning")
    ax.set_xlim(left=0, right=max(b_list) * 1.15)
    ax.set_ylim(bottom=0)
    ax.legend(frameon=False, loc="upper right")

    plt.tight_layout()
    Path(out_path).parent.mkdir(parents=True, exist_ok=True)
    fig.savefig(out_path, dpi=300)
    plt.close(fig)

# %%
rng = np.random.default_rng(42)
X = generate_base_data(n=100_000, low=0.0, high=100.0, rng=rng)

b_values = [0.1, 0.2, 0.5, 1.0, 2.0, 3.0, 5.0]
b_values = [
    0.1, 0.3, 0.5,
    0.7, 1.0, 1.5, 2.0,
    2.5, 3.0, 3.5, 4.0, 4.5, 5.0
]
w_values = [1.0, 5.0, 10.0]

laplace_results = sweep_laplace(X, b_values, rng=rng)
bin_results = sweep_binning(X, w_values)

make_pretty_plot(laplace_results, bin_results)

# Save CSV for reference
Path("plots").mkdir(exist_ok=True, parents=True)
with open("plots/results_summary.csv", "w", newline="") as f:
    writer = csv.writer(f)
    writer.writerow(["mechanism", "b_or_w", "I_bits", "H_X_bits", "H_Y_bits"])
    for r in laplace_results:
        writer.writerow(["laplace", r["b"], r["I_bits"], r["H_X_bits"], r["H_Y_bits"]])
    for r in bin_results:
        writer.writerow(["bin", r["w"], r["I_bits"], r["H_X_bits"], r["H_Y_bits"]])


```
