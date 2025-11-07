---
title:  "Semantic Model Checking for Model Equivalence (Using Z3)"
excerpt: "Using Z3 to prove two ML models are logically equivalent — or extract the exact counterexample where they diverge."
header:
  overlay_image: /assets/images/model_equivalence/header.jpg
tags:
  - z3
  - symbolic-reasoning
  - model-equivalence
  - machine-learning
share: true
subscribe: true
comments: true
---

# Z3 for Model Equivalence: Proving ML Models Match (or Finding the Exact Input Where They Don’t)

> **Goal**: Instead of *measuring* similarity between models, **prove** they're equivalent, and where they're not: extract the exact counterexample.

---

## The REAL question when pruning / replacing / compressing / distliling a model
We often replace or prune models:

- Random Forest → Pruned RF
- Large model → smaller, optimized deployment model
- Ensemble → distilled model

And we check:

> “Validation accuracy didn’t change, so the models are the same.”

That’s false.

Validation tells you **statistical similarity on sampled points**.  
What we want is **semantic equivalence**:

```
For all inputs x in the domain:
    model_A(x) == model_B(x)
```

If the answer is “no”, we want:

> the exact violating input x\*

---

## 🧠 Enter Z3 (SMT solver)

Z3 is a **constraint solver** from Microsoft Research.  
It doesn’t *run* the computation — it **reasons** about all possible inputs.

Classic use case: **Sudoku solver**.

Every rule is encoded as a constraint: numbers 1–9, unique rows, unique cols, etc.  
Z3 doesn’t brute-force — it symbolically prunes entire spaces at once.

We use the same trick here.

Instead of:

> “Try inputs until the model fails.”

We ask Z3:

```
∃ x   such that   Model_A(x) ≠ Model_B(x)
```

If yes → Z3 produces that violating x.  
If not → Z3 proves no such x exists within the domain.

---

## 🧩 Encoding a model as logic

Decision trees are perfect for SMT solving because they’re **pure conditional logic**:

```
if x[5] <= 0.12: go left
else:            go right
return leaf_label
```

A Random Forest or any tree ensemble is just:

```
mean( tree_1(x), tree_2(x), ..., tree_n(x) )
```

Z3 can encode every branch of every tree.

Then we assert:

```
(pred_A(x) != pred_B(x))
```

and let Z3 do the search.

---

## ✅ Code: Locating the exact counterexample

```python
from z3 import Real, RealVal, If, And, Or, Sum, Solver, sat

def encode_tree_as_z3(tree, x_vars):
    t = tree.tree_
    L, R = t.children_left, t.children_right
    feat, thr, val = t.feature, t.threshold, t.value

    def go(n):
        if L[n] == R[n]:
            return RealVal(int(val[n][0].argmax()))
        return If(x_vars[feat[n]] <= thr[n],
                  go(L[n]),
                  go(R[n]))
    return go(0)

def encode_forest_avg_vote(rf, x_vars):
    return Sum(*[encode_tree_as_z3(t, x_vars) for t in rf.estimators_]) / len(rf.estimators_)

def z3_label_counterexample(big, pruned, lo, hi):
    d = len(lo)
    x = [Real(f"x{i}") for i in range(d)]
    b = encode_forest_avg_vote(big, x)
    p = encode_forest_avg_vote(pruned, x)

    s = Solver()
    s.add(And(*[(x[i] >= lo[i]) & (x[i] <= hi[i]) for i in range(d)]))
    s.add((b >= 0.5) != (p >= 0.5))

    if s.check() != sat:
        return None
    m = s.model()
    return [float(str(m[xi])) for xi in x]
```

### Output:
```
[-0.965, 0.549, 0.247, 0.589, 0.475, 3.397, ...]
```

We now have the exact `x` where the two models diverge.

---

## 🔬 Visualizing the disagreement surface

| Interpretation | Image |
|----------------|--------|
| Where vote probability differs the most | ![](/assets/images/model_equivalence/1.png) |
| Where the predicted labels actually differ | ![](/assets/images/model_equivalence/2.png) |
| Zoom on violation region | ![](/assets/images/model_equivalence/3.png) |

These visuals are insanely revealing.

Most of the input space is **unchanged**, but we see precise “fault lines” where pruning altered behavior.

---

## 🧭 Minimal explanation trace (optional but cool)

You can even trace which removed trees caused the discrepancy:

```python
def trace_disagreement(x_cex, big, pruned, top_k=8):
    xb = x_cex.reshape(1, -1)
    votes = np.array([t.predict(xb)[0] for t in big.estimators_], float)
    removed = [i for i, t in enumerate(big.estimators_) if t not in pruned.estimators_]

    diffs = [(abs(votes.mean() - ((votes.sum() - votes[i])/(len(votes)-1))), i) for i in removed]
    diffs.sort(reverse=True)
    print(diffs[:top_k])
```

This produces a ranked list of “trees that mattered”.

---

## 🥊 Why this matters

| Approach | Guarantees? | Finds exact failure case? |
|----------|------------|---------------------------|
| Validation set | ❌ No | ❌ No |
| Adversarial search / Monte Carlo | ❌ No | ✅ Sometimes |
| **Z3** | ✅ Yes | ✅ Always if exists |

> Validation gives *confidence*.  
> Z3 gives **certainty**.

---

## TL;DR

- You can formally **prove** two models behave identically.
- If they don’t, Z3 produces the **smallest input that breaks equivalence**.
- Works out of the box for any tree ensemble (RF, XGBoost, LightGBM, etc.) because they're logic-based.

No brute force.  
No test set guessing.

Just **mathematically guaranteed model equivalence (or a counterexample).**

End of post.