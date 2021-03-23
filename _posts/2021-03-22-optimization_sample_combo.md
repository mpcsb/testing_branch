---
title: "Subsampling as a strategy to find optimal parameters"
excerpt: "Part 2: probing and fusing parameter space explorations"
header:
  overlay_image: /assets/images/bayes_opt_variation/header.jpg  
tags:
    - machine learning 
    - optimization
share: true
subscribe: true
comments: true
--- 


This follow up to this [post](https://www.testingbranch.com/parameter_optimization_subsampling/) where we explore the changes in the output of machine learning models when they are trained on samples of varying sizes.   
This second part will try to explore a bit deeper in what circumstances subsampling is helpful; compare convergence speeds with a standard bayesian optimization approach; and observe if there's a strategy to how we spend our computational budget.  

---

Some preliminary thoughts:  
1. Complexity of the models determine how profitable it is to explore in lower samples. For quadratic algorithms and ignoring the actual implementation, training one model with a full dataset should cost the same amount of time as training 6.25 with 40% of that dataset.   
2. Before a threshold sampling percentage, the results of a model are not informative for the full dataset. Being greedy doesn't help here.  
3. Overall, models at smaller samples seem to be noisier images of the full dataset models.

---

Let's take this [example](https://github.com/fmfn/BayesianOptimization/blob/master/examples/sklearn_example.py) from bayes_opt and observe the standard bayesian optimizer running 100 samples -- 10 randomly to get acquinted with the model's response and 90 to find the maximum.  

[run and insert bayes_opt results]

---

To benchmark all the variants in the exploration, let's fix some figures:  
1. Computational budget: we provide enough time to run N models on the full data. The budget is divided between different sample sizes, and for each size, we can compute a quantity of models given by the complexity relation.  
2. We fix the lower percentage that samples the dataset. This can be tuned depending on the complexity of the signal in the data.
3. How many sample sizes should we explore?
4. How to strategy to use when dividing the budget: equally over sample sizes or something more complex?
 
```python
def abcd: 
    return -1 
```

---

The key concern here is how to fuse the information gathered at one level and pass it to the next.  
Bayes_opt has a couple of functionalities that work out for this: passing points to probe (to highlight peaks and areas of interest that were discovered previously) and adjusting the boundaries in order not to explore flat areas; the second feature is adjusting the strategy of exploration. Exploring at lower samples and exploiting at higher samples seems promissing.   




