---
layout: single
permalink: /src-embedding-quality/
title: "src_embedding_quality"
--- 

Full_run.py
```

import os
import numpy as np
from pathlib import Path
from datetime import datetime
from itertools import product
import pandas as pd
from tqdm.auto import tqdm
from z3 import Solver, Bool, RealVal, Or, Implies, sat

# ---- local modules ----
from corpus_loader import load_corpora
from local_model_io import load_local_model      # loads SENTENCE TRANSFORMERS from local dir
from embed_utils import embed_texts              # with tqdm batching
from embed_utils import pca_project, quantize_uniform


# ==============================================================
# 1) LOAD CORPUS
# ==============================================================
FOOD = "data/Food Composition.csv"
MED  = "data/PubMed_200k_RCT"   
food_chunks, medical_chunks = load_corpora(FOOD, MED, n_food=1000, n_med=1000)


# ==============================================================
# 2) LOAD MODELS FROM LOCAL DISK (NO DOWNLOAD)
# ==============================================================
# these paths assume you ran mA.save() / mB.save() earlier
PATH_A = "./models_local/distilbert-base-nli-stsb-mean-tokens"
PATH_B = "./models_local/all-MiniLM-L6-v2"

mA = load_local_model(PATH_A)  # 768d
mB = load_local_model(PATH_B)  # 384d


# ==============================================================
# 3) EMBEDDINGS IN MEMORY (E[(corpus, model_variant)])
# ==============================================================

def degraded(X):
    Z64, _, _ = pca_project(X, out_dim=64)
    Z64 /= (np.linalg.norm(Z64, axis=1, keepdims=True) + 1e-12)
    Zq = quantize_uniform(Z64, bits=4, per_dim=True)
    Zq /= (np.linalg.norm(Zq, axis=1, keepdims=True) + 1e-12)
    return Zq.astype(np.float32)

E = {}

for corpus_name, chunks in [("food", food_chunks), ("medical", medical_chunks)]:
    print(f"\n🔹 embedding {corpus_name} (model A)")
    E[(corpus_name, "A_raw")] = embed_texts(mA, chunks, batch_size=256, normalize=True, progress=True)

    print(f"🔹 embedding {corpus_name} (model B)")
    E[(corpus_name, "B_raw")] = embed_texts(mB, chunks, batch_size=256, normalize=True, progress=True)

    print(f"🔹 PCA→64 + quant(4bit) {corpus_name} (model B_pca64q4)")
    E[(corpus_name, "B_pca64q4")] = degraded(E[(corpus_name, "B_raw")]) 


# ==============================================================
# 4) GEOMETRIC CONSISTENCY CHECK (Z3)
# ==============================================================

def cosine_distance_matrix_from_unit(X):
    S = X @ X.T
    np.clip(S, -1, 1, out=S)
    return (1.0 - S).astype(np.float32)

def knn_indices(D, k):
    idx = np.argsort(D, axis=1)
    return idx[:, 1:k+1].astype(np.int32)

def z3_violation(D, N, anchor, tau):
    i = int(anchor)
    s = Solver()
    bools = []
    for j in N[i]:
        j = int(j)
        for k in N[j]:
            if k == i or k == j: continue
            b = Bool(f"b_{i}_{j}_{k}")
            s.add(Implies(b, RealVal(float(D[i,j] + D[j,k])) < RealVal(float(D[i,k] - tau))))
            bools.append(b)
    if not bools:
        return False, None
    s.add(Or(*bools))
    out = s.check()
    if out == sat:
        m = s.model()
        for b in bools:
            if m.evaluate(b, model_completion=True):
                parts = b.decl().name().split("_")  # <-- CORRECT
                _, i, j, k = parts
                return True, (int(j), int(k))

    return False, None


def assess_local(X, k, tau, max_examples=5, desc=""):
    """Returns (summary_dict, examples)."""
    D = cosine_distance_matrix_from_unit(X)
    N = knn_indices(D, k)
    clean = 0
    examples = []
    for i in tqdm(range(X.shape[0]), desc=desc):
        sat, pair = z3_violation(D, N, i, tau)
        if not sat:
            clean += 1
        elif len(examples) < max_examples:
            j, k2 = pair
            examples.append((i, j, k2, float(D[i,j] + D[j,k2]), float(D[i,k2])))
    return clean, examples


# ==============================================================
# 5) SWEEP ALL MODELS & WRITE CSVs
# ==============================================================

from pathlib import Path
from datetime import datetime
from itertools import product
import pandas as pd

stamp = datetime.utcnow().strftime("%Y%m%d-%H%M%S")

configs = [
    ("food",   "A_raw"),
    ("food",   "B_raw"),
    ("food",   "B_pca64q4"),
    ("medical","A_raw"),
    ("medical","B_raw"),
    ("medical","B_pca64q4"),
]

ks   = [2, 5, 10, 15, 20]
taus = [0.0, 0.01, 0.05, 0.10]

rows_metrics = []
rows_examples = []

for (corp, model), k, tau in product(configs, ks, taus):
    X = E[(corp, model)]
    desc = f"{corp}/{model} k={k} tau={tau}"
    clean, exs = assess_local(X, k=k, tau=tau, max_examples=6, desc=desc)

    rows_metrics.append({
        "timestamp": stamp,
        "corpus": corp,
        "model": model,
        "k": k,
        "tau": tau,
        "n": X.shape[0],
        "clean": clean,
        "clean_frac": clean / X.shape[0],
    })

    for (i, j, k2, lhs, rhs) in exs:
        rows_examples.append({
            "timestamp": stamp,
            "corpus": corp,
            "model": model,
            "k": k,
            "tau": tau,
            "i": i,
            "j": j,
            "k2": k2,
            "lhs": lhs,
            "rhs": rhs,
            "margin": rhs - lhs,
        })

# ---- write to disk ----
Path("./outputs").mkdir(exist_ok=True)

metrics_csv  = f"./outputs/geometry_metrics_{stamp}.csv"
examples_csv = f"./outputs/geometry_examples_{stamp}.csv"

pd.DataFrame(rows_metrics).to_csv(metrics_csv, index=False)
pd.DataFrame(rows_examples).to_csv(examples_csv, index=False)

print("\n saved results:")
print(f"  metrics  --> {metrics_csv}")
print(f"  examples --> {examples_csv}")



##==============================================================
#6) VIZ
# ==============================================================

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# --- inputs ---
metrics = pd.read_csv("./outputs/geometry_metrics_0.csv")  # replace
metrics["model"] = metrics["model"].astype(str)
metrics["corpus_model"] = metrics["corpus"] + " · " + metrics["model"]

# --- order models by performance (mean clean_frac across k, tau) ---
order_by_perf = (
    metrics.groupby(["corpus", "model"])["clean_frac"]
    .mean()
    .reset_index()
    .sort_values(["corpus", "clean_frac"], ascending=[True, False])
)
order_map = {
    c: list(df.sort_values("clean_frac", ascending=False)["model"])
    for c, df in order_by_perf.groupby("corpus")
}

# a copper-ish palette for lines/bars
palette_models = sns.color_palette("copper", n_colors=3)


import pandas as pd, seaborn as sns, matplotlib.pyplot as plt
MODEL_ORDER = ["A_raw", "B_raw", "B_pca64q4"]
CORPUS_ORDER = ["food", "medical"]  # change if you want
metrics["model"]  = pd.Categorical(metrics["model"],  MODEL_ORDER,  ordered=True)
metrics["corpus"] = pd.Categorical(metrics["corpus"], CORPUS_ORDER, ordered=True)
COPPER3 = sns.color_palette("copper", 3)



def plot_stability_curves(df):
    df2 = (df.groupby(["corpus","model","k"], as_index=False)["clean_frac"].mean()
             .sort_values(["corpus","model","k"]))
    g = sns.FacetGrid(df2, col="corpus", sharey=True, height=4, aspect=1.2, col_order=CORPUS_ORDER)
    for (corp, ax) in zip(CORPUS_ORDER, g.axes.flat):
        sub = df2[df2["corpus"]==corp]
        for m, color in zip(MODEL_ORDER, COPPER3):
            s = sub[sub["model"]==m]
            ax.plot(s["k"], s["clean_frac"], marker="o", label=m, color=color)
        ax.set_ylim(0,1.02); ax.grid(alpha=.25, lw=.6); ax.set_title(corp); ax.set_xlabel("k"); ax.set_ylabel("fraction of clean anchors")
        ax.legend(title="model", loc="lower left")
    g.fig.suptitle("Stability vs k (mean over τ)", y=1.02, fontsize=13)
    
    plt.savefig("images/stability_curves.png", dpi=200, bbox_inches="tight");plt.show()


plot_stability_curves(metrics)



def plot_heatmaps_by_tau(df):
    row_labels = [f"{c} · {m}" for c in CORPUS_ORDER for m in MODEL_ORDER]
    taus = sorted(df["tau"].unique())
    ncols = len(taus)
    fig, axes = plt.subplots(1, ncols, figsize=(4.2*ncols+1.5, 0.75*len(row_labels)+1), constrained_layout=True)
    if ncols==1: axes=[axes]
    for ax, tau in zip(axes, taus):
        sub = df[df["tau"]==tau].copy()
        sub["row"] = sub["corpus"].astype(str) + " · " + sub["model"].astype(str)
        piv = (sub.pivot_table(index="row", columns="k", values="clean_frac", aggfunc="mean")
                  .reindex(row_labels))
        sns.heatmap(piv, ax=ax, cmap="copper", vmin=0, vmax=1, annot=True, fmt=".2f",
                    cbar=(ax is axes[-1]), cbar_kws={"label":"clean_frac"})
        ax.set_title(f"τ = {tau:g}"); ax.set_xlabel("k"); ax.set_ylabel("" if ax is not axes[0] else "corpus · model")
    fig.suptitle("Embedding Retrieval Stability", y=1.02, fontsize=13)
    
    plt.savefig("images/heatmap.png", dpi=200, bbox_inches="tight");plt.show()


plot_heatmaps_by_tau(metrics)



import seaborn as sns, matplotlib.pyplot as plt
from matplotlib.lines import Line2D

ex = examples.copy()  # columns: model, corpus, lhs, rhs
ex["model"] = pd.Categorical(ex["model"], ["A_raw","B_raw","B_pca64q4"], ordered=True)

g = sns.FacetGrid(
    ex.sample(min(4000, len(ex))), col="model", col_order=["A_raw","B_raw","B_pca64q4"],
    hue="corpus", hue_order=["food","medical"], height=4, aspect=1
)
g.map_dataframe(sns.scatterplot, x="lhs", y="rhs", s=18, alpha=0.6)
for ax in g.axes.flat:
    lim = max(ax.get_xlim()[1], ax.get_ylim()[1])
    ax.plot([0,lim],[0,lim],"k--",lw=1)
    ax.set_xlim(0, lim); ax.set_ylim(0, lim)
    ax.set_xlabel("d(i,j)+d(j,k)"); ax.set_ylabel("d(i,k)")
g.add_legend(title="corpus")
g.fig.suptitle("Triangle Violations by Model", y=1.02)

plt.savefig("images/Triangle_Violations.png", dpi=200, bbox_inches="tight")
plt.show()



import numpy as np, pandas as pd, seaborn as sns, matplotlib.pyplot as plt
from sklearn.random_projection import SparseRandomProjection
from umap import UMAP

MODEL_ORDER  = ["A_raw","B_raw","B_pca64q4"]
CORPUS_ORDER = ["food","medical"]
PALETTE      = sns.color_palette("copper", len(MODEL_ORDER))

def pad_to_dim(X, target=768):
    D = X.shape[1]
    if D == target:
        return X
    Z = np.zeros((X.shape[0], target), dtype=X.dtype)
    Z[:, :D] = X
    return Z

# ---- build matrix with shared basis ----
rows = []
mats = []
for corpus in CORPUS_ORDER:
    for model in MODEL_ORDER:
        X = E[(corpus, model)]
        idx = np.random.choice(len(X), size=min(500, len(X)), replace=False)
        Xs = X[idx]
        Xs = Xs / (np.linalg.norm(Xs, axis=1, keepdims=True) + 1e-12)   # normalize
        Xs = pad_to_dim(Xs, target=768)                                 # common dim
        mats.append(Xs)
        rows += [(corpus, model)] * len(Xs)

M = np.vstack(mats)

# one random projection for ALL (shared basis), then UMAP
rp = SparseRandomProjection(n_components=64, density='auto', random_state=42)
M64 = rp.fit_transform(M)

um = UMAP(n_neighbors=20, min_dist=0.1, metric="euclidean", random_state=42)
U = um.fit_transform(M64)

dfu = pd.DataFrame({
    "x": U[:,0], "y": U[:,1],
    "corpus": [r[0] for r in rows],
    "model":  [r[1] for r in rows],
})
dfu["model"]  = pd.Categorical(dfu["model"],  MODEL_ORDER,  ordered=True)
dfu["corpus"] = pd.Categorical(dfu["corpus"], CORPUS_ORDER, ordered=True)

import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
from scipy.spatial import ConvexHull

def plot_umap_with_labels(df, palette="copper"):
    plt.figure(figsize=(10,7))
    colors = sns.color_palette(palette, df["model"].nunique())

    # scatter
    sns.scatterplot(
        data=df, x="x", y="y",
        hue="model", style="corpus",
        palette=colors, s=20, alpha=0.7, linewidth=0,
        hue_order=["A_raw","B_raw","B_pca64q4"],
        style_order=["food","medical"],
    )

    # draw convex hulls per (model, corpus)
    for (model, corpus), sub in df.groupby(["model","corpus"]):
        if len(sub) < 5: continue
        pts = sub[["x","y"]].to_numpy()
        hull = ConvexHull(pts)
        plt.fill(
            pts[hull.vertices,0], pts[hull.vertices,1],
            alpha=0.08, color=colors[["A_raw","B_raw","B_pca64q4"].index(model)],
            label=None
        )
        # centroid + label
        cx, cy = pts.mean(axis=0)
        plt.text(cx, cy, f"{model}\n{corpus}", fontsize=9, weight="bold",
                 ha="center", va="center", color="black",
                 bbox=dict(boxstyle="round,pad=0.25", fc="white", alpha=0.6, lw=0))

    plt.title("UMAP of embeddings with corpus–model clusters")
    plt.xlabel("UMAP-1"); plt.ylabel("UMAP-2")
    plt.grid(alpha=0.25, lw=0.5)
    plt.legend(title=None, loc="best", frameon=False)
    plt.tight_layout()
    plt.savefig("images/umap_embeddings.png", dpi=200, bbox_inches="tight")
    plt.show()

# run
plot_umap_with_labels(dfu)

```

