---
layout: single
permalink: /src-z3-overconfidence/
title: "src_z3_overconfidence"
--- 

Full_run.py
```
# %%
 
import argparse, json, math, os
import numpy as np
from sklearn.datasets import load_digits, make_classification
from sklearn.model_selection import train_test_split
from sklearn.neural_network import MLPClassifier
from sklearn.metrics import accuracy_score
import z3
import torch, torch.nn as nn, torch.nn.functional as F
import matplotlib.pyplot as plt

def wilson_lcb(correct: int, total: int, z: float = 1.96) -> float:
    if total <= 0: return 0.0
    p = correct / total
    denom  = 1.0 + (z*z)/total
    center = (p + (z*z)/(2*total)) / denom
    margin = z * math.sqrt((p*(1-p) + (z*z)/(4*total)) / total) / denom
    return max(0.0, center - margin)

def make_ood_like(X, rng: np.random.Generator, noise_sigma=0.8):
    Xs = X[:, rng.permutation(X.shape[1])]
    Xs = np.clip(Xs + rng.normal(0, noise_sigma, Xs.shape), 0, 1)
    return Xs

def temp_hack(probs, factor=8.0):
    p = probs ** factor
    return p / p.sum(axis=1, keepdims=True)

def make_imbalance(seed=0, n_samples=4000):
    Xb, yb = make_classification(
        n_samples=n_samples, n_features=32, n_informative=6, n_redundant=2,
        weights=[0.98, 0.02], random_state=seed
    )
    Xtrb, Xtb, ytrb, ytb = train_test_split(Xb, yb, test_size=0.5, random_state=seed, stratify=yb)
    clf_b = MLPClassifier(hidden_layer_sizes=(32,), max_iter=200, random_state=seed)
    clf_b.fit(Xtrb, ytrb)
    probs_b = clf_b.predict_proba(Xtb)
    preds_b = probs_b.argmax(axis=1)
    acc_b = accuracy_score(ytb, preds_b)
    return probs_b, ytb, acc_b

def build_bins(conf, acc, num_bins=6, wilson_z=1.96):
    edges = np.linspace(0.0, 1.0, num_bins+1)
    meta = []
    for i in range(num_bins):
        lo, hi = edges[i], edges[i+1]
        mask = (conf >= lo) & (conf < hi if i < num_bins-1 else conf <= hi)
        n = int(mask.sum())
        if n == 0: continue
        correct = int(acc[mask].sum())
        L = wilson_lcb(correct, n, wilson_z)
        meta.append({"bin": i, "lo": float(lo), "hi": float(hi),
                     "conf": float(conf[mask].mean()), "LCB": float(L), "support": n})
    return meta

def plot_bins(meta, out_path="calibration_plot.png", title="Calibration bins"):
    bins = [b["bin"] for b in meta]
    conf = [b["conf"] for b in meta]
    LCB  = [b["LCB"] for b in meta]
    plt.figure(figsize=(8,4))
    plt.plot(bins, conf, marker="o", label="mean_confidence")
    plt.plot(bins, LCB, marker="o", label="LCB_accuracy")
    plt.title(title); plt.xlabel("bin index"); plt.ylabel("value")
    plt.legend(); plt.grid(True); plt.tight_layout()
    plt.savefig(out_path, dpi=180); plt.close()

def z3_prob_vector_for_violating_bin(meta, epsilon, num_classes):
    vb = max(meta, key=lambda b: b["conf"] - b["LCB"])
    lo, hi, LCB = vb["lo"], vb["hi"], vb["LCB"]
    s = z3.Solver()
    p = [z3.Real(f"p_{i}") for i in range(num_classes)]
    pred = [z3.Bool(f"pred_{i}") for i in range(num_classes)]
    for i in range(num_classes): s.add(p[i] >= 0)
    s.add(z3.Sum(p) == 1)
    s.add(z3.PbEq([(pred[i], 1) for i in range(num_classes)], 1))
    conf_expr = z3.Sum([z3.If(pred[i], p[i], 0) for i in range(num_classes)])
    s.add(conf_expr >= lo); s.add(conf_expr <= hi); s.add(conf_expr > LCB + epsilon)
    if s.check() != z3.sat: return None
    m = s.model()
    def z3_to_float(val):
        s = str(val)
        if '/' in s:
            num, den = s.split('/'); return float(num)/float(den)
        return float(s.replace('?', ''))
    p_star = np.array([z3_to_float(m.eval(p[i])) for i in range(num_classes)], dtype=np.float32)
    target_idx = next(i for i in range(num_classes) if m.eval(pred[i]) == z3.BoolVal(True))
    return p_star, target_idx, (lo, hi), LCB + epsilon

def train_torch_digits(seed=0):
    X, y = load_digits(return_X_y=True)
    X = (X / 16.0).astype(np.float32)
    Xtr, Xt, ytr, yt = train_test_split(X, y, test_size=0.2, stratify=y, random_state=seed)
    Xtr_t = torch.tensor(Xtr); ytr_t = torch.tensor(ytr, dtype=torch.long)
    Xt_t  = torch.tensor(Xt);  yt_t  = torch.tensor(yt, dtype=torch.long)
    class MLP(nn.Module):
        def __init__(self): super().__init__(); self.fc1=nn.Linear(64,64); self.fc2=nn.Linear(64,10)
        def forward(self,x): return self.fc2(torch.relu(self.fc1(x)))
    model = MLP(); opt = torch.optim.Adam(model.parameters(), lr=1e-3)
    for _ in range(15):
        model.train(); idx=torch.randperm(len(Xtr_t))
        for i in range(0,len(Xtr_t),128):
            b=idx[i:i+128]; logits=model(Xtr_t[b])
            loss=F.cross_entropy(logits,ytr_t[b]); opt.zero_grad(); loss.backward(); opt.step()
    model.eval()
    with torch.no_grad():
        logits = model(Xt_t); pred = logits.argmax(1); acc = (pred==yt_t).float().mean().item()
    return model, acc

def cegis_input(model, p_star, target_idx, lo, hi, lcb_plus_eps, steps=1200, lr=0.12, lam=1e-3):
    torch.manual_seed(0)
    p_star_t = torch.tensor(p_star)
    x = torch.rand(64, requires_grad=True)
    opt_x = torch.optim.Adam([x], lr=lr)
    def kl(p,q): return torch.sum(p*(torch.log(p+1e-9)-torch.log(q+1e-9)))
    hit=None; q=None; floor=max(lo,lcb_plus_eps)
    for t in range(steps):
        logits=model(x); q=torch.softmax(logits,dim=0)
        loss=kl(p_star_t,q)+lam*torch.sum(x*x)
        opt_x.zero_grad(); loss.backward(); opt_x.step()
        with torch.no_grad(): x.clamp_(0.0,1.0)
        if (q[target_idx]>=floor) and (q[target_idx]<=hi): hit=t; break
    with torch.no_grad(): logits=model(x); q=torch.softmax(logits,dim=0)
    return x.detach().numpy(), q.detach().numpy(), hit



# %%
 
import os, json, numpy as np, z3
from sklearn.datasets import load_digits
from sklearn.model_selection import train_test_split
from sklearn.neural_network import MLPClassifier
from sklearn.metrics import accuracy_score

runs = [
    {"tag":"temp_hack_strong", "mode":"temp_hack", "temp_factor":10.0, "bins":6, "min_support":30, "epsilon":0.02},
    {"tag":"ood_shift",        "mode":"ood",       "noise_sigma":0.9,  "bins":6, "min_support":20, "epsilon":0.02},
    {"tag":"imbalance",        "mode":"imbalance",                         "bins":6, "min_support":10, "epsilon":0.02},
    {"tag":"clean_strict",     "mode":"clean",                             "bins":6, "min_support":50, "epsilon":0.02},
]

# base data once
X_all, y_all = load_digits(return_X_y=True)
X_all = X_all / 16.0

for r in runs:
    tag = r["tag"]
    outdir = os.path.join(".", f"out_{tag}")
    os.makedirs(outdir, exist_ok=True)
    print(f"\n--- RUN: {tag} (mode={r['mode']}) ---")

    # train sklearn model for probs
    Xtr, Xt, ytr, yt = train_test_split(X_all, y_all, test_size=0.2, random_state=0, stratify=y_all)
    clf = MLPClassifier(hidden_layer_sizes=(64,), max_iter=120, random_state=0).fit(Xtr, ytr)
    probs_clean = clf.predict_proba(Xt)
    acc_clean = accuracy_score(yt, probs_clean.argmax(1))
    print(f"[sklearn] clean accuracy={acc_clean:.3f}")

    # --- choose mode
    if r["mode"] == "clean":
        probs, y_eval = probs_clean, yt

    elif r["mode"] == "temp_hack":
        f = r.get("temp_factor", 8.0)
        p = probs_clean ** f
        probs = p / p.sum(axis=1, keepdims=True)
        y_eval = yt

    elif r["mode"] == "ood":
        # FIX: build OOD from Xt (size 360), not Xtr (1437)
        rng = np.random.default_rng(0)
        X_ood = Xt[:, rng.permutation(Xt.shape[1])]
        X_ood = np.clip(X_ood + rng.normal(0, r.get("noise_sigma", 0.8), X_ood.shape), 0, 1)
        probs = clf.predict_proba(X_ood)
        y_eval = yt  # labels from the test split
        # sanity
        assert probs.shape[0] == len(y_eval), f"OOD size mismatch: probs={probs.shape[0]} vs labels={len(y_eval)}"

    elif r["mode"] == "imbalance":
        probs, y_eval, _ = make_imbalance(seed=0, n_samples=4000)

    else:
        raise ValueError("unknown mode")

    # --- eval vectors
    preds = probs.argmax(axis=1)
    conf  = probs.max(axis=1)
    acc   = (preds == y_eval).astype(int)
    print(f"[eval] mean conf={conf.mean():.3f}, accuracy={acc.mean():.3f}")

    # --- bins + artifacts
    meta = build_bins(conf, acc, num_bins=r["bins"], wilson_z=1.96)
    for b in meta: b["num_classes"] = probs.shape[1]

    with open(os.path.join(outdir, "calibration.json"), "w") as f:
        json.dump({"bins":meta, "mode":r["mode"], "epsilon":r["epsilon"], "min_support":r["min_support"]}, f, indent=2)

    plot_bins(meta, out_path=os.path.join(outdir, "calibration_plot.png"), title=f"Calibration bins ({tag})")

    # --- SMT decision (exists violating bin with support >= min_support)
    s = z3.Solver()
    conf_v=[b["conf"] for b in meta]; LCB_v=[b["LCB"] for b in meta]; sup_v=[b["support"] for b in meta]
    B=[z3.Bool(f"Bin_{i}") for i in range(len(meta))]
    for i in range(len(meta)):
        s.add(z3.Implies(B[i], conf_v[i] > LCB_v[i] + r["epsilon"]))
        s.add(z3.Implies(B[i], sup_v[i] >= r["min_support"]))
    s.add(z3.Or(B) if B else z3.BoolVal(False))
    print("SMT overconfident bin exists?", "YES" if s.check()==z3.sat else "NO")

    # --- Z3: violating probability target + CEGIS (only if K matches torch model)
    out = z3_prob_vector_for_violating_bin(meta, r["epsilon"], probs.shape[1])
    if out is None:
        print("  -> no violating probability vector (no non-empty gap).")
        continue

    p_star, target_idx, (lo,hi), lcb_eps = out
    K = probs.shape[1]
    print(f"  -> Z3 p* conf={p_star[target_idx]:.4f}, bin=({lo:.2f},{hi:.2f}), LCB+eps={lcb_eps:.4f}, K={K}")

    # CEGIS demo is implemented for the 10-class digits model (64→64→10).
    if K != 10:
        print(f"  -> [CEGIS] skipped (Torch demo model is 10-class; this run has K={K}). "
              f"Artifacts (calibration.json/plot) written.")
        print(f"Artifacts -> {os.path.abspath(outdir)}: calibration.json, calibration_plot.png")
        continue

    # ---- 10-class only: train torch digits model + CEGIS input synthesis
    model, tacc = train_torch_digits(seed=0)
    x_img, q, hit = cegis_input(model, p_star, target_idx, lo, hi, lcb_eps,
                                steps=1200, lr=0.12, lam=1e-3)
    print(f"  -> CEGIS hit? {'YES' if hit is not None else 'NO'} at step {hit}; q[target]={q[target_idx]:.4f}")

    import matplotlib.pyplot as plt
    plt.figure(figsize=(3,3)); plt.imshow(x_img.reshape(8,8), cmap="gray"); plt.axis("off")
    plt.title(f"{tag} q[target]={q[target_idx]:.3f}"); plt.tight_layout()
    plt.savefig(os.path.join(outdir, "cegis_input.png"), dpi=180); plt.close()

    print(f"Artifacts -> {os.path.abspath(outdir)}: calibration.json, calibration_plot.png, cegis_input.png")

```
