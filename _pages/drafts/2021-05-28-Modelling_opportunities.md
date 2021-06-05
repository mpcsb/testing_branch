---
title: Model based simulations  
excerpt: "Bayesian decision making applied to sales opportunities"
permalink: /drafts/bayesian_simulation/
header:
  overlay_image: /assets/images/bayesian_simulation/header.jpg 
tags:
    -  bayesian modelling, simulation
share: true
subscribe: true
comments: true
--- 


Once we have a statistical model built, assuming it's a decent one, we can use it for more than predicting outcomes of things to come. For this post, we're going to build a simple model and extract insights from it in order to exploit the environment in which our observations take place.  
The ability that linear models provide to model noisy problems is one of the features I like. Using Bayesian models, we have added strengths in our model: the ability to inject domain knowledge in a model -> instrumental when observations alone may not be sufficient to determine driving factors in our outcomes; we can quantitfy the uncertainty associated with our predictions, and we can quantify it in a principled way.  
If we want to estimate the outcome of simulated scenarios, this is very valuable.  

---

One study that seemed particularly suited for this, was the case of converted sales opportunities. To give just enough context, typically sales reps log opportunities in the accounts they monitor, and they log information relevant for it. In particular, the unit price of the offer and status -- whether it was converted or not.     
Some attributes in these logs ends up being very informative for the outcome of the opportunity. Much like with anything that we purchase, the price is *the* driving factor behind a conversion. The said, the data does not contain all information needed to make deterministic claims about the opportunity; competitor pricing conditions or the credit limit for a specific account would of course have an impact, and in it's absence, the conversion target becomes noisier.
Because we understand what is being study so well, and we understand the impact of pricing, it's an ideal case to model, and an ideal model to manipulate in order to reach optimal scenarios.  

---

Let's set up a simulated dataset, of 500 records, that resembles sales opportunities.  
There will be a conversion status (won/lost -> 1/0) of those opportunities. This label was made to depend primarily on unit price of the items being sold and their relation to specific groups -- this is a random effect and represents potential sales reps' discounts or promotions. Additionally, random effects were also added to represent events not contained in the dataset.  

The basic mechanics of the [code](https://www.testingbranch.com/src_model_simulation/) that generates the data, is that we have a base price for each product, and based on the amount ordered, there will be quantity discounts. In addition, each country and each product might have promotions (relatively small magnitude effects) which *don't interact* with each other.  
The ratio between the discounted unit price and the base price is the major force in the conversion mechanism in our simulated data.  

There was a zscore normalization applied to the price feature - essentially a transformation that is close to zero (naturally easy to assign prior distributions to).

Some plots that show how the target varies with the 5 simulated products and the 3 simulated prices. There is a clear division on the zscore -- and the model should pick it up easily.   

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/country_conversion.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/product_conversion.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

---

Let's then setup a linear model to study converted opportunities; I'll use pymc3 to implement the bayesian form of a logistic regression. If some aspect behind the model definition escapes you, refer to their [examples and docs](https://docs.pymc.io/).  
Our model will have a linear terms for products and countries and it will use the logit as a link function to generate probabilities. These probabilities are used in a Binomial distribution to generate the posterior distribution.  
Because we know that the unit price is the most important factor here, let's set a prior distribution that is able to reach larger values easily. This will generalize for all country and products.    
Countries and products were marginalized - we have essentially one model per combination of product and country, with shared intercepts. Because we can still use NUTS in this model formulation, this is more performant and in the end accurate than most alternatives. Using a sampler that is able to sample from discrete variables is possible, but is not fast and it can result in completely inaccurate posteriors.    

y = intercept + intercept_prod + alpha_prod * price + intercept_country + alpha_country * price  
prob =  inverse_logit(y)  
observations ~ Binomial(p=prob)  

N=len(train_status)
dim1 = len(set(product_id))
dim2 = len(set(country))  

      with pm.Model() as shared_data_model: 

          intercept = pm.Normal('intercept', mu=0, sd=1)  

          alpha_product = pm.Normal('alpha_product', mu=0, sd=1, shape=dim1)
          alpha_country = pm.Normal('alpha_country', mu=0, sd=1, shape=dim2) 

          sigma_beta = 3
          beta_product = pm.Normal('beta_product', mu=0, sd=sigma_beta, shape=dim1)
          beta_country = pm.Normal('beta_country', mu=0, sd=sigma_beta, shape=dim2)  

          train_cty = pm.Data("train_cty", train_country)
          train_p = pm.Data("train_p", train_product_id)
          train_offers = pm.Data("train_offers", train_normalized_offers)
          train_p_cty = pm.Data("train_p_cty", train_p_cty)

          p = invlogit(intercept 
                       + alpha_product[train_p] 
                       + alpha_country[train_cty]    
                       + beta_product[train_p] * train_offers 
                       + beta_country[train_cty] * train_offers   
                      ) 

          y = pm.Bernoulli('y', p=p, observed=train_status) 

          trace = pm.sample(init='advi+adapt_diag', n_init=100000,
                                tune=1000, draws=1500, chains=3, cores=8,
                                target_accept=0.90, max_treedepth=10)
      az.plot_trace(trace, compact=True); plt.show()


{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/traceplot.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

For simple models such as this, even weaker priors would probably be informative enough. Adding terms for other attributes, like industry or period, will make it more complex, and harder to sample.  
Also, in cases where noise is significant and our observations are not providing a clear signal for the model to pick up, encoding knowledge in priors helps the sampler significantly.  


The model seems to pick up the signal clearly, and the separation in the conversion of opportunities by the pricing is clear.  

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/posterior_predictive.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

This is replicated in our hold-out dataset in which we're going to perform our simulations.  
{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/test_posterior.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>


Below we can observe the predictions of the test set and the uncertainty (the standard deviation of the posterior predictions) of each prediction. This is will be helpfull to understand how much trust can be deposited in each prediction.   

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/simul_prob_var_circle1.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>


---

Linear models extrapolate well, or at least better than other classes of models, but of course, the extrapolations follow a linear relation. This is not realistic of course - we can imagine that there are strong non-linear relations if unit price get close to nothing, and also when they get several times higher than the base price. That said, they're still helpful within reasonable values.  


If we wanted to answer the question of what discount to apply to an offer to have it accepted, in this models, it's simply a matter of sampling from the posterior with a different price value.  
In the plot below we can see a range of discounts that would turn previously declined offers into conversions. Quite interesting! Ideally a sales rep would like to see large spikes, without granting large discounts.  


{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/discount.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>


The same exercise can be executed to assess ideal increases to unit prices.  
Here we can see the amount of offers lost as we keep raising the prices -- sales reps could use this to increase prices just below what would lose an offer, or to maximize sales (if you're able to sell for 3x the base price, some lost offers could be acceptable). This is business dependent.   

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/mark-up.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

A final remark: all of these predictions and simulations should be considered based on the uncertainty of the model; however this also assumes the we were able to build something that models the behavior well enough.  


[Code](https://www.testingbranch.com/src_model_simulation/)