embed_utils.py
```
# emb_utils.py
import numpy as np
import torch
from sentence_transformers import SentenceTransformer

def load_st_model(name: str):
    device = "cuda" if torch.cuda.is_available() else "cpu"
    model = SentenceTransformer(name, device=device)
    return model

from tqdm.auto import tqdm
import math
import numpy as np
import torch
from sentence_transformers import SentenceTransformer

@torch.no_grad()
def embed_texts(
    model: SentenceTransformer,
    texts,
    batch_size: int = 128,
    normalize: bool = False,
    progress: bool = True,
    desc: str = "Embedding",
):
    texts = list(texts)
    n = len(texts)
    out = []
    for i in tqdm(range(0, n, batch_size),
                  total=math.ceil(n / batch_size),
                  disable=not progress,
                  desc=desc):
        batch = texts[i:i+batch_size]
        vecs = model.encode(
            batch,
            batch_size=batch_size,           # internal batching still helps on tokenization
            convert_to_numpy=True,
            normalize_embeddings=False,      # we handle below
            show_progress_bar=False,         # we control tqdm
        )
        out.append(vecs)

    X = np.vstack(out).astype(np.float32)
    if normalize:
        X /= (np.linalg.norm(X, axis=1, keepdims=True) + 1e-12)
    return X  # [N, D]


def pca_project(X: np.ndarray, out_dim: int):
    Xc = X - X.mean(axis=0, keepdims=True)
    # economy SVD
    U, S, Vt = np.linalg.svd(Xc, full_matrices=False)
    W = Vt[:out_dim].T  # [D, out_dim]
    Z = Xc @ W          # [N, out_dim]
    return Z, W, X.mean(axis=0, keepdims=True)

def quantize_uniform(X: np.ndarray, bits=4, per_dim=True):
    q = 2**bits - 1
    if per_dim:
        mn = X.min(axis=0, keepdims=True)
        mx = X.max(axis=0, keepdims=True)
    else:
        mn = np.array([[X.min()]])
        mx = np.array([[X.max()]])
    span = (mx - mn) + 1e-12
    Y = (X - mn) / span
    Yq = np.round(Y * q) / q
    Xq = Yq * span + mn
    return Xq


```


