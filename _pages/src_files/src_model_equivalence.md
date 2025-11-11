---
layout: single
permalink: /src-model-equivalence/
title: "src_model_equivalence"
--- 

Full_run.py
```
# %%
# A1. Setup & data
import numpy as np
from sklearn.datasets import make_classification
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier

SEED = 7
X, y = make_classification(
    n_samples=8000, n_features=6, n_informative=5, n_redundant=1,
    n_clusters_per_class=2, class_sep=1.6, random_state=SEED
)
X_tr, X_tmp, y_tr, y_tmp = train_test_split(X, y, test_size=0.40, random_state=SEED)
X_val, X_te, y_val, y_te = train_test_split(X_tmp, y_tmp, test_size=0.50, random_state=SEED)

# Domain bounds (box) for verification — tighten if needed
lo = X_tr.min(axis=0)
hi = X_tr.max(axis=0)

# A2. Large forest
big = RandomForestClassifier(
    n_estimators=60, max_depth=8, min_samples_leaf=2,
    random_state=SEED, n_jobs=-1
).fit(X_tr, y_tr)

print("Big RF — train/val acc:",
      (big.score(X_tr, y_tr), big.score(X_val, y_val)))


# %%
from copy import deepcopy
from sklearn.metrics import accuracy_score

def prune_forest_by_val_greedy(rf: RandomForestClassifier, X_val, y_val, target_trees: int):
    """Drop trees that least reduce validation accuracy, until n_estimators == target_trees."""
    if target_trees >= len(rf.estimators_):
        return deepcopy(rf)

    keep = list(range(len(rf.estimators_)))
    rf_work = deepcopy(rf)

    def forest_pred_on(estim_idx):
        # average votes from the selected subset of estimators
        estims = [rf.estimators_[i] for i in estim_idx]
        proba = sum(e.predict_proba(X_val) for e in estims) / len(estims)
        return (proba[:,1] >= 0.5).astype(int)

    base_acc = accuracy_score(y_val, forest_pred_on(keep))
    while len(keep) > target_trees:
        # test dropping each tree; pick the one whose removal keeps acc highest
        best_drop, best_acc = None, -1.0
        for i in keep:
            cand = [j for j in keep if j != i]
            acc = accuracy_score(y_val, forest_pred_on(cand))
            if acc >= best_acc:
                best_acc, best_drop = acc, i
        keep.remove(best_drop)

    pruned = deepcopy(rf)
    pruned.estimators_ = [rf.estimators_[i] for i in keep]
    pruned.n_estimators = len(pruned.estimators_)
    return pruned, keep

pruned, kept_idx = prune_forest_by_val_greedy(big, X_val, y_val, target_trees=18)
print("Pruned RF — trees kept:", len(kept_idx))
print("Big vs Pruned val acc:", big.score(X_val, y_val), pruned.score(X_val, y_val))


# %%
# C1. Z3 imports
from z3 import Real, Bool, And, Or, Not, If, Solver, sat

def encode_sklearn_tree_as_z3(tree, x_vars):
    """
    Returns a Z3 expression for a sklearn DecisionTreeClassifier:
      output in {0,1} = class argmax at the reached leaf.
    """
    t = tree.tree_
    feat = t.feature
    thresh = t.threshold
    children_left = t.children_left
    children_right = t.children_right
    values = t.value  # shape [nodes, 1, n_classes]

    def node_expr(idx):
        if children_left[idx] == children_right[idx]:  # leaf
            counts = values[idx][0]
            pred_class = int(np.argmax(counts))
            return RealVal(pred_class)
        f = feat[idx]
        thr = thresh[idx]
        cond = (x_vars[f] <= thr)
        return If(cond, node_expr(children_left[idx]), node_expr(children_right[idx]))

    from z3 import RealVal
    return node_expr(0)

def encode_forest_as_z3_avg_vote(rf: RandomForestClassifier, x_vars):
    """Average of tree votes (each 0/1)."""
    from z3 import Sum, ToReal
    tree_exprs = [encode_sklearn_tree_as_z3(t, x_vars) for t in rf.estimators_]
    # average = sum / n_trees (keep as real)
    return Sum(*tree_exprs) / len(tree_exprs)

def make_box_constraints(x_vars, lo, hi):
    cons = []
    for i, xi in enumerate(x_vars):
        cons += [xi >= lo[i], xi <= hi[i]]
    return And(*cons)


# %%
# D1. Build Z3 problem
from z3 import RealVal

d = X.shape[1]
x = [Real(f"x{i}") for i in range(d)]

big_out   = encode_forest_as_z3_avg_vote(big, x)
prun_out  = encode_forest_as_z3_avg_vote(pruned, x)

def to_label(expr):  # >= 0.5 ⇔ class 1
    return If(expr >= RealVal(0.5), RealVal(1), RealVal(0))

s = Solver()
s.add(make_box_constraints(x, lo, hi))
s.add(to_label(big_out) != to_label(prun_out))   # ask for a disagreement

# D2. Check
res = s.check()
if res == sat:
    m = s.model()
    cex = np.array([float(m[xi].as_decimal(10).replace("?", "")) for xi in x], dtype=float)
    print("❌ Counterexample found (big vs pruned differ):", cex)
else:
    print("✅ Equivalent on the bounded box [lo, hi].")


# %%
x_cex = cex.reshape(1, -1)
print("big:",    big.predict(x_cex), big.predict_proba(x_cex)[0])
print("pruned:", pruned.predict(x_cex), pruned.predict_proba(x_cex)[0])


# %%
rng = np.random.default_rng(0)
Z = rng.uniform(lo, hi, size=(20000, len(lo)))
emp = (big.predict(Z) != pruned.predict(Z)).mean()
print("sampled disagree rate:", emp)


# %% [markdown]
# ### Extras

# %%
import numpy as np

def tree_leaf_and_path(dt, x):
    """
    Returns (leaf_class, path_node_indices) for one sklearn DecisionTreeClassifier and 1×d x.
    """
    t = dt.tree_
    node = 0
    path = [0]
    while t.children_left[node] != t.children_right[node]:
        f = t.feature[node]
        thr = t.threshold[node]
        if x[0, f] <= thr:
            node = t.children_left[node]
        else:
            node = t.children_right[node]
        path.append(node)
    # leaf class = argmax counts at leaf
    cls = int(np.argmax(t.value[node][0]))
    return cls, path

def pretty_path(dt, path, feature_names=None, x=None):
    """Human-readable path constraints."""
    t = dt.tree_
    out = []
    for i in range(len(path)-1):
        n = path[i]
        f = t.feature[n]; thr = t.threshold[n]
        left = t.children_left[n]; right = t.children_right[n]
        name = feature_names[f] if feature_names is not None else f"x[{f}]"
        went_left = (path[i+1] == left)
        cond = f"{name} <= {thr:.6g}" if went_left else f"{name} > {thr:.6g}"
        if x is not None:
            cond += f"  (x={x[0,f]:.6g})"
        out.append(cond)
    return " ∧ ".join(out)

def trace_forest_disagreement(x_cex, big, pruned, feature_names=None, top_k=10):
    """
    Prints:
      - forest votes
      - per-tree votes
      - trees that differ between big and pruned on x_cex
      - path constraints for a few differing trees
      - greedy minimal subset of kept trees whose removal flips big's vote on x_cex
    """
    xb = x_cex.reshape(1, -1)

    # Forest-level
    big_prob   = np.mean([t.predict(xb)[0] for t in big.estimators_])
    prun_prob  = np.mean([t.predict(xb)[0] for t in pruned.estimators_])
    print(f"[forest] big: prob1={big_prob:.6f}, pred={int(big_prob>=0.5)}")
    print(f"[forest] pruned: prob1={prun_prob:.6f}, pred={int(prun_prob>=0.5)}")

    # Per-tree votes
    big_votes  = np.array([t.predict(xb)[0] for t in big.estimators_], dtype=int)
    prun_votes = np.array([t.predict(xb)[0] for t in pruned.estimators_], dtype=int)

    # Trees present in pruned forest
    kept = set(id(t) for t in pruned.estimators_)
    kept_idx = [i for i,t in enumerate(big.estimators_) if id(t) in kept]

    # Differences among kept trees (structure identical; prediction might differ if you later distill/simplify)
    diff_idx = [i for i in kept_idx if big.estimators_[i].predict(xb)[0] != pruned.estimators_[kept_idx.index(i)].predict(xb)[0]]
    print(f"[kept trees] disagreeing predictions: {len(diff_idx)} / {len(kept_idx)}")

    # Differences due to pruned-away trees (vote lost vs kept)
    removed_idx = [i for i in range(len(big.estimators_)) if i not in kept_idx]
    removed_vote = big_votes[removed_idx].mean() if removed_idx else np.nan
    print(f"[removed trees] count={len(removed_idx)}, mean vote={removed_vote}")

    # Show a few paths that vote 1 vs 0 in BIG (useful to see why vote changed)
    # Pick top_k trees with largest absolute contribution change after pruning
    if len(removed_idx):
        # effect = how much average vote would drop if this single tree were removed
        base = big_votes.mean()
        effects = []
        for i in removed_idx:
            new_mean = (big_votes.sum() - big_votes[i]) / (len(big_votes) - 1)
            effects.append((abs(base - new_mean), i))
        effects.sort(reverse=True)
        show = [j for _, j in effects[:min(top_k, len(effects))]]
        print(f"[removed trees] top contributors (by single-tree effect on mean vote): {show}")
        for i in show:
            leaf, path = tree_leaf_and_path(big.estimators_[i], xb)
            print(f"  - tree#{i} vote={leaf} | path: {pretty_path(big.estimators_[i], path, feature_names, xb)}")

    # Minimal subset of kept trees whose removal flips BIG prediction at x_cex (greedy)
    # Insight: identifies “responsible coalition” for the decision at this x
    target_label = int(big_prob >= 0.5)
    votes = big_votes.copy().astype(float)
    idxs = list(range(len(votes)))
    current_mean = votes.mean()
    coalition = []
    while int(current_mean >= 0.5) == target_label and idxs:
        best_drop, best_mean = None, None
        for i in idxs:
            new_mean = (votes.sum() - votes[i]) / (len(idxs) - 1) if len(idxs) > 1 else (1.0 - votes[i])  # degenerate
            if (best_mean is None) or (abs(new_mean - 0.5) < abs(best_mean - 0.5)):
                best_drop, best_mean = i, new_mean
        coalition.append(best_drop)
        idxs.remove(best_drop)
        current_mean = (votes.sum() - votes[coalition].sum()) / (len(votes) - len(coalition))
    print(f"[minimal-ish coalition] #trees to flip BIG at x_cex (greedy): {len(coalition)}")
    return {
        "big_prob": big_prob, "pruned_prob": prun_prob,
        "removed_idx": removed_idx, "diff_idx": diff_idx, "coalition": coalition
    }


# %%
_ = trace_forest_disagreement(cex, big, pruned, feature_names=None, top_k=8)


# %% [markdown]
# ### margin calls
# 

# %%
from z3 import Solver, Real, RealVal, And, Or, Sum, ToReal, If, sat

def z3_counterexample_margin(big, pruned, lo, hi, eps=0.10):
    d = len(lo)
    x = [Real(f"x{i}") for i in range(d)]

    big_out  = encode_forest_as_z3_avg_vote(big, x)
    prun_out = encode_forest_as_z3_avg_vote(pruned, x)

    s = Solver()
    s.add(make_box_constraints(x, lo, hi))
    # margin condition:
    s.add( Or(big_out - prun_out >= RealVal(eps),
              prun_out - big_out >= RealVal(eps)) )

    if s.check() == sat:
        m = s.model()
        cex = np.array([float(m[xi].as_decimal(20).replace("?", "")) for xi in x], dtype=float)
        return cex
    return None

# Example:
cex_margin = z3_counterexample_margin(big, pruned, lo, hi, eps=0.25)
print("margin-CE:", cex_margin)
if cex_margin is not None:
    print("big/pruned probs at margin-CE:",
          np.mean([t.predict(cex_margin.reshape(1,-1))[0] for t in big.estimators_]),
          np.mean([t.predict(cex_margin.reshape(1,-1))[0] for t in pruned.estimators_]))


# %% [markdown]
# ### viz

# %%
# z3_rf_viz.py
import numpy as np
import matplotlib.pyplot as plt

# ---------- smoothing (scipy optional) ----------
def _smooth(Z, sigma):
    if sigma is None or sigma <= 0:
        return Z
    try:
        from scipy.ndimage import gaussian_filter  # noqa
        return gaussian_filter(Z, sigma=float(sigma))
    except Exception:
        # tiny separable box blur fallback
        k = max(1, int(round(sigma * 2)))
        if k % 2 == 0: k += 1
        pad = k // 2
        Zp = np.pad(Z, pad, mode="edge")
        W = np.ones((k, k), dtype=float) / (k * k)
        out = np.zeros_like(Z)
        for i in range(out.shape[0]):
            for j in range(out.shape[1]):
                out[i, j] = (Zp[i:i+k, j:j+k] * W).sum()
        return out

# ---------- core helpers ----------
def rf_vote_prob(estimators, X):
    """Mean per-tree P(class=1)."""
    return np.mean([t.predict_proba(X)[:, 1] for t in estimators], axis=0)

def _grid(lo, hi, center, i, j, n):
    xs = np.linspace(lo[i], hi[i], n)
    ys = np.linspace(lo[j], hi[j], n)
    XX, YY = np.meshgrid(xs, ys)
    base = np.tile(center, (n * n, 1))
    for r in range(n):
        base[r * n:(r + 1) * n, i] = XX[r]
        base[r * n:(r + 1) * n, j] = YY[r]
    return xs, ys, base

def best_dims_for_disagreement(big, pruned, lo, hi, samples=4000, rng=0):
    """Pick (i,j) where |Δvote| shows the most structure (variance over coarse grid)."""
    r = np.random.default_rng(rng)
    X = r.uniform(lo, hi, size=(samples, len(lo)))
    dv = np.abs(rf_vote_prob(big.estimators_, X) - rf_vote_prob(pruned.estimators_, X))
    d = len(lo); bins = 16
    scores = {}
    for i in range(d):
        for j in range(i + 1, d):
            bi = np.clip(((X[:, i] - lo[i]) / (hi[i] - lo[i]) * bins).astype(int), 0, bins - 1)
            bj = np.clip(((X[:, j] - lo[j]) / (hi[j] - lo[j]) * bins).astype(int), 0, bins - 1)
            grid_sum = np.zeros((bins, bins)); grid_cnt = np.zeros((bins, bins))
            for k in range(len(X)):
                grid_sum[bi[k], bj[k]] += dv[k]; grid_cnt[bi[k], bj[k]] += 1
            with np.errstate(invalid='ignore', divide='ignore'):
                grid = grid_sum / grid_cnt
            scores[(i, j)] = np.nanvar(grid)
    return max(scores, key=scores.get)

def _imshow_copper(ZZ, xs, ys, title, cbar_label, xlabel=None, ylabel=None, vmin=None, vmax=None):
    if vmin is None or vmax is None:
        finite = ZZ[np.isfinite(ZZ)]
        if finite.size:
            vmin = np.nanpercentile(finite, 5)
            vmax = np.nanpercentile(finite, 95)

    fig, ax = plt.subplots(figsize=(6, 5))
    im = ax.imshow(
        ZZ,
        extent=[xs.min(), xs.max(), ys.min(), ys.max()],
        origin="lower",
        aspect="equal",
        cmap="copper",
        vmin=vmin,
        vmax=vmax,
    )
    cbar = fig.colorbar(im, ax=ax)
    cbar.set_label(cbar_label)

    # ✅ axis labels restored
    if xlabel is not None:
        ax.set_xlabel(xlabel)
    if ylabel is not None:
        ax.set_ylabel(ylabel)

    ax.set_title(title)
    fig.tight_layout()
    plt.show()


# ---------- visuals ----------
def plot_vote_diff_slice(
    big, pruned, lo, hi, *, center=None, dims=None, n=220, pts=None,
    eps=None, smooth_sigma=1.0, title="|Δ vote probability| on 2D slice"
):
    """
    Heatmap of |P_big(1) - P_pruned(1)| on a 2D slice.
    Args:
      center: fixed values for other dims (default: mid-box)
      dims: (i,j) to plot (default: auto via best_dims_for_disagreement)
      n: grid resolution (use ~150–250 for readability)
      eps: if set, mask values < eps
      smooth_sigma: gaussian sigma (or box-blur fallback) for visual smoothing
    """
    d = len(lo)
    if center is None: center = (lo + hi) / 2.0
    if dims is None: dims = best_dims_for_disagreement(big, pruned, lo, hi)
    i, j = dims
    xs, ys, base = _grid(lo, hi, center, i, j, n)

    vb = rf_vote_prob(big.estimators_, base)
    vp = rf_vote_prob(pruned.estimators_, base)
    ZZ = np.abs(vb - vp).reshape(n, n)

    ZZ = _smooth(ZZ, smooth_sigma)
    if eps is not None:
        ZZ = np.where(ZZ >= eps, ZZ, np.nan)

    _imshow_copper(
        ZZ, xs, ys, title,
        cbar_label="|Δ vote prob|",
        xlabel=f"x[{i}]",
        ylabel=f"x[{j}]"
    )


    # overlay points
    if pts:
        plt.figure();  # small overlay figure for markers only (no replot)
        plt.close()  # keep API simple; users can scatter on their own if they want

def plot_label_disagreement_region(
    big, pruned, lo, hi, *, center=None, dims=None, n=220, pts=None,
    smooth_sigma=0.0, title="Label disagreement region"
):
    d = len(lo)
    if center is None: center = (lo + hi) / 2.0
    if dims is None: dims = best_dims_for_disagreement(big, pruned, lo, hi)
    i, j = dims
    xs, ys, base = _grid(lo, hi, center, i, j, n)

    yb = (rf_vote_prob(big.estimators_, base) >= 0.5).astype(int)
    yp = (rf_vote_prob(pruned.estimators_, base) >= 0.5).astype(int)
    D = (yb != yp).reshape(n, n).astype(float)
    D = _smooth(D, smooth_sigma)

    _imshow_copper(
        D, xs, ys, title,
        cbar_label="disagree=1 / agree=0",
        xlabel=f"x[{i}]",
        ylabel=f"x[{j}]"
    )


def plot_removed_tree_effects_at_x(
    big, pruned, x_cex, top_k=15, title="Top removed trees at CE"
):
    xb = x_cex.reshape(1, -1)
    big_votes = np.array([t.predict_proba(xb)[:, 1][0] for t in big.estimators_], dtype=float)
    kept_ids = {id(t) for t in pruned.estimators_}
    removed = [i for i, t in enumerate(big.estimators_) if id(t) not in kept_ids]
    if not removed:
        print("No removed trees."); return

    base = big_votes.mean()
    eff = []
    for i in removed:
        new_mean = (big_votes.sum() - big_votes[i]) / (len(big_votes) - 1)
        eff.append((abs(base - new_mean), i))
    eff.sort(reverse=True)
    eff = eff[:min(top_k, len(eff))]
    deltas = [e[0] for e in eff]; idxs = [e[1] for e in eff]

    plt.figure(figsize=(8, 4))
    plt.bar(range(len(eff)), deltas, color="#b87333")
    plt.xticks(range(len(eff)), idxs, rotation=45)
    plt.ylabel("Δ avg vote if removed"); plt.title(title)
    plt.tight_layout(); plt.show()

def plot_conflict_where_big_confident(
    big, pruned, lo, hi, *, center=None, dims=None, n=220, m=0.2,
    title="Pruned disagrees where BIG margin is high"
):
    d = len(lo)
    if center is None: center = (lo + hi) / 2.0
    if dims is None: dims = best_dims_for_disagreement(big, pruned, lo, hi)
    i, j = dims
    xs, ys, base = _grid(lo, hi, center, i, j, n)

    vb = rf_vote_prob(big.estimators_, base)
    yb = (vb >= 0.5).astype(int)
    yp = (rf_vote_prob(pruned.estimators_, base) >= 0.5).astype(int)
    confident = (vb >= 0.5 + m) | (vb <= 0.5 - m)
    conflict = (yb != yp) & confident
    Z = conflict.reshape(n, n).astype(float)

    _imshow_copper(
        Z, xs, ys, title,
        cbar_label=f"disagree & margin≥{m}",
        xlabel=f"x[{i}]",
        ylabel=f"x[{j}]"
    )



# %%
pts = [] 
if 'cex' in globals(): pts.append(cex)
if 'cex_margin' in globals() and cex_margin is not None: pts.append(cex_margin)

plot_vote_diff_slice(big, pruned, lo, hi, center=(lo+hi)/2, dims=None, n=300, pts=pts, eps=0.06)

# 2) Show where labels differ on that slice
plot_label_disagreement_region(big, pruned, lo, hi, center=(lo+hi)/2, dims=None, n=300, pts=pts)

# 3) Explain which removed trees mattered at a specific CE
if 'cex' in globals():
    plot_removed_tree_effects_at_x(big, pruned, cex, top_k=12)

# 4) Safety view: disagreements only where BIG is confident by ≥ 0.2 margin
plot_conflict_where_big_confident(big, pruned, lo, hi, center=(lo+hi)/2, dims=None, n=300, m=0.05)

# 5) (Optional) Force the slice through a particular CE and feature pair
# dims=(0,3) or any other two indices; center=cex to slice through the counterexample
if 'cex' in globals():
    plot_vote_diff_slice(big, pruned, lo, hi, center=cex, dims=(0,3), n=350, pts=[cex], eps=0.05)


```