---
title: Exploring optimal parameters over sample sizes  
excerpt: ""
header:
  image: /assets/images/hyperparam_sampling/header.jpg 
tags:
    - optimization 
share: true
subscribe: true
comments: true
--- 

This is the first of two posts about finding optimal parameters for machine learning models, and is motivated by [Hyper-Parameter Optimization: A Review of Algorithms and Applications](https://arxiv.org/abs/2003.05689), where subsampling is commented on a later section, as a strategy to reduce the training time; and doing so, reduces the search time for necessary to find optimal values. It's stated that subsampling is risky in terms of the potential to introduce more noise and uncertainty.  
On this first post we're going to explore what this means for some well known methods (Random Forest and SVM), if somehow there is some ability to generalize information gained at smaller samples which can somehow lead to a reduction of the computational budget.  
There are lessons that we expect to learn when exploring model performance and the amount of data it's given. A non-exaustive list:  
1. Are there scale dependent parameters or combinations of parameters  
2. How performance deteriorates and how much can be attributed to subsampling    
3. How does sample size affect the variance of the model score   
4. How the distribution of the scores varies over different sample sizes  

___

The key thing we need to explore is how model performance changes when we feed the models less and less data.   
Of course if models are not able to generalize what they learn from data, they're not very useful - but there is a size which serves as a boundary for lack of generalizing ability of the model.  

Let's pick then the well known Random Forest implementation by sklearn, and pick 3 of the many parameters we are given. The task is the well known, and now polemic, Boston housing dataset.  

What we expect to find is evidence that smaller samples are still informative for the optimal parameters of the dataset (sample size=100%).  
For each size and combination of parameters, we randomly sample from the original dataset, while keeping the random seed of the algorithm to maintain some amount of determinism.

{% capture fig_img %}
![Foo]({{ "/assets/images/hyperparam_sampling/one_param.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

We can see that the behaviour of the models is affected by the size of the sample - there are two components that are responsible for this: 
1. Less data means less to learn -> the performance necessarily decreases.  
2. Less data means greater variation in how the training data can be generated - some combinations can be very unrepresentative of the dataset. This needs to be explored further.  

The main insight here is that at the parameter curves seems to share a lot of features across sample sizes, and as the size increases the convergence seems to be even more apparent. To put it simply, the optimal parameters are quite similar after a certain size.  

___

Let's explore the variation of the scores a bit further.  
Let's focus on one parameter, min_sample_split and repeat the exploration a few times.  

{% capture fig_img %}
![Foo]({{ "/assets/images/hyperparam_sampling/variance_mss.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>
{% capture fig_img %}
![Foo]({{ "/assets/images/hyperparam_sampling/mean_and_sd_.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

Smaller samples have a greater variance than larger samples - there are certainly odd combinations, in particular for a small dataset as this one (500 records).  
Larger samples will have a significant overlap with the orignal dataset which means that there's less to vary in the training data, and the results should scatter much less.  
For this implementation, even for sample sizes equal to the entire dataset, the order is not kept and this adds additional variation, which is not only acceptable, but actually desirable to explore the inner workings of these methods.  

___

Before trying to observe the same patterns hold in other scenarios, let's take a minute and explore the distributions for the scores at each sample size. The reason is to start observing  the actual dynamics of these distributions as more data gets fed to the model.  
 
{% capture fig_img %}
![Foo]({{ "/assets/images/hyperparam_sampling/distributions.gif" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

Below we can see that if we exclude very low sample sizes, there is a very significant overlap in the R² scores distributions. In other words, there is plenty of useful information at lower samples.   

{% capture fig_img %}
![Foo]({{ "/assets/images/hyperparam_sampling/distributions_0.gif" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

On interesting aspect of these repeated draws at a specific sample size seems to be the bell shape of the distribution. Normality tests are passed and we can at least use this as information to model the behavior.

___

One continuation to this exploration needs to be related with the relation between sample size and more than one parameter.  
We have two examples of combinations of parameters that support what we saw previously: the surfaces share plenty of similarities for various sample sizes, and most importantly, the parameters that maximize the R² score seem to be at the very least neighbours and at the very best the exact same.  

{% capture fig_img %}
![Foo]({{ "/assets/images/hyperparam_sampling/min_min.gif" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

{% capture fig_img %}
![Foo]({{ "/assets/images/hyperparam_sampling/min_max.gif" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>
 
___

One final exploration with another model - a SVM - is carried out. There is no scaling of the features or anything remotely trying to maximize the performance; again, the point is to see that there is no dramatic changes to the model behaviour. 

{% capture fig_img %}
![Foo]({{ "/assets/images/hyperparam_sampling/svm.gif" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

We can see that for the very smallest sample size, the maximum seems to be contested by two distinct locations in the parameter space - expected. Small samples are troublesome as we've seen.  
The second smallest sample already seems to converge to the optimal set of parameters and at this point we can make some comments that motivate the next post.  
Our first method was the random forest, which scales quite nicely, with O(n.log(n)). SVMs on another hand have quadratic complexity, and this is key.  
To compute one model with the entire dataset it costs us the same as the cost of training seven in the second smallest sample size: we can understand the rough geometry of the surface with a lot more detail.  
A structured, yet simple, approach to how this exploration can be made, leveraging the trade-off between information gained and reduced computational load, is the content of the next post.

___

One comment regarding how different datasets affect what we observed above. There seems to be a point in the sample size after which the dataset is informative enough for the model to pick up patterns. Rich datasets are a bit more demanding when it comes to how small samples can be -- this adds another layer of variance to what we see.  
In the next post of this series we'll tackle this in a principled way.  
___

Thanks for reading and let me know if you have anything to say.