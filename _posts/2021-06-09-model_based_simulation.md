---
title: Model based simulations  
excerpt: "Bayesian decision making applied to sales opportunities"
header:
  overlay_image: /assets/images/bayesian_simulation/header.jpg 
share: true
subscribe: true
comments: true

--- 

For this post, we're going to build a very simple model and extract insights from it in order to simulate specific scenarios.  
Linear models are able to handle very noisy observations with some abiity and are in the end more resilient — as oppposed to high variance models, they don't get lost in the weeds, focusing on irrelevant details.   
Using Bayesian regression models, we have additional strengths in our model: the ability to inject domain knowledge in a model -> instrumental when observations alone may not be sufficient to determine the driving factors in our outcomes; and we can quantitfy the uncertainty associated with our predictions in a principled way. It comes directly from the posterior distributions, straight from the working principle of the algorithm; one additional advantage is the fact that the end result of a bayesian model are probability distributions, and this means that we can communicate probabilities to domain experts instead of p-values, confidence intervals, ... and other statistical constructs which are more sophisticated concepts.  
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

A preview of the dataset below.  

| id  | unit_price | p_id | amount     | country | status |
|-----|------------|------|------------|---------|--------|
| 325 | 30.342365  | 4    | 62.734691  | a       | 1      |
| 457 | 69.475791  | 5    | 20.922939  | c       | 0      |
| 351 | 30.164137  | 4    | 73.612906  | b       | 1      |
| 224 | 2.851734   | 1    | 207.205554 | c       | 1      |
| 123 | 39.875412  | 4    | 7.842334   | b       | 0      |

The basic mechanics of the [code that generates the data](https://www.testingbranch.com/src_model_simulation/).  
 
Some plots that show how the target varies with the 5 simulated products and the 3 simulated countries. There is a division on the ratio of the offered unit price and the base price: increasing the simulation noise will make this division less clear and overall, create a harder problem.  

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/country_product.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure> 

---

Let's then setup a simple model to study converted opportunities. This is not meant to ideally model the data, it's just a basic object to generate simulations.  

I'll use pymc3 to implement the bayesian form of a logistic regression. If some aspect behind the model definition escapes you, refer to their [examples and docs](https://docs.pymc.io/).   
The pricing figures are normalized by the base pricing of each product; essentially a transformation that scales the figures and makes them close to zero (naturally easy to assign prior distributions to).  

Our model will have a linear terms for products and for countries in addition to a common intercept; it will use a logit as a link function to generate probabilities. These probabilities are used to generate a Binomial distribution that model our observations.  

Because we know that the unit price is the most important factor here, let's set a prior distribution for a multiplicative parameter, which is free to reach larger values easily.    

The overall formula for the model:  
y = intercept + intercept_prod + alpha_prod * price + intercept_country + alpha_country * price  
prob = inverse_logit(y)  
observations ~ Binomial(p=prob)  

      
      N=len(train_status)
      dim1 = len(set(product_id))
      dim2 = len(set(country))  

      with pm.Model() as shared_data_model: 

          intercept = pm.Normal('intercept', mu=0, sd=1)  

          alpha_product = pm.Normal('alpha_product', mu=0, sd=1, shape=dim1)
          alpha_country = pm.Normal('alpha_country', mu=0, sd=1, shape=dim2) 

          sigma_beta = 10
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

This model is simple enough for this data, so there's no divergences or anything that raises any red flags.  

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/traceplot.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

Let's proceed.  
For simple models such as this, even weaker priors would probably be informative enough. Adding terms for other attributes, like industry or some time component will make it more complex and harder to sample.  
In cases where noise is significant and our observations are not providing a clear signal for the model to pick up, encoding knowledge in priors helps the sampler significantly.  


Sampling from the posterior, we can see the separation in the conversion of opportunities by the pricing is clear.   
We can observe the highest posterior density regions and how well it separates the normalized price. Other transformations, like zscoring the price by product, presented cleaner regions, but since the performance of the model was identical, having the price presented as it is, was more convenient for the simulations — the focus of the post.  

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/train_posterior.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

The key to take from the model, is that if probabilities are converted to outcomes, the predictive performance of the model is good.  

Below we can observe the predictions of an hold-out set and the uncertainty (the standard deviation of the posterior predictions) of each prediction. This is will be helpfull to understand how much trust can be deposited in each prediction.  
Notice that the standard deviation for a Binomial distribution is bounded at 0.5. Anything greater would make probability pend towards the other outcome.

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/simul_prob_var_circle1.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

In addition to the posterior spread in our predictions, we can also assess uncertainty in these models by investigating the other posterior distributions that composed the model.  
Listing the standard deviations of the posteriors is an easy way to quantify why some predictions, because they're modelled by wider curves, will have inherently more uncertainty associated.  

---

Linear models extrapolate well, or at least better than some classes of models, but of course, these extrapolations assume a linear relation.  
This is not realistic for all cases, of course — we can imagine that there are strong non-linear relations if unit price get close to zero, and also when they get several times higher than the base price.  


If we wanted to answer the question of what discount to apply to an offer to have it accepted, in this models, it's simply a matter of sampling from the posterior with a different price value.  
In the plot below we can see a range of discounts that would convert previously declined offers into conversions. Quite interesting! Ideally a sales rep would like to see large spikes in won opportunities without giving large discounts.  

Below we can see the evolution of conversions with discounts and the color represents the mean of a measure of uncertainty (std dev of the posterior) of all previously declined offers.  
The smaller prices will affect the outcome of the logit model, and therefore the probability (which as seen above, has a direct relation to the uncertainty). The shape of the posterior on the other hand is fixed. To put it in other words, some countries or products, because they have a lower signal-to-noise ratio, will always be more uncertain.    

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/discount.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

The key point that we can take from the simulations is that adding a 20% discount on top of the previous offer will gain all of the opportunities. More than that is essentially losing money.  


The same exercise can be executed to assess ideal increases to unit prices and analyze the tradeoff between revenue and declined offers in a principled manner.  
Here we can see the amount of offers lost as we keep raising the prices — sales reps could use this to increase prices just below what would lose an offer, or to maximize profit (if you're able to sell for 3x the base price, less business could be acceptable).    

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/mark-up.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

The simulation shows that we could, based on the model, increase the price dramatically, until we lose all opportunities.  
Both of these simulations seem to agree with our knowledge of the problem.

---

This post hopefully helped illustrate how we can use models to assist in simulating scenarios.  
More complex models will bring very interesting simulations, and optimizing these parameter landscapes will become a less trivial exercise.  

[Check the code and adjust noise parameters to explore different scenarios](https://www.testingbranch.com/src_model_simulation/)
