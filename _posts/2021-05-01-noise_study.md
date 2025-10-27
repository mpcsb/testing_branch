---
title:  "Noise, Stability, and Calibration"
excerpt: "How models behave when the data gets messy — and what calibration does about it."
header:
  overlay_image: /assets/images/noise_study/header.png
tags:
  - machine-learning
  - noise
share: true
subscribe: true
comments: true
---

## Motivation

Some models thrive on clean, abundant data. Others hold their own when the data is noisy, inconsistent, or incomplete.  
This post asks a simple question that [Claudia Perlich once explored on Quora](https://www.quora.com/Which-classifier-works-best-with-noisy-data):

> *Which models degrade most gracefully when the data gets noisy?*

To find out, I simulated different kinds of noise and compared **logistic regression**, **random forests**, and **XGBoost** — both *before* and *after* applying **isotonic calibration** to their predicted probabilities.

---

## Setup

We generate a synthetic binary classification dataset with moderate signal (12 features, 6 informative).  
Noise is injected in three ways:

1. **Label noise** – randomly flipping a share of true labels (0 → 80 %).  
2. **Gaussian feature noise** – smooth jitter added to every feature.  
3. **Laplace feature noise** – heavy-tailed outliers.

Each run evaluates:

- **AUC** and **accuracy** – discrimination and correctness  
- **Log-loss** and **Brier score** – probability quality  
- **Expected Calibration Error (ECE)** – reliability of confidence

All models were trained with scikit-learn / XGBoost defaults and isotonic calibration via 3-fold cross-validation.

---

## Label Noise — When truth itself wobbles

When labels are wrong, all models lose accuracy — but **logistic regression** holds up best.  
Its AUC falls from ~0.93 → 0.74 as labels become 80 % corrupted.  
Random Forest and XGBoost drop faster, confirming that high-capacity models can easily “learn” the noise.

{% capture fig_img %}
![AUC vs Label Noise]({{ "/assets/images/noise_study/label_noise_auc.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>
  *Line plot showing AUC vs. label-noise fraction (x-axis 0–0.8). Curves for Logistic Regression (blue), Random Forest (green), XGBoost (orange), and their calibrated versions (dotted lines). Logistic curve declines slowest; XGBoost drops fastest.*
  </figcaption>
</figure>

Calibration doesn’t recover accuracy — it’s not supposed to — but it **halves the ECE** for both ensembles, making their probability estimates realistic again.

{% capture fig_img %}
![Reliability Diagrams – Label Noise]({{ "/assets/images/noise_study/reliability_label_0_vs_0.8.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>
  *Four reliability diagrams (0 % and 80 % label noise, before/after calibration).  
  Uncalibrated curves bow away from the diagonal; after isotonic calibration they align closely along the 45° line.*
  </figcaption>
</figure>

---

## Feature Noise — The world gets blurry

Injecting Gaussian noise into features barely dents the models.  
AUCs stay near 0.96 even with heavy jitter.  
XGBoost and Random Forest remain accurate, and logistic regression degrades smoothly.

{% capture fig_img %}
![AUC vs Gaussian Noise]({{ "/assets/images/noise_study/feature_noise_gaussian_auc.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>
  *Line plot of AUC vs. Gaussian-noise level. All three models cluster tightly; calibrated variants overlay nearly indistinguishably, illustrating robustness to feature jitter.*
  </figcaption>
</figure>

Calibration again reduces ECE and Brier loss without touching accuracy.

| Model | Mean ECE (before) | Mean ECE (after) |
|:------|------------------:|-----------------:|
| RF | 0.066 | **0.031** |
| XGB | 0.032 | **0.024** |
| Logistic | 0.030 | 0.031 |

{% capture fig_img %}
![Reliability – Gaussian Noise]({{ "/assets/images/noise_study/reliability_gaussian_0_vs_0.8.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>
  *Two-panel reliability plot for Random Forest (or XGBoost) at 0 % vs 80 % Gaussian noise.  
  The post-calibration curve aligns more closely with the diagonal, showing improved probability reliability.*
  </figcaption>
</figure>

---

## Heavy-Tailed (Laplace) Noise — Outliers everywhere

Laplace noise simulates occasional extreme outliers.  
All models keep strong accuracy (AUC ≈ 0.96), but ensembles become **over-confident** in these odd regions.  
Calibration again fixes that.

{% capture fig_img %}
![AUC vs Laplace Noise]({{ "/assets/images/noise_study/feature_noise_laplace_auc.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>
  *AUC vs. Laplace-noise level.  
  Logistic, RF, and XGB curves remain high and close; calibration barely shifts AUC, underscoring that it affects confidence, not ranking.*
  </figcaption>
</figure>

{% capture fig_img %}
![Reliability – Laplace Noise]({{ "/assets/images/noise_study/reliability_laplace_0.8_xgb_cal.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>
  *Side-by-side reliability diagrams for XGBoost at 80 % Laplace noise:  
  Left – uncalibrated (S-shaped, over-confident); Right – after isotonic calibration (points along the diagonal).*
  </figcaption>
</figure>

---

## What calibration really changes

| Noise Type | Model | Δ ECE (before → after) |
|:------------|:------|-----------------------:|
| Label | XGB | −0.07 |
| Label | RF | −0.02 |
| Gaussian | RF | −0.03 |
| Laplace | RF | −0.06 |

Calibration barely nudges AUC or accuracy — but it **restores probability trustworthiness**.  
For logistic regression, gains are minimal (it was already well-calibrated).  
For ensembles, isotonic calibration transforms spiky, over-confident scores into credible probabilities.

---

## Takeaways

- **Label noise** hurts most — accuracy collapses, especially for flexible models.  
- **Feature noise** (Gaussian / Laplace) is survivable.  
- **Logistic regression** remains the most stable and naturally calibrated.  
- **XGBoost + Isotonic calibration** gives the best *calibrated* accuracy on cleaner data.  
- Always calibrate when probabilities drive downstream decisions (risk, pricing, triage).

---

> “In practice, linear models are surprisingly robust to noisy data, while complex trees can chase the noise.”  
> — *Claudia Perlich*


**
