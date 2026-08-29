---
title: "LLM distillation: optimizing for the labels that matter"
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

An LLM can label a text-classification dataset without building a task-specific model first. But a large API pass still takes time, and every new prediction carries the teacher's latency and cost. The labels are not ground truth either.

The difficult examples are often where an LLM is least consistent: mixed evidence, vague language, neighbouring classes, and rules with exceptions. Those examples also define the decision boundary of the smaller model trained from the labels.

That shifts the question **after** distillation:

> Once a student model has learned most of the task, where should the next unit of labelling budget go?

Not towards another random batch. Much of that batch will repeat what the model already knows. 

A better use of the budget is to probe the teacher-labelled dataset with the student, identify weak class boundaries, particular examples of low performance attributes, and retrieve new examples from those regions.

Distillation changes the economics of running inference. Once trained, the student can predict on large datasets locally (in particular on CPU) without a paid LLM call for every row. CPU inference is not fast in absolute terms, but an offline batch can cost much less than repeatedly sending the same task to a large hosted model and such instances are readily available. The teacher is used just for teaching and rarely, when judgement is needed. The student handles dense, routine passes over training, validation and acquisition data, and specializes.

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
- the example is genuinely hard;
- the dataset contains too few examples of that kind;
- the class definition is unclear at that boundary.

Any of these is worth knowing.

LLM supervision makes this especially relevant. The same labelling request can produce different answers, and difficult judgements tend to be the least stable. Asking the teacher again is one check. A trained model gives us another, independent check over the entire dataset.

---

## A binary classification experiment

I set up a fast and reproducible example to illustrate the mechanics of this: 3000 Amazon appliance reviews and an LLM to assign one of two labels:

- `defect`: a concrete failure in construction, operation, durability, or intended performance;
- `no_defect`: all else.

The distinction is semantic. A one-star review can describe incompatibility rather than a defect. A mostly positive review can still mention a concrete failure. The LLM received the product and review text plus the labelling rules, but not the star rating.

I kept 400 rows as a holdout and used 2,600 for development. A `microsoft/deberta-v3-base` student, trained only on title and review text, reached 0.9 accuracy and **0.89 macro F1** on this first iteration -> from experience, it could have been optimized, but for the hours spent, it helped form some discussion points.  

### The budget has two phases

Before using the student to choose new data, I need to know when it became informative at all. I trained the same architecture on increasing amounts of teacher-labelled data, always evaluating on the same 400-row holdout.

| Teacher-labelled rows available | Holdout macro F1 | Behaviour |
|---:|---:|---|
| 100 | 0.416 | predicted only the majority class |
| 250 | 0.416 | predicted only the majority class |
| 500 | 0.810 | first useful student |
| 1,000 | 0.841 | boundary begins to refine |
| 2,600 | 0.882 | full public run |

Each run reserved 20% of the available rows for validation, so the model fitted 80, 200, 400, 800 and 2,080 rows respectively.

The jump between 250 and 500 labels is more important than a generic claim that more data helps. Below that threshold there is no useful student to guide the next purchase: the teacher budget is still buying basic task coverage. At 500 labels, the student becomes good enough to expose disagreements and weak regions. From that point onward, more labels continue to help, but each teacher call has an alternative: another random example, or an example chosen because the current model is weak there.

This turns the curve into a budget policy. **Sample broadly until the student is informative; then spend increasingly around its errors.** If the price and latency of a teacher label are known, every point on the table can be expressed in money and elapsed time as well as F1.

These are single training runs, not a smooth estimate of marginal returns. The exact increment between two points contains training and sampling noise. The robust feature is the change of regime: first set up a usable student, then use it to guide the remaining budget.

I then inferred over both the training and holdout sets, turning the model back on the labels that produced it.

The student disagreed with 65 of 2,600 training labels and 39 of 400 holdout labels. Those 104 rows were reviewed using the original prompt. Twenty-nine labels were clear enough to change: 19 in training and 10 in the holdout set.

![A model-guided audit reduces the number of labels that need manual review](/assets/images/llm_distillation/guided_label_audit.png)

Reading **3.5% of the dataset** got us 29 corrections! More than a quarter of the reviewed disagreements were label errors.

The disagreements were not automatically correct. Some of the student's most confident predictions were obvious model mistakes:

| Shortened review | LLM label | Student | Truth |
|---|---|---|---|
| “Handle attachment is chipped and sharp out of the box” | `no_defect` | `defect` | label wrong |
| “It didn't seem to be filtering anything” | `no_defect` | `defect` | label wrong |
| “WAY too big to fit my regular stove” | `no_defect` | `defect` | model wrong |
| “Hinge came broken ... holes had no threads” | `defect` | `no_defect` | model wrong |

The queue still needs review; it is not an automatic relabelling system.

