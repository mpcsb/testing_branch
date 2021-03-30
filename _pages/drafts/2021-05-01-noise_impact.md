---
layout: single
permalink: /drafts/noise_impact/
title: "Comparing high and low variance models with noisy data"
subscribe: true
--- 


This post is an exploration based on this [quora answer](https://www.quora.com/What-are-the-advantages-of-logistic-regression-over-decision-trees-Are-there-any-cases-where-its-better-to-use-logistic-regression-instead-of-decision-trees/answer/Claudia-Perlich?ch=10&share=ef233af4&srid=28C3J) by Claudia Perlich. The post will try to explore a but further in what circumstances some low variance models outperform high variance models.  

Essentially, the route for the post is as follows:
1. Generate data with a binary target -- to compare with the metrics mentioned in the post.
2. Choice of one low variance model (a logistic regression) and a high variance model (a random forest).
3. Generate custom features for each model -- e.g. interaction terms for LR or numerical interactions for RF.  
4. The best performance for each model will serve as a benchmark for the subsequent conditions.
5. Add progressively more noise to the target and compare the performance drop for each model.
6. Add progressively more noise to the features and compare the performance drop for each mode.  

