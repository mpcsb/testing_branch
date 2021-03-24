---
title: "Subsampling as a strategy to find optimal parameters (2/2)"
excerpt: "Probing and fusing parameter space explorations"
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

Let's take this [example](https://github.com/fmfn/BayesianOptimization/blob/master/examples/sklearn_example.py) from bayes_opt and observe the standard bayesian optimizer run 100 models with the full dataset -- 10 randomly to get acquinted with the model's response and 90 to find the optimum.  

```
Optimizing Random Forest: 100 models; budget: 100 
|   iter    |  target   | max_fe... | min_sa... | n_esti... |
=============================================================
|  4        | -0.3418   |  0.4902   |  0.02077  |  10.02    |
|  8        | -0.3349   |  0.6166   |  0.01651  |  10.02    |
|  13       | -0.2919   |  0.999    |  0.01     |  250.0    |
=============================================================
``` 

{% capture fig_img %}
![Foo]({{ "/assets/images/bayes_opt_variation/full_1.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

To benchmark all the variants in the exploration we should have the same compute time to run 100 models; let's consider negligeble the compute time for the gaussian process that fits the hyperparameter space, even though it isn't 1) as observations grow, 2) as the hyperparameter space grows; 3) and if the model function is not to expensive to compute.   
Some remarks:   
1. Computational budget: we provide enough time to run a fixed number of models on the entire dataset. The budget is divided between different sample sizes, and for each size, we can compute a quantity of models given by the complexity relation.     
2. Fixing the lower percentage that samples the dataset. This can be tuned depending on the complexity of the data.
3. How many sample sizes should we explore?
4. What strategy to use when dividing the budget: equally over sample sizes or something more complex?
 

