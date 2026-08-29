---
title: "Distilling an LLM, then choosing what to label next"
excerpt: "2026-08-29 — Using a small student model not only to reproduce LLM labels, but to find weak class boundaries and decide where the next labels will be most useful."
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

LLMs are very good at classification tasks that used to require a custom model.

They can also be awkward to serve when the task itself is stable. The model is large, often proprietary, its behaviour can change, and every prediction has a cost.

A natural alternative is to use the LLM offline: ask it to label enough examples, keep those decisions as data, and train a smaller model to reproduce them.

This is not distillation in the strict sense of training on a teacher's logits. The thing being transferred here is the **decision**: an LLM creates supervision, then a smaller model learns from its hard labels.

I wanted to explore three questions:

1. How many LLM-labelled examples does the smaller model need?
2. Can disagreements between student and teacher expose questionable labels?
3. Can the remaining errors tell us which labels would be useful to acquire next?

The third question turned out to be the most interesting. Once the student is reasonably good, adding more random labels spends part of the budget on regions it already understands. The errors provide a way to spend that budget around weak decision boundaries instead.

---

## A small public experiment

I used 3,000 reviews from the Amazon Reviews 2023 Appliances dataset and reduced the task to two classes:

- `defect`: a concrete failure in construction, operation, durability, or intended performance;
- `no_defect`: no product failure, including preference, compatibility, misuse, shipping, packaging, seller, or service issues.

The distinction is deliberately semantic. A one-star review is not necessarily a defect, while a product that stops working is a defect even if the rest of the review is positive.

The LLM received the product and review text plus these rules. It did not receive the star rating. I kept 400 reviews as an untouched holdout and used the remaining 2,600 for model development.

