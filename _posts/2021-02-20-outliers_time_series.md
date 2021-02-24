---
title: Identifying outliers in time series  
excerpt: ""
header:
  image: /assets/images/outliers_ts/header.jpg 
tags:
    -  time series
share: true
subscribe: true
comments: true
--- 

This is essentially a back of the envolope study for the identification of outliers in time series. The idea is to sketch a method that associates model quality to the presence of outliers.  
When dealing with data which does not follow time, finding outliers is hard, but even simple approaches might yield decent results. Setting a threshold for the percentile that determines what is a classifier works nicely in one dimensional data, and might even be useful in low dimensional data. To make sure, add a Bonferroni Outlier test and whatever you decide, it has some support.  
For time series that evidently not a satisfying answer. Even very rare values can be periodical; this is in fact a common pattern.  

One decent definition of outlier is a measurement that does not fit with the data generating process.   
For a sufficient amount of samples, the signal makes itself clear, even when in presence of _significant_ noise. Let's focus on the problem with a small amount of data points -- something like monthly series, a frequent business scenario.  

___

Let's create a small series which has the following decomposition:  
{% capture fig_img %}
![Foo]({{ "/assets/images/outliers_ts/signal_decomposition.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

We need to create a generating model which will be critical to evaluate the likelihood of a point being an outlier. Let's not use the entirity of our knowledge of the series.
For a series this simple, we'll use a gaussian processes regression, and we'll define the covariance function as the sum of the Matérn 5/2 kernel and a periodic kernel of period 12. We also define a linear mean funcion, with the slope defined with by a random variable that is inferred using MCMC.  
This is as a plausible injection of basic yet _informative_ priors to the model. More complex series may require complex models, which are harder to sample and harder to illustrate the idea of the post.  
 
___
 
A quick test, performing a 12 month forecast, shows the model capturing the signal pretty well when there is no noise, and as the noise magnitude increases,the predictive ability decreases, as expected.    

{% capture fig_img %}
![Foo]({{ "/assets/images/outliers_ts/forecast_snr.gif" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>  

___

One particular feature that I enjoy in gaussian processes is the ability to interpolate data very nicely and allowing imputation of missing values in a principled way. Because we can draw samples from the model, we can generate distributions for each of the points in the series. We exclude each point and, assuming the model is sufficiently well defined, we could collect percentile values for the values of the series.  
Now, the outcome of this step seems redundant or a symptom of a weak model/a hard problem to model. However, the main objective is to show that the absence of outliers will generate a superior model, that reduces the modelling error significantly for the rest of the series.  

This extra iteration over the entire series adds a significant amount of computing time to an already complex method - but this is a small series and a few seconds per model is nothing obscene
Below we get to see the process for the series with minimal amount of noise.

{% capture fig_img %}
![Foo]({{ "/assets/images/outliers_ts/interp.gif" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>  
 
___


{% capture fig_img %}
![Foo]({{ "/assets/images/outliers_ts/interp_1_outlier.gif" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>  