Sample percentage:30%
```
Optimizing Random Forest: 148 models; budget: 33 
|   iter    |  target   | max_fe... | min_sa... | n_esti... |
=============================================================
|  4        | -0.3858   |  0.4902   |  0.02077  |  10.02    |
|  9        | -0.3753   |  0.9791   |  0.01979  |  23.29    |
|  19       | -0.3539   |  0.6998   |  0.02344  |  241.5    |
|  43       | -0.3354   |  0.999    |  0.01     |  221.5    |
|  112      | -0.3344   |  0.999    |  0.01     |  46.79    |
|  137      | -0.3343   |  0.999    |  0.01     |  40.97    |
=============================================================
```
{% capture fig_img %}
![Foo]({{ "/assets/images/bayes_opt_variation/0_3.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

Sample percentage:70%
```
Optimizing Random Forest: 57 models; budget: 33
|   iter    |  target   | max_fe... | min_sa... | n_esti... |
=============================================================
|  3        | -0.3023   |  0.999    |  0.01     |  114.4    |
|  5        | -0.302    |  0.999    |  0.01     |  234.8    |
|  42       | -0.3006   |  0.7511   |  0.0109   |  67.98    |
=============================================================
```
{% capture fig_img %}
![Foo]({{ "/assets/images/bayes_opt_variation/0_7.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

Sample percentage:100%
```
Optimizing Random Forest: 33 models; budget: 33 
|   iter    |  target   | max_fe... | min_sa... | n_esti... |
=============================================================
|  32       | -0.2917   |  0.7301   |  0.01     |  250.0    |
=============================================================
```
{% capture fig_img %}
![Foo]({{ "/assets/images/bayes_opt_variation/1.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>
---

The key concern here is how to fuse the information gathered at one level and pass it to the next.  
Bayes_opt has a couple of functionalities that work out for this: passing points to probe (to highlight peaks and areas of interest that were discovered previously) and adjusting the boundaries in order not to explore flat areas; the second feature is adjusting the strategy of exploration. Exploring at lower samples and exploiting at higher samples seems promissing.   


---
### Code to replicate figures

```python
from sklearn.datasets import make_classification
from sklearn.model_selection import cross_val_score
from sklearn.ensemble import RandomForestClassifier as RFC 
from sklearn.gaussian_process.kernels import Matern, WhiteKernel
from sklearn.gaussian_process import GaussianProcessRegressor
from bayes_opt import BayesianOptimization
from bayes_opt.util import Colours

import numpy as np
import matplotlib.pyplot as plt
import matplotlib as mpl
from matplotlib import colors, cm 

from math import log, floor, sqrt

copper = mpl.cm.copper 
cNorm  = colors.Normalize(vmin=-0.9, vmax=-0.25)
scalarMap = cm.ScalarMappable(norm=cNorm, cmap=copper)
```

Utilities to compute time allocation

```python
def cost_per_model(pct, algo='svm'): 
    x = [i for i in range(1,101, 1)] 
 
    if algo == 'rf': 
        nlogn = [i*log(i) for i in x]
        return nlogn[99]/nlogn[int(pct*100) - 1]
    if algo == 'svm':
        n_n = [i*i for i in x]
        return n_n[99]/n_n[int(pct*100) - 1] 
    


def budget_division(budget, how='equal', steps=3, lower=0.4):
    
    def normalizing_factor(lst, budget):
        '''sum(lst).X = budget'''
        return budget / sum(lst)
    
    if how == 'equal':
        return [int(budget/steps) for _ in range(steps)]
    else:
        slices = [budget/(1+s) for s in range(steps)]
        norm_factor = normalizing_factor(slices, budget)
        normalized_slices = [norm_factor*s for s in slices]
        
        if how == 'linear_asc':
            return normalized_slices
        if how == 'linear_desc':
            return normalized_slices[::-1]
        

def models_at_sample_size(budget, sample_size, algo):
    return int(budget*cost_per_model(sample_size, algo))


def size(i, lower=0.4, steps=3):
    #i += 1
    return lower + i * (1 - lower)/(steps - 1)
```

```python
def get_data():
    """Synthetic binary classification dataset."""
    data, targets = make_classification(
        n_samples=5_000,
        n_features=22,
        n_informative=12,
        n_redundant=4, 
        random_state=0,
    )
    return data, targets
```

Function to optimize: random forest classifier being score with negative log loss.

```python
def rfc_cv(n_estimators, min_samples_split, max_features, data, targets): 
    estimator = RFC(
        n_estimators=n_estimators,
        min_samples_split=min_samples_split,
        max_features=max_features,
        random_state=2
    ) 
    
    cval = cross_val_score(estimator, data, targets,
                           scoring='neg_log_loss', cv=3)
    return cval.mean()
```

```python
# points to probe in next level. 
#Something dynamic like sqrt(observations) could do the job but needs additional control mechanisms.
n_points = 5

from sklearn.gaussian_process.kernels import (RBF, Matern, RationalQuadratic,
                                              ExpSineSquared, DotProduct,
                                              ConstantKernel)
def points_to_probe(optimizer):
    x0_obs = np.array([[res["params"]["max_features"]] for res in optimizer.res]) 
    x1_obs = np.array([[res["params"]["min_samples_split"]] for res in optimizer.res])
    x2_obs = np.array([[res["params"]["n_estimators"]] for res in optimizer.res]) 
    y_obs = np.array([res["target"] for res in optimizer.res]) 
     

    fig = plt.figure(figsize=(8,6))
    ax = fig.add_subplot(111, projection='3d')
    for m, zlow, zhigh in [('o', -50, -25), ('^', -30, -5)]: 
        ax.scatter(x0_obs, x1_obs, x2_obs, c=scalarMap.to_rgba(y_obs), alpha=0.5)

    ax.set_xlabel('max_features')
    ax.set_ylabel('min_samples_split')
    ax.set_zlabel('n_estimators')
    plt.colorbar(scalarMap)
    plt.tight_layout()
    plt.show()
        
    #plt.matshow(optimizer._gp.L_)
    #plt.title('Lower-triangular Cholesky decomposition of cov')
    #plt.show() 
    
    idx = y_obs.argsort()[-n_points:][::-1]
    probe = [[x0_obs[i], x1_obs[i], x2_obs[i]] for i in idx]
    
    return probe



def optimize_rfc(data, targets, level, cov_function_prior, n_iter=0, bounds=None, to_probe=None):
    """
    level: index + 1 of sample size in [pct0, pct1, .. pctN].
    cov_function_prior: definition of cov. function by the gaussian process regression. It's going to be updated every step.
    n_iter: number of models to be computed at each sample size. Is constrained by the total budget.
    bounds: updated boundaries for hyper param. space.
    to_probe: promissing points found in smaller sample sizes.
    
    
    """
    def rfc_crossval(n_estimators, min_samples_split, max_features): 
        return rfc_cv(
            n_estimators=int(n_estimators),
            min_samples_split=float(min_samples_split),
            max_features=max(min(max_features, 0.999), 1e-3), 
            data=data,
            targets=targets,
        )

    optimizer = BayesianOptimization(
        f=rfc_crossval,
        pbounds={
            "n_estimators": (10, 250),
            "min_samples_split": (0.01, 0.999),
            "max_features": (0.1, 0.999), 
        },
        random_state=1234,
        verbose=1
    ) 
    
    # model noise in each sample size (level)
    optimizer._gp.kernel = cov_function_prior + WhiteKernel(noise_level=0.01/(level + 1))
     
    if len(to_probe) > 0:
        for point in to_probe: 
            optimizer.probe(
                params=point,
                lazy=True,
                )
    
    # control structure to constrain compute budget
    if level == 1:
        init_points = 2 # minimum amount of points to start inference -> randomly generated.
    else:
        init_points = 0
    n_iter -= n_points 
        
    optimizer.maximize(init_points=init_points, n_iter=n_iter, acq="ucb", kappa=20/level) 
    
    #print(Colours.yellow(f'Prior kernel: {optimizer._gp.kernel}'))
    #print(Colours.purple(f'Posterior kernel: {optimizer._gp.kernel_}'))
    
    cov_function_posterior = optimizer._gp.kernel_

    return points_to_probe(optimizer), cov_function_posterior
```


```python
data, targets = get_data()

lower = 0.3
steps = 3
budget = 100

bounds = None
to_probe = []
cov_function_prior = Matern(nu=2.5) + WhiteKernel(noise_level=0.01)

plt.figure()
for level, b in enumerate(budget_division(budget, how='equal', steps=steps, lower=lower)):
    sample_size = size(level, lower, steps) 
    n_iter = models_at_sample_size(b, sample_size, 'rf')
    
    rows = int(len(data) * sample_size)
    idx = np.random.choice(len(data), rows, replace=False)
    sampled_X = data[idx,:]
    sampled_y = targets[idx]

    print(Colours.green(f"--- Optimizing Random Forest: {n_iter} models; budget: {b} --- "))
    to_probe, cov_function_posterior = optimize_rfc(sampled_X, sampled_y, level + 1, cov_function_prior, n_iter, bounds, to_probe)
    
    cov_function_prior = cov_function_posterior 
```