The student was [`microsoft/deberta-v3-base`](https://huggingface.co/microsoft/deberta-v3-base). It received only the review title and text. The training setup was intentionally ordinary: up to six epochs, early stopping, balanced class weights, and macro F1 for checkpoint selection.

The full run reached:

| Metric | Holdout |
|---|---:|
| Accuracy | 0.9025 |
| Macro F1 | **0.8819** |
| Defect F1 | 0.8326 |
| No-defect F1 | 0.9312 |

The aim was not to maximize this score. I wanted a useful student and, more importantly, a way to study the data around it.

---

## How much teacher data was enough?

I trained the same model repeatedly, changing only the number of LLM-labelled examples available. Every run used the same 80/20 training-validation procedure and the same 400-row holdout.

![Holdout macro F1 by number of LLM-labelled examples](/assets/images/llm_distillation/data_efficiency.png)

| LLM-labelled rows available | Rows used to fit | Holdout macro F1 |
|---:|---:|---:|
| 100 | 80 | 0.4161 |
| 250 | 200 | 0.4161 |
| 500 | 400 | 0.8104 |
| 1,000 | 800 | 0.8406 |
| 2,000 | 1,600 | 0.8566 |
| 2,600 | 2,080 | **0.8819** |

With 100 or 250 source labels, the model collapsed to the majority class and predicted every holdout review as `no_defect`. At 500 labels it became useful: macro F1 jumped to 0.81. The full dataset reached 0.88.

More teacher data helped, but the returns were not linear. A few hundred examples bought most of the initial model; later labels refined its boundary. Once the cost per teacher label is known, this becomes a direct cost-performance curve.

This resembles an earlier [subsampling experiment](https://www.testingbranch.com/parameter_optimization_subsampling/): small samples can contain a surprising amount of useful information, but below a certain size the signal becomes unreliable. Here the resource being purchased is supervision rather than compute for parameter search.

---

## Disagreement is a compact label audit

The full model disagreed with 39 of the 400 holdout labels. Instead of treating all 39 as model failures, I sorted them by confidence and read them again using the original rules.

Some disagreements were label errors; others were very clear model errors.

| Shortened review | Original label | Student | Confidence | Audit |
|---|---|---|---:|---|
| “Handle attachment is chipped and sharp out of the box” | `no_defect` | `defect` | 99.72% | label wrong |
| “It didn't seem to be filtering anything” | `no_defect` | `defect` | 99.85% | label wrong |
| “WAY too big to fit my regular stove” | `no_defect` | `defect` | 99.71% | model wrong |
| “Hinge came broken ... holes had no threads” | `defect` | `no_defect` | 99.96% | model wrong |

Ten of the 39 holdout disagreements were clear label errors. On the training set, the model disagreed with only 65 of 2,600 labels; reviewing those surfaced another 19 clear errors.

In total, reading 104 disagreements found 29 labels worth correcting. Instead of reviewing all 3,000 LLM labels, I reviewed 3.5% of them.

A disagreement is not proof that the teacher was wrong. Some of the most confident disagreements above are obvious student mistakes. It is simply a high-yield filter over the teacher's work.

The confidence is also important. Many useful disagreements were above 99%, so a loop that sends only low-confidence student predictions back for review would miss them. Confidence describes the student's certainty about its own boundary; it does not establish that the label on the other side is trustworthy.

---

## Correcting labels is not the same as improving the model

I corrected the 29 clearest cases—19 in training and 10 in the holdout—then retrained from scratch. The retrained model reached 0.9048 macro F1 against the corrected holdout.

Comparing that directly with 0.8819 would be misleading. Ten holdout labels had been selected precisely because the original model disagreed with them. Correcting the evaluation labels therefore improves the apparent score even without changing the model.

In fact, the **old** model scores approximately 0.914 macro F1 on the corrected holdout, slightly above the retrained model. This run shows that disagreement improved the dataset; it does not show that changing 19 training labels improved generalization.

That distinction matters. Label auditing asks, “which existing labels are questionable?” Data acquisition asks, “which new examples could change what the model has learned?” The same errors can guide both activities, but only a clean holdout can tell us whether either activity improved the model.

---

## From individual errors to weak regions

For a final pass, I joined the retrained model's remaining errors to metadata it had never seen. Star rating is a crude heuristic, but it cheaply identifies different linguistic regimes in the reviews.

![False negatives and false positives by review rating](/assets/images/llm_distillation/errors_by_rating.png)

The model had no errors on five-star reviews and few on four-star reviews. Most errors were in the one- to three-star range, but the direction of error was more useful than the total:

- In three-star reviews, 8 of 26 actual defects were missed. These reviews often mix neutral or positive language with a partial failure.
- In one-star reviews, 5 of 29 `no_defect` examples were called defects. Strong negative sentiment can come from incompatibility or expectations without describing a product failure.

These are different regions of the decision boundary:

- **mixed language + real defect**;
- **strong negative language + no defect**.

If I bought another batch of labels, I would deliberately sample from those regions and measure their marginal value rather than label another random batch of appliance reviews.

Rating is only one weak heuristic. Depending on the task, useful slices can come from keywords, source, category, product attributes, time periods, embedding clusters, or combinations of them. They do not need to classify correctly. Their job is to help locate examples near a known weakness.

---

## Why multiclass boundaries make this more useful

The appliance experiment is binary, but the result that motivated this work came from a separate ordered three-class problem. The underlying data are not publishable, so I will describe only the abstract structure and keep it separate from the reproducible results above.

Call the classes `A`, `B`, and `C`. The model already understood the interiors of `A` and `C`. Its errors concentrated around the adjacent boundaries `A ↔ B` and `B ↔ C`; almost no budget was needed for an implausible `A ↔ C` confusion.

In that experiment, changing roughly 50 targeted training labels moved macro F1 by about **two percentage points** after retraining. The number 50 was not important by itself. Those rows mattered because they sat on weak boundaries and changed where the model placed them.

This suggests a more useful unit of analysis than “hard example”:

> Which class boundary is weak, and which observable slice helps us find more examples near it?

For a multiclass model, the workflow becomes:

1. Count disagreements by direction, such as `A → B` and `B → A`, rather than only counting total errors.
2. Identify the boundaries with enough errors to matter.
3. Within those boundaries, use cheap heuristics or metadata to describe recurring slices.
4. Review questionable labels and acquire new teacher labels from those slices.
5. Retrain and evaluate once on a holdout that was not used to choose the rows.

This avoids improving the model where it is already nearly perfect. It also makes “get more data” specific enough to test: acquire a small targeted batch, compare its marginal value with an equally sized random batch, and keep the strategy only if it wins.

```text
LLM labels a broad sample
        ↓
student learns the task
        ↓
directional disagreements reveal weak class boundaries
        ↓
metadata and weak heuristics reveal slices within those boundaries
        ↓
review labels or acquire targeted examples
        ↓
retrain and compare against random acquisition
```

---

## Final remarks

- A few hundred LLM-labelled examples were enough to train a useful specialist model for this task.
- Student-teacher disagreement reduced a 3,000-row label audit to 104 candidate rows and found 29 clear label errors.
- Correcting evaluation labels can create an apparent gain, so the holdout must remain outside the label-selection process.
- Error direction matters in multiclass problems: it tells us which boundaries need data and which ones do not.
- Weak heuristics are useful as search tools even when they would be poor classifiers.
- The next batch should be compared with random acquisition. Otherwise, “targeted” is only a plausible story.

The useful output is therefore not only the distilled model. It is a feedback loop between **teacher, dataset, and student**: the teacher bootstraps the task, the student exposes where the supervision is thin, and the next labels are spent where they can still move the boundary.