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

This is essentially a collection of thoughts on the identification of outliers time series.  
We're narrowing the scope of what signals we're dealing down to time series composed of a few dozen measurements -- these are frequent in business scenarios, for instance as monthly revenue or expenses.  
The key idea here is that whatever is considered an outlier, is not expected from the data generating process. If there's some amount of prior information about what generates, then a generative model can be constructed.  
This post is a small sketch around the response of the model when we exclude each of the data points that make the series.  
You probably got an itch when reading the exclusion of **each** data point, and rightfully so; but this is a retrospective exercise, so a relaxed stance is acceptable.  

___

First thing to try is the detection of the outliers; second thing to explore is the signal to noise ratio and how it affects outlier identification.  
Our first time series is essentialy the sum of a yearly period a sine trend and gaussian noise. This is a simple series in order for the generating model to also be simple.  

Let's model this using a Gaussian Processes regression, specifying a periodic kernel, with a period of 12 months, and a Matern kernel, to model the remaining interactions.  

[code]  

[/code]  

