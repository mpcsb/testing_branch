---
title: "After distillation: where should the next label go?"
excerpt: "2026-08-29 — Using a student model to audit LLM labels, find weak class boundaries, and spend the next labelling budget where it can still change the model."
permalink: /distillation-targeted-labels/
header:
  overlay_image: /assets/images/llm_distillation/header.jpg
  caption: "Photo: [Doug Lynne](https://commons.wikimedia.org/wiki/File:Twin_Sisters,_Jura_Knob.jpg), [CC BY-SA 2.0](https://creativecommons.org/licenses/by-sa/2.0/)"
tags:
  - machine-learning
  - llm
  - distillation
  - active-learning
share: true
subscribe: true
comments: false
---
Code: [github.com/mpcsb/tb-llm-distillation](https://github.com/mpcsb/tb-llm-distillation)

An LLM can label a text-classification dataset quickly. That does not make the labels ground truth.

The difficult examples are exactly where an LLM is most likely to be inconsistent: mixed evidence, vague language, neighbouring classes, and rules with awkward exceptions. Unfortunately, these are also the examples that define the decision boundary of the smaller model trained from those labels.

So I think the useful question comes **after** distillation:

> Once a student model has learned most of the task, where should the next unit of labelling budget go?

Not towards another random batch. Much of that batch will repeat what the model already knows.

Instead, I want to use the student to probe the teacher-labelled dataset, identify weak class boundaries, and retrieve new examples specifically from those regions.

---

## The student is also a dataset test

The usual distillation flow is one-way:

```text
LLM labels examples → student learns labels → student is deployed
```

But once the student exists, we can run it over the data that trained it. That creates a second flow in the opposite direction:

```text
student predictions → disagreements → inspect labels and weak regions
```

A disagreement can mean several things:

- the LLM label is wrong;
- the student is wrong;
- the example is genuinely ambiguous;
- the dataset contains too few examples of that kind;
- the class definition is unclear at that boundary.

All five are useful information.

This is particularly important with LLM supervision. LLMs are inconsistent, and the error rate tends to rise with the difficulty of the judgement. Repeating the same labelling request can produce a different answer, but asking the teacher again is not the only check available. A trained model gives us an independent, dataset-wide probe.

---

## A public binary experiment

For a reproducible example, I used 3,000 Amazon appliance reviews and asked an LLM to assign one of two labels:

- `defect`: a concrete failure in construction, operation, durability, or intended performance;
- `no_defect`: no product failure, including preference, compatibility, misuse, shipping, packaging, seller, or service issues.

This boundary is less trivial than it first appears. A one-star review can describe incompatibility rather than a defect. A mostly positive review can still mention a concrete failure. The LLM received the product and review text plus the labelling rules, but not the star rating.

I kept 400 rows as a holdout and used 2,600 for development. A `microsoft/deberta-v3-base` student, trained only on title and review text, reached 0.9025 accuracy and **0.8819 macro F1**.

That score is not the interesting part. The interesting part is what happened when I inferred over both the training and holdout sets.

The student disagreed with 65 of 2,600 training labels and 39 of 400 holdout labels. I reviewed those 104 rows using the original rules. Twenty-nine labels were clear enough to change: 19 in training and 10 in the holdout.

![A model-guided audit reduces the number of labels that need manual review](/assets/images/llm_distillation/guided_label_audit.png)

Reading **3.5% of the dataset** surfaced 29 corrections. More than a quarter of the reviewed disagreements were label errors.

The disagreements were not automatically correct. Some of the student's most confident predictions were obvious model mistakes:

| Shortened review | LLM label | Student | Audit |
|---|---|---|---|
| “Handle attachment is chipped and sharp out of the box” | `no_defect` | `defect` | label wrong |
| “It didn't seem to be filtering anything” | `no_defect` | `defect` | label wrong |
| “WAY too big to fit my regular stove” | `no_defect` | `defect` | model wrong |
| “Hinge came broken ... holes had no threads” | `defect` | `no_defect` | model wrong |

That is why this is an audit queue, not automatic relabelling.

It also explains why low-confidence sampling is not enough. Many useful disagreements were above 99% student confidence. Confidence tells us how strongly the student prefers one side of its learned boundary. It does not tell us that the LLM label on the other side is correct.

---

## Do not contaminate the evaluation

The holdout disagreements were useful for finding questionable labels, but changing them creates an evaluation problem.

After correcting 19 training labels and 10 holdout labels, the retrained student scored 0.9048 macro F1 on the corrected holdout. It is tempting to compare that with 0.8819 and claim a 2.3-point improvement.

That comparison is invalid. The ten holdout labels were chosen because the original model disagreed with them. In fact, the original model scores approximately **0.914 macro F1** after only changing those evaluation labels.

The correction pass improved the dataset, but this run alone does not show that changing 19 training rows improved generalization.

The practical rule is simple:

> Use model errors to audit evaluation labels, but measure the next training iteration on a separate frozen set that did not participate in row selection.

This is the difference between repairing a benchmark and improving a model.

---

## From disagreements to an acquisition strategy

Label correction is only the first use of inference over the training set. The more valuable use is deciding what to label next.

Suppose the task has three ordered classes: `A`, `B`, and `C`. If most errors are `A ↔ B` and `B ↔ C`, then the student already tells us two things:

1. which boundaries are weak;
2. which parts of the class interiors do not need more budget.

We can then search an unlabelled pool for examples near those boundaries. Useful retrieval signals can include:

- the two largest class probabilities and their margin;
- disagreement between different models;
- nearest neighbours with mixed labels;
- keywords or phrases associated with known failures;
- source, category, time, or other metadata;
- repeated-group behaviour, such as several examples from the same source disagreeing in the same direction.

These are **weak heuristics**, not replacement labels. Their job is to rank candidates for LLM or human annotation.

This makes even a crude keyword rule useful. A keyword may be a poor classifier over the entire dataset while still being an excellent retrieval mechanism for a rare, high-value slice.

---

## What this looked like in a three-class task

The binary appliance example demonstrates the mechanics publicly. The workflow itself came from a separate ordered three-class project whose domain and data I cannot publish. I will keep the classes anonymized and report only aggregate experiment results.

The model was run over a large unlabelled pool. For each row, I took the top two class probabilities and grouped examples by boundary. After excluding existing training rows, ranking by small probability margin, deduplicating, and limiting repeated sources, the candidate pools were:

| Boundary | Candidates found | Selected for review |
|---|---:|---:|
| `A ↔ B` | ~1,400 | 500 |
| `B ↔ C` | ~700 | 500 |
| `A ↔ C` | ~250 | 250 |

The imbalance is informative. It tells us that the adjacent boundaries contained far more unresolved data than the outer `A ↔ C` boundary.

The selected examples were labelled and added in successive rounds. Additional queues came from confident disagreements on existing training rows and from weak keyword/metadata heuristics over the unlabelled pool.

With the architecture fixed at DeBERTa-v3-base and evaluation kept on the same frozen holdout, macro F1 moved from approximately **0.862 to 0.870** across the iterative data rounds. The values shown here are rounded aggregates.

![Boundary-targeted candidate pools and macro F1 over iterative data rounds](/assets/images/llm_distillation/targeted_acquisition.png)

This is not a claim that every targeted batch beats every random batch. The rounds included different targeted sources, and a clean experiment would compare each batch with an equally sized random control.

It does show the operational pattern I care about: the same model continued to improve when the dataset was extended using its known weaknesses. A separate correction pass in this work changed only about 50 labels and moved macro F1 by roughly two percentage points in one run—small edits can move a boundary decisively when the rows sit in the right place.

---

## The complete loop

The process I would use is:

```text
1. Ask an LLM to label a broad, diverse seed set
2. Train a smaller student model
3. Infer over training and validation data
4. Review confident teacher/student disagreements
5. Count errors by direction and identify weak class boundaries
6. Use uncertainty, neighbours, keywords, and metadata to rank unlabelled rows
7. Label a small targeted batch
8. Retrain and evaluate on a frozen holdout
9. Compare the targeted batch with an equal random batch
10. Repeat only where the marginal gain justifies another label
```

There are three distinct datasets in this loop and they should not be confused:

- **training data**, which the model is allowed to shape and audit;
- **acquisition data**, from which the next candidates are selected;
- **frozen evaluation data**, which cannot be used to choose those candidates.

Without that separation it is very easy to report an apparent improvement that came from tuning the test itself.

---

## Final remarks

LLM-labelled data should be treated as a first version of a dataset, not as ground truth.

- **LLMs are inconsistent.** They make mistakes frequently enough to matter, especially when the question is difficult or the class definitions are close.
- **A trained model can audit its own supervision.** Inference over the training set exposes contradictions, confident disagreements, duplicates, and regions the teacher labelled inconsistently.
- **Evaluation labels also deserve inspection.** But once a holdout example is used to select a correction, it cannot provide an unbiased estimate of the resulting model.
- **Use every cheap signal available.** Probability margins, neighbours, keywords, metadata, source-level patterns, and model disagreement can all help retrieve useful unlabelled rows.
- **More data helps when it adds information.** Random sampling often buys examples from regions where the model is already correct. Boundary-targeted sampling has a better chance of changing what the model knows.
- **Measure marginal value.** Compare a targeted batch with an equally sized random batch, on a frozen holdout, before funding the next round.

The main output of distillation is therefore not only a smaller model.

It is a way to turn a one-off teacher call into an iterative dataset-improvement system: bootstrap with the LLM, probe with the student, and spend the next label where the model is still uncertain, inconsistent, or wrong.

**Do not spend the labelling budget teaching the model what it already knows.**