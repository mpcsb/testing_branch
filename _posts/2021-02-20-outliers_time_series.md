---
title: Identifying outliers in time series  
excerpt: ""
header:
  image: /assets/images/outliers_ts/header.jpg 
tags:
    -  
share: true
subscribe: true
comments: true
--- 

This is essentially a back of the envolope study for the identification of outliers in time series.  
When dealing with data which does not follow time, finding outliers is hard, but even simple approaches might yield decent results. Setting a threshold for the percentile that determines what is a classifier works nicely in one dimensional data, and might even be useful in low dimensional data.  
For time series that evidently not a satisfying answer. Even very rare values can be periodical, in fact, that is a common pattern.  

One decent definition of outlier is a measurement that does not fit with the data generating process.   
For a sufficient amount of samples, the signal makes itself clear, even when in presence of _significant_ noise. Let's focus on the problem of a small amount of data points -- something like monthly series, a frequent business scenario.  

___

Let's create a small series which has the following decomposition:  
{% capture fig_img %}
![Foo]({{ "/assets/images/outliers_ts/signal_decomposition.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

We need to create a generating model which will be critical to evaluate the likelihood of a point being an outlier. Let's not use the entirity of our knowledge of the series.
For a series this simple, we'll use a gaussian processes regression, and we'll define the covariance function as the sum of the Matérn 5/2 kernel and a periodic kernel of period 12. We also define a linear mean funciont, with the slope defined with by a random variable that is inferred using MCMC.  
This is as a plausible injection _common sense_ priors into the model. More complex series may require complex models, which are harder to sample and harder to illustrate the idea of the post.  

code 
code

___
 
A quick run indicates that the model captures the signal perfectly when there is no noise. 
As noise keeps getting added, the performance of the forecast decreases, as expected.  

{% capture fig_img %}
![Foo]({{ "/assets/images/outliers_ts/forecast_snr.gif" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>
