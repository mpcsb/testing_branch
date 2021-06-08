---
title: Model based simulations  
excerpt: "Bayesian decision making applied to sales opportunities"
permalink: /drafts/bayesian_simulation/
header:
  overlay_image: /assets/images/bayesian_simulation/header.jpg 
share: true
subscribe: true
comments: true

--- 

For this post, we're going to build a very simple model and extract insights from it in order to simulate specific scenarios.  
Linear models are able to handle noisy observations with some abiity and are in the end more resilient — as oppposed to high variance models, they don't get lost in the weeds, focusing on irrelevant details.   
Using Bayesian models, we have additional strengths in our model: the ability to inject domain knowledge in a model -> instrumental when observations alone may not be sufficient to determine the driving factors in our outcomes; and we can quantitfy the uncertainty associated with our predictions in a principled way. It comes directly from the posterior distributions, straight from the working principle of the algorithm.    
If we want to estimate the outcome of simulated scenarios, this is very valuable.  

---

One study that seems particularly suited for this, is the case of converted sales opportunities.  
To give just enough context, typically sales reps log opportunities in the accounts they monitor, and they log information relevant for it. In particular, the unit price of the offer and status — whether it was converted or not.     
Some attributes in these logs end up being very informative for the outcome of the opportunity. Much like with anything that we purchase, the price is *the* driving factor behind a conversion.  
That said, the data does not contain all information needed to make deterministic claims about the opportunity; competitor pricing conditions or the credit limit for a specific account would of course have an impact, and in it's absence, the conversion target appears noisier.
Because we understand what is being study so well, and we understand the impact of pricing, it's an ideal case to model.  

---

Let's set up a small simulated dataset of 500 opportunities.  
There will be a conversion status (won/lost -> 1/0) and it will depend primarily on the unit price of the items being sold as well as specific attributes (the account country and the product being sold) -- this is represented with a random effect and can be interpreted as potential sales reps' discounts or product promotions.  
Additionally, random effects were also added, and here we want to represent factors that have a direct impact on the conversion of the opportunity, essentially model market competitiveness.  

The basic mechanics of the [code](https://www.testingbranch.com/src_model_simulation/).  
 
Some plots that show how the target varies with the 5 simulated products and the 3 simulated countries. There is a clear division on the ratio of the offered unit price and the base price.  

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/country_product.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure> 

---

Let's then setup a simple model to study converted opportunities. This is not meant to ideally model the data, it's just something to generate simulations.  
I'll use pymc3 to implement the bayesian form of a logistic regression. If some aspect behind the model definition escapes you, refer to their [examples and docs](https://docs.pymc.io/).   
The pricing figures are zscored, essentially a transformation that is close to zero (naturally easy to assign prior distributions to).  

Our model will have a linear terms for products and for countries in addition to a common intercept; it will use a logit as a link function to generate probabilities. These probabilities are used to generate a Binomial distribution to model our observations.  
Because we know that the unit price is the most important factor here, let's set a prior distribution for a multiplicative parameter, which is free to reach larger values easily.  
To efficiently explore the parameter space of the model, we want to have a performant sampler. Pymc3 implements NUTS, which efficient as it is, is not able to explore discrete parameters. Other samplers are able to deal with discrete values, but not efficiently as potentially inaccurate.  
By marginalizing over the discrete values in the model, we can still use NUTS in this model formulation and without loss of information. 

The overall formula for the model:  
y = intercept + intercept_prod + alpha_prod * price + intercept_country + alpha_country * price  
prob =  inverse_logit(y)  
observations ~ Binomial(p=prob)  

      
      N=len(train_status)
      dim1 = len(set(product_id))
      dim2 = len(set(country))  

      with pm.Model() as shared_data_model: 

          intercept = pm.Normal('intercept', mu=0, sd=1)  

          alpha_product = pm.Normal('alpha_product', mu=0, sd=10, shape=dim1)
          alpha_country = pm.Normal('alpha_country', mu=0, sd=10, shape=dim2) 

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

This model is simple enough for this data, so there's no divergences or anything that raises any red flags. Let's proceed.  

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/traceplot.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

For simple models such as this, even weaker priors would probably be informative enough. Adding terms for other attributes, like industry or some time component will make it more complex and harder to sample.  
In cases where noise is significant and our observations are not providing a clear signal for the model to pick up, encoding knowledge in priors helps the sampler significantly.  


Sampling from the posterior, we can see the separation in the conversion of opportunities by the pricing is clear.  
We can observe the highest posterior density regions and how well it separates te normalized price. Other transformations, like zscoring the price by product, presented cleaner regions, but since the performance of the model was identical,  having the price presented as it is was more convenient for the simulations — the focus of the post.  

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/train_posterior.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>


Below we can observe the predictions of an hold-out set and the uncertainty (the standard deviation of the posterior predictions) of each prediction. This is will be helpfull to understand how much trust can be deposited in each prediction.  
Notice that the standard deviation for a Binomial distribution is bounded at 0.5. Anything greater would make probability pend towards the other outcome.

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/simul_prob_var_circle1.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

In addition to the posterior deviation in our predictions, we can also assess uncertainty in these models by investigating the individuals distributions that composed the model.  
Listing the standard deviations of the posteriors is an easy way to quantify that some predictions, because they're modelled by wider curves, will have inherently more uncertainty associated.  

---

Linear models extrapolate well, or at least better than some classes of models, but of course, the extrapolations assume a linear relation.  
This is not realistic of course — we can imagine that there are strong non-linear relations if unit price get close to nothing, and also when they get several times higher than the base price. That said, they're more helpful nearer values that have been observed.  


If we wanted to answer the question of what discount to apply to an offer to have it accepted, in this models, it's simply a matter of sampling from the posterior with a different price value.  
In the plot below we can see a range of discounts that would turn previously declined offers into conversions. Quite interesting! Ideally a sales rep would like to see large spikes in won opportunities without giving large discounts.  

Below we can see the evolution of conversions with discounts and the color represent the mean uncertainty of all previously declined offers. The smaller prices will affect the outcome of the logit model. The shape of the posterior on the other hand fixed, so we can also interpret some of the marginalized distributions for countries of for products.  

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/discount.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>


The same exercise can be executed to assess ideal increases to unit prices.  
Here we can see the amount of offers lost as we keep raising the prices — sales reps could use this to increase prices just below what would lose an offer, or to maximize sales (if you're able to sell for 3x the base price, less business could be acceptable).    

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/mark-up.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>


[Code](https://www.testingbranch.com/src_model_simulation/)