local_model_io.py
```
# local_model_io.py
from sentence_transformers import SentenceTransformer
import torch
from pathlib import Path
import os

def load_local_model(model_dir: str, device: str = None):
    """
    Load a SentenceTransformer from a local directory.
    No network calls.
    """
    # Guarantee offline behavior
    os.environ["HF_HUB_OFFLINE"] = "1"
    os.environ.setdefault("TRANSFORMERS_OFFLINE", "1")
    p = Path(model_dir)
    if not p.exists():
        raise FileNotFoundError(f"Model dir not found: {p}")
    return SentenceTransformer(str(p), device=device or ("cuda" if torch.cuda.is_available() else "cpu"))


```


corpus_loader.py
```
# corpus_loader.py
from __future__ import annotations
import re
import csv
from pathlib import Path
from typing import List, Tuple
import pandas as pd

# ---------------------------
# Generic text chunking utils
# ---------------------------
def _chunk_text(text: str, max_tokens=200, stride=80, min_chars=100) -> List[str]:
    toks = text.split()
    if not toks:
        return []
    out, i = [], 0
    while i < len(toks):
        w = " ".join(toks[i:i+max_tokens]).strip()
        if len(w) >= min_chars:
            out.append(w)
        if i + max_tokens >= len(toks):
            break
        i += max(1, max_tokens - stride)
    return out

def _dedupe_keep_order(items: List[str]) -> List[str]:
    seen, out = set(), []
    for x in items:
        k = x.strip()
        if k and k not in seen:
            seen.add(k); out.append(k)
    return out

# ---------------------------
# Food corpus (single CSV)
# ---------------------------
def _read_csv_loose(path: Path) -> pd.DataFrame:
    """
    Robust CSV read: try default, then fallbacks with sep inference.
    """
    try:
        return pd.read_csv(path, low_memory=False)
    except Exception:
        # try python engine with sniffed delimiter
        with path.open("r", encoding="utf-8", newline="") as f:
            sample = "".join(f.readlines(5000))
            dialect = csv.Sniffer().sniff(sample, delimiters=",;\t|")
        return pd.read_csv(path, low_memory=False, engine="python", sep=dialect.delimiter)

def load_food_chunks(
    csv_path: str | Path,
    target_chunks: int = 1000,
    max_tokens: int = 180,
    stride: int = 60,
    min_chars: int = 80,
) -> List[str]:
    """
    Build ~target_chunks from the Food Composition CSV by templating text fields.
    """
    path = Path(csv_path)
    df = _read_csv_loose(path)

    cols = {
        "name": "Food Name",
        "desc": "Food Description",
        "der":  "Derivation",
        "class":"Classification Name",
        "samp": "Sampling Details",
    }
    present = {k: c for k, c in cols.items() if c in df.columns}
    if not present:
        # fallback: any object columns
        obj_cols = [c for c in df.columns if df[c].dtype == "object"]
        if not obj_cols:
            return []
        present = {f"c{i}": c for i, c in enumerate(obj_cols)}

    chunks: List[str] = []
    for _, r in df.iterrows():
        parts = []
        # structured template if the expected columns exist
        if "name" in present and isinstance(r.get(present["name"]), str):
            parts.append(f"Recipe ingredient: {r[present['name']]}.")
        if "desc" in present and isinstance(r.get(present["desc"]), str):
            parts.append(f"Description: {r[present['desc']]}.")
        if "der" in present and isinstance(r.get(present["der"]), str):
            parts.append(f"Derivation: {r[present['der']]}.")
        if "class" in present and isinstance(r.get(present["class"]), str):
            parts.append(f"Category: {r[present['class']]}.")
        if "samp" in present and isinstance(r.get(present["samp"]), str):
            parts.append(f"Sampling details: {r[present['samp']]}.")

        # if template produced nothing, coalesce any string columns
        if not parts:
            vals = [str(r[c]).strip() for c in present.values()
                    if isinstance(r.get(c), str) and r.get(c).strip()]
            para = " | ".join(vals)
        else:
            para = " ".join(p.strip() for p in parts if p and p.strip())

        if not para:
            continue

        chunks.extend(_chunk_text(para, max_tokens=max_tokens, stride=stride, min_chars=min_chars))
        if len(chunks) >= target_chunks:
            break

    return _dedupe_keep_order(chunks[:target_chunks])

# ---------------------------
# PubMed RCT (dir with .txt OR CSV fallback)
# ---------------------------
def _parse_rct_txt(path: Path) -> List[str]:
    """
    Parse one RCT .txt file:
      '###<id>' lines separate abstracts
      other lines: 'LABEL<TAB>SENTENCE'
    Returns: list of abstracts (each a single concatenated string).
    """
    abstracts, cur = [], []
    with path.open("r", encoding="utf-8") as f:
        for line in f:
            line = line.rstrip("\n")
            if not line:
                continue
            if line.startswith("###"):
                if cur:
                    abstracts.append(" ".join(cur))
                    cur = []
                continue
            parts = line.split("\t")
            sent = parts[-1].strip() if parts else ""
            if sent:
                cur.append(sent)
    if cur:
        abstracts.append(" ".join(cur))
    return abstracts

def _collect_rct_abstracts(dir_path: Path) -> List[str]:
    files = [dir_path / "train.txt", dir_path / "dev.txt", dir_path / "test.txt"]
    files = [p for p in files if p.exists()]
    if not files:
        files = list(dir_path.glob("*.txt"))
    abstracts: List[str] = []
    for p in files:
        abstracts.extend(_parse_rct_txt(p))
    return abstracts

def load_pubmed_chunks(
    dir_or_csv: str | Path,
    target_chunks: int = 1000,
    use_txt_first: bool = True,
    max_tokens: int = 220,
    stride: int = 90,
    min_chars: int = 120,
) -> List[str]:
    """
    Build ~target_chunks from PubMed RCT data:
      - If a directory: parse RCT .txt files (preferred: richer text).
      - Else: treat as CSV with columns [abstract_id, line_number, abstract_text],
              rebuild abstracts by grouping + concatenation.
    """
    p = Path(dir_or_csv)

    chunks: List[str] = []
    if use_txt_first and p.is_dir():
        abstracts = _collect_rct_abstracts(p)
        for abs_txt in abstracts:
            abs_txt = re.sub(r"\s+", " ", abs_txt).strip()
            chunks.extend(_chunk_text(abs_txt, max_tokens=max_tokens, stride=stride, min_chars=min_chars))
            if len(chunks) >= target_chunks:
                break
        return _dedupe_keep_order(chunks[:target_chunks])

    # CSV fallback (robust read)
    df = _read_csv_loose(p)
    required = {"abstract_id", "line_number", "abstract_text"}
    if not required.issubset(set(df.columns)):
        raise ValueError(f"CSV missing required columns {required}")

    grouped = (
        df.sort_values(["abstract_id", "line_number"])
          .groupby("abstract_id")["abstract_text"]
          .apply(lambda s: " ".join(s.astype(str)))
    )
    for abs_txt in grouped:
        abs_txt = re.sub(r"\s+", " ", abs_txt).strip()
        chunks.extend(_chunk_text(abs_txt, max_tokens=max_tokens, stride=stride, min_chars=min_chars))
        if len(chunks) >= target_chunks:
            break
    return _dedupe_keep_order(chunks[:target_chunks])

# ---------------------------
# Public API
# ---------------------------
def load_corpora(
    food_csv: str | Path,
    pubmed_path: str | Path,  # dir with RCT .txt OR CSV file
    n_food: int = 1000,
    n_med: int = 1000,
) -> Tuple[List[str], List[str]]:
    food = load_food_chunks(food_csv, target_chunks=n_food)
    med  = load_pubmed_chunks(pubmed_path, target_chunks=n_med)
    return food, med


```
