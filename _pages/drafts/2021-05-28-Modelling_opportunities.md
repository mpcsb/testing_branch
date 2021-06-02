---
layout: single
permalink: /drafts/bayesian_simulation/
title: "Bayesian based simulations"
subscribe: true
--- 

Let's cover some of the strong points when using bayesian models to make predictions and simulate scenarios in a structured manner.  
The ability that linear models provide to model noisy problems is one of the features I like. Using bayesian priors to inject domain knowledge in a model proves to be instrumental when observations alone may not be sufficient to determine driving factors in what we want to study.  

 
---

One study that seemed particularly suited to draw some of these conclusions was the modelling of what affects the success of sales opportunities.  
Some variations can be justified with different attributes (regions, industry, products,...), but the thing that determines whether or not an opportunity is converted to a sale is the price per unit. Of course additional factors such as competitor pricing would be very relevant, but quite hard to access.  
Because we understand what is being study so well, and we understand the impact of pricing, it's an ideal case to model, and an ideal model to manipulate in order to reach optimal scenarios.  

---

Let's set up a simulated dataset that resembles sales opportunities let's have the status of those opportunities depend on the price of these products and their relation to specific groups - in particular products and countries. In addition some random effects were also associated with information contained outside of the data.  
This random effects will be increased to compare how important prior distributions are to effectively model our observations.  

---

modelling

---

linear models extrapolate better
