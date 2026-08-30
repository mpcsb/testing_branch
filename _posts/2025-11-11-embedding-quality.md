---
title:  "Using geometry to choose embeddings"
excerpt: "2025-11-11 — Empirical evaluation of local geometry in vector embeddings across models and corpora."
header:
  overlay_image: /assets/images/embedding_quality/header.png
tags:
  - embeddings
  - rag
  - machine-learning
  - z3
share: true
subscribe: true
comments: false
---
Code: [github.com/mpcsb/tb-embedding-quality](https://github.com/mpcsb/tb-embedding-quality)

## Why this matters


We often use **cosine distance** as if the resulting neighborhoods behaved like a clean metric space.  
Cosine distance does **not** satisfy triangle inequality: explicitly proven **[here](https://arxiv.org/abs/2107.04071)**.


Some metric indexes *do* rely on triangle inequality to prune search space, shown in  
**[Efficient Metric Indexing for Similarity Search](https://homes.cs.aau.dk/~csj/Papers/Files/2015_ChenICDE.pdf)**.

> Metric indexing relies on triangle inequality for pruning.

HNSW / FAISS don’t require strict metric axioms, and this post does not benchmark retrieval directly.  
That said, local neighborhood consistency matters: if a point is closer, greedy search and neighborhood expansion lead to other useful nearby points.

This is the thing I wanted to measure: not whether retrieval succeeds or fails, but whether the embedding space has stable local geometry.

### What can make the embedding geometry less stable

Two independent things:

1. **Bad corpus / domain mismatch**  
   If the embedding model wasn't trained on similar text, semantics may not be properly represented.

2. **Compression (PCA + quantization)**  
   Removes structure. Local neighborhoods can become less coherent. This is particularly relevant because compression solves a lot of operational problems.
   Compression comes in many flavours, and can be done with competence → this post illustrates a low effort compression to illustrate the point.

Both can lead to the same warning signs:

- local neighborhoods become less consistent  
- triangle inequality fails locally, and fails harder as distances increase.  
- retrieval may become more fragile, especially when the system expands or reranks large candidate sets

This post measures one approximation of that: how often local neighbor triplets violate triangle inequality.



## Setup  

We embed two different datasets:

| Corpus | What it contains | Notes |
|--------|------------------|----------------|
| **[food](https://www.kaggle.com/datasets/vinitshah0110/food-composition)** | short ingredient / composition snippets | noisy, repetitive text |
| **[medical](https://www.kaggle.com/datasets/matthewjansen/pubmed-200k-rtc)** | clinical trial abstracts | dense, clean text |

Three embedding variants:

| Name        | Model                     | Dim | Notes |
|-------------|---------------------------|-----|-------|
| `A_raw`     | DistilBERT STS-B          | 768 | strong baseline, 'high' dimension |
| `B_raw`     | MiniLM-L6-v2              | 384 | common model in local/demo RAG systems |
| `B_pca64q4` | MiniLM → PCA 64 → 4-bit   | 64  | aggressive compression |

Each corpus was chunked into 1000 samples.

---

## What we measure

For each point *i*:

1. find its top-k nearest neighbors (`j`)
2. check if any neighbor of a neighbor (`k`) breaks triangle inequality:  
d(i, k) > d(i, j) + d(j, k) + τ


If no violation exists, the point is **clean**.

The metric:  
>clean_frac = fraction of points with consistent neighborhoods


τ = tolerance.  
Higher `clean_frac`: stable space.  
Lower `clean_frac`: distances are not reliable.

(Note: I originally used **Z3** for this check because I was exploring constraint solvers around the same time as the previous Z3 post. Z3 is not needed here: the candidate triplets are finite, and a direct loop over `(i, j, k)` would answer the same question without any performance loss.)

The useful part is the question itself:

> “Does *any* neighbor-of-neighbor violate triangle inequality for this anchor, beyond tolerance τ?”


## Results
Three parts: 

### 1) UMAP: do embeddings even cluster coherently?

![umap_embeddings](/assets/images/embedding_quality/umap_embeddings.png)

Raw embedding models produce tighter clusters separated by corpus, whereas PCA+quantization blurs the two corpora together.

This already suggests some geometry degradation, although it is only a visual check.

---

### 2) Heatmap: metric stability across `k` neighbors and τ tolerance
(In the heatmap, the horizontal axis is the neighbor count k and the vertical axis is the tolerance τ. Color indicates the fraction of points that remain clean)

![heatmap](/assets/images/embedding_quality/heatmap.png)

Observations:

- medical corpus: **stable local geometry** (clean_frac ≈ 1.0)
- food corpus: noisy semantics, with lower local consistency
- PCA+quantized: large drop in clean_frac

Even at τ = 0.1 (a large tolerance), PCA+quantized still shows many violations.

---

### 3) Stability vs k: how fast the neighborhood falls apart

![stability_curves](/assets/images/embedding_quality/stability_curves.png)

- raw embeddings degrade slowly as k expands
- compressed embedding loses clean anchors quickly, especially by k=10

If retrieval expands `k` during recall-then-rerank, this kind of geometry is a warning sign: the larger neighborhood may contain less coherent candidates.

---

## Key takeaways  

1. **Embeddings are not guaranteed to form a metric space.**  
   Triangle inequality failures do not prove retrieval will fail, but they show that local neighborhoods are less metric-like than they may appear.

2. **Compression can damage neighborhood structure.**  
   PCA+quantization doesn’t only 'reduce redundancy'. This step needs extra monitoring, as local consistency can degrade **fast**.
   

3. **Corpus quality matters.**  
   The weaker, more repetitive corpus produced less stable local geometry.

> Geometry is not retrieval, but it is worth measuring before choosing or compressing embeddings.



---

Vector search does not always require a true metric, but it does depend on useful neighborhood structure.  
Most embedding models do not guarantee that structure under every corpus and compression setting.  

If the embedding space becomes less coherent because of a wrong model, wrong corpus, or aggressive compression, nearest-neighbor retrieval becomes a weaker signal. The triangle-violation check is one way to notice that before treating the index as a black box.

 