---
title:  "Semantic Model Checking for Model Equivalence (Using Z3)"
excerpt: "2025-11-07 — Using Z3 to prove two ML models are logically equivalent — or extract the exact counterexample where they diverge."
header:
  overlay_image: /assets/images/model_equivalence/header.jpg
tags:
  - z3
  - optimization
  - model-equivalence
  - machine-learning
  - uncertainty
share: true
subscribe: true
comments: false
---

Most model compression techniques stop after validation accuracy.
If loss and accuracy remain roughly the same, the task is completed.

But there’s something flawed in that logic:  
validation accuracy doesn’t tell us *where the models disagree*, it tells us only where they didn’t disagree on the points we checked.


## Z3 for Model Equivalence: Proving ML Models Match (or Finding the exact input where they don’t)

**Goal**: Instead of *measuring* similarity between models, **prove** they're equivalent, and where they're not: extract the exact counterexample.


## The question when pruning / replacing / compressing / distlilling a model

We prune or replace models for practical reasons (essentially operational constraints).  
Things like: latency, memory, cost, deployment simplicity, simplification for interpretability...

And this will for instance creating a pipeline like so: Random Forest → Pruned RF. It's our use case in this post.

We check if the validation accuracy didn’t change, and hope it means the models are the same.

That's false.  
And dependending on the agressiveness of the pruning and amount of data at our disposal, something critical to know.

Validation tells us **similarity on sampled points**, on information that we already have.  
What we want is **equivalence**:

```
For all inputs x in the domain:
    model_A(x) == model_B(x)
```

If the answer is no, we want the exact violating input *X*

---

## Enter Z3 (SMT solver)

Z3 is a **constraint solver** from Microsoft Research.  
Optimizers try values and adjust based on results.  
Z3 doesn’t search, it doesn’t *run* the computation, it **reasons** about all possible inputs.  
We state the rules, and it determines whether any input satisfies them.  
> For model equivalence, we ask: is there any x where the two models disagree? If yes, Z3 returns that x; if not, it proves none exists.

The classic use case (or at least how I first heard of z3): **[Sudoku solver](https://ericpony.github.io/z3py-tutorial/guide-examples.htm#sudoku)**.

Every rule is encoded as a constraint: numbers 1–9, unique rows, unique cols, etc.  
Z3 doesn’t brute-force — it symbolically prunes entire spaces at once.

We use the same trick here.

Instead of trying inputs until the model fails, we ask Z3:

```
∃ x   such that   Model_A(x) ≠ Model_B(x)
```

If yes → Z3 produces that violating x.  
If not → Z3 proves no such x exists within the domain.

---

## Encoding a model as logic

Decision trees are perfect for SMT solving because they’re **pure conditional logic**:

```
if x[5] <= 0.12:  
   left
else:             
   right
return leaf_label
```

Z3 can encode every branch of every tree.

Then we assert:

```
(pred_A(x) != pred_B(x))
```

and let Z3 do the search.

---

## Code: Locating the exact counterexample

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

```
>>> [-0.965, 0.549, 0.247, 0.589, 0.475, 3.397, ...]
```

We now have the exact `x` where the two models diverge.

---

## Visualizing the disagreement surface

| Interpretation | Image |
|----------------|--------|
| Where vote probability differs the most | ![](/assets/images/model_equivalence/1.png) |
| Where the predicted labels actually differ | ![](/assets/images/model_equivalence/2.png) |
| Zoom on violation region with arbitrary differnce | ![](/assets/images/model_equivalence/3.png) |

These visuals are easy to track, and with some work, creating something for the most problematic combinations of features, would be very revealing for the pruning process.

Most of the input space is essentially the same, but we see precise "fault lines" where pruning changes the target predictions.

---

##  Minimal explanation trace 

We can even trace which removed trees caused the discrepancy:

```python
def trace_disagreement(x_cex, big, pruned, top_k=8):
    xb = x_cex.reshape(1, -1)
    votes = np.array([t.predict(xb)[0] for t in big.estimators_], float)
    removed = [i for i, t in enumerate(big.estimators_) if t not in pruned.estimators_]

    diffs = [(abs(votes.mean() - ((votes.sum() - votes[i])/(len(votes)-1))), i) for i in removed]
    diffs.sort(reverse=True)
    print(diffs[:top_k])
```

This produces a ranked list of the trees that mattered with respect to the divergence of the two models.

---

## Why this matters

| Approach | Guarantees? | Finds exact failure case? |
|----------|------------|---------------------------|
| Validation set |  No |  No |
| **Z3** |  Yes |  Always if exists |

Validation gives confidence, Z3 gives **certainty**.


## Why this does *not* work well for neural networks
I experimented with neural nets a bit and things get complex really fast; when compared with conditional logic, which are *relatively* small models, even moderate networks use many thousands of numeric operations that interact in complex, continuous ways. For Z3 to reason about them, every multiplication and activation has to become a constraint.

Expanding this to an LLM, and how we could assess whether a distlied model be roughly equivalent, would be practically impossible.


---

## Closing Remarks

- We can formally prove two models behave identically.
- If they don’t, we can have Z3 produce the smallest input that breaks equivalence.
- Works out of the box for any tree ensemble (RF, XGBoost, LightGBM, etc.) because they're logic-based.

No brute force,no test dataset guesses.

Just **mathematically guaranteed model equivalence (or a counterexample).**


## Further reading — neural network equivalence via SMT

The idea of proving that two models are equivalent (or extracting counterexamples when they aren’t) originates from formal verification research — in particular:

Eleftheriadis et al., On Neural Network Equivalence Checking Using SMT Solvers.
FORMATS 2022.
https://www.ccs.neu.edu/~stavros/papers/2022-formats-NN_Equivalence.pdf

Their work focuses on neural networks and supports strict + approximate equivalence relations.

This post adapts a similar encoding idea to decision-tree ensembles (random forests), making equivalence checking usable in practical DS/ML pipelines.