Low-confidence sampling alone would miss much of this. Many informative disagreements were above 99% student confidence. Confidence tells us how strongly the student prefers one side of its learned boundary. It says nothing about whether the LLM label on the other side is correct.

---
 
---

## From disagreements to an acquisition strategy

Label correction is only the first use of inference over the training set. The more valuable use is deciding what to label next.

In another (richer) problem where the task had three ordered classes: `A`, `B`, and `C`, there were a lot more useful patterns and borders to mine. If most errors are `A ↔ B` and `B ↔ C`, then the student already tells us two things:

1. which boundaries are weak;
2. which parts of the class interiors do not need more budget.

We can then search an unlabelled pool for examples near those boundaries. Candidate-ranking signals include:

- the two largest class probabilities and their margin;
- disagreement between different models;
- nearest neighbours with mixed labels;
- keywords or phrases associated with known failures;
- source, category, time, or other metadata;
- repeated-group behaviour, such as several examples from the same source disagreeing in the same direction.

These are **weak heuristics**, not replacement labels. Their job is to rank candidates for LLM or human annotation.

Even a crude keyword rule can help here. It may be a poor classifier over the whole dataset but a good retrieval mechanism for a rare, high-value slice.

The value of an example is conditional on the current model. After one boundary improves, another may become the bottleneck; examples that looked valuable before retraining may now be redundant. This favours small acquisition rounds with a cheap student rescan between them, rather than one large purchase based on the first model's errors.

---

## What this looked like in a three-class task

The binary appliance example demonstrates the mechanics publicly. The workflow came from a separate ordered three-class project whose domain and data I cannot publish. The classes below are anonymized and the results are aggregate.

The task was difficult. No keyword or simple rule separated neighbouring classes, and many border cases were hard for human reviewers to resolve consistently. A disagreement near the boundary did not necessarily indicate careless LLM labelling. It often marked a real semantic ambiguity where the dataset needed better coverage and a more consistent decision rule.

The model was run over a large unlabelled pool. For each row, I took the top two class probabilities and grouped examples by boundary. After excluding existing training rows, ranking by small probability margin, deduplicating, and limiting repeated sources, the candidate pools were:

| Boundary | Candidates found | Selected for review |
|---|---:|---:|
| `A ↔ B` | ~1,400 | 500 |
| `B ↔ C` | ~700 | 500 |
| `A ↔ C` | ~250 | 250 |

The counts themselves mattered: the adjacent boundaries contained far more unresolved data than the outer `A ↔ C` boundary.

The selected examples were labelled and added in successive rounds. Additional queues came from confident disagreements on existing training rows and from weak keyword/metadata heuristics over the unlabelled pool.

With the architecture fixed at DeBERTa-v3-base and evaluation kept on the same frozen holdout, macro F1 moved from approximately **0.862 to 0.870** across the iterative data rounds. The values shown here are rounded aggregates.

![Boundary-targeted candidate pools and macro F1 over iterative data rounds](/assets/images/llm_distillation/targeted_acquisition.png)

The rounds included different targeted sources, so they do not prove that every targeted batch beats every random batch. A cleaner experiment would compare each batch with an equally sized random control.

The same model nevertheless improved as the dataset was extended around known weaknesses. In a separate correction iteration, changing only about 50 labels moved macro F1 by roughly two percentage points. Small edits can move a boundary decisively when the rows sit in the right place! This is critical.  

Data is not the only lever. Once the label definitions are stable and the weak regions are better represented, persistent errors may point to model capacity rather than data quality. In this experiment, moving from the base student to a larger version on the same data added roughly another 1.8 percentage points of macro F1. A larger model is worth considering when the task depends on long context, nuanced language, or interactions between several low signal terms as the first response to a noisy dataset.

My order would be: fix the supervision, add data where it is missing, and increase model size only when the remaining errors suggest that the smaller student lacks the capacity for the task.

---

## The complete loop

The resulting loop is:

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

The loop needs three separate datasets:

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
- **Use every cheap signal available.** Probability margins, neighbours, keywords, metadata, source-level patterns, and model disagreement can all help retrieve useful unlabelled rows. Use combinations of these low information signals.
- **More data helps when it adds information.** Random sampling gets examples from regions where the model is already predictive. Boundary-targeted sampling has a better chance of changing what the model knows.
- **Use the smallest model that is adequate.** Local CPU inference keeps routine dataset scans cheap and trivial to run at scale. 
- **Measure marginal value.** Compare a targeted batch with an equally sized random batch, on a frozen holdout, before continuing to  the next iteration.

Distillation leaves behind more than a smaller model. It gives us a cheap instrument that should be fully automated to question the dataset: bootstrap with the LLM, probe with the student, and spend the next label where the model is still uncertain, inconsistent, or wrong.

**Do not spend the labelling budget teaching the model what it already knows.**
