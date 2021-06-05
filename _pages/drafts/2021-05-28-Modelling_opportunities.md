---
title: Bayesian based simulations  
excerpt: "Bayesian decision making applied to sales opportunities"
permalink: /drafts/bayesian_simulation/
header:
  overlay_image: /assets/images/outliers_ts/header.jpg 
tags:
    -  bayesian modelling
share: true
subscribe: true
comments: true
--- 



Let's cover some of the strong points when using bayesian models to make predictions and simulate scenarios in a structured manner.  
The ability that linear models provide to model noisy problems is one of the features I like. Using bayesian priors to inject domain knowledge in a model proves to be instrumental when observations alone may not be sufficient to determine driving factors in what we want to study.  

 
---

One study that seemed particularly suited to draw some of these conclusions was the modelling of what affects the success of sales opportunities.  
Some variations can be justified with different attributes (regions, industry, products,...), but the thing that determines whether or not an opportunity is converted to a sale is the price per unit. Of course additional factors such as competitor pricing would be very relevant, but quite hard to access.  
Because we understand what is being study so well, and we understand the impact of pricing, it's an ideal case to model, and an ideal model to manipulate in order to reach optimal scenarios.  

---

Let's set up a simulated dataset that resembles sales opportunities let's have the status of those opportunities depend on the price of these products and their relation to specific groups - in particular products and countries. In addition some random effects were also added to represent information contained outside of the data - competitor pricing, payment terms and other factors that might have an impact.  

The basic idea is that we have a base price for each product, and based on the amount ordered, there will be quantity discounts. In addition, each country and each product might have promotions (relatively small magnitude effects) which don't interact with each other.  
The ratio between the discounted unit price and the base price is the major force in the conversion mechanism in our simulated data.  

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

Let's use a linear model to study converted opportunities; let's use pymc3 to implement the bayesian form of a logistic regression.  
Our model will have a linear terms for products and countries and it will use the logit as a link function to generate probabilities. These probabilities are used in a Binomial distribution to generate the posterior distribution.  
Because we know that the unit price is the most important factor here, let's have a prior distribution that is free to explore the parameter space more readily.  
All attributes are marginalized - we have essentially one model per combination of product and country, with shared intercepts. This is more performant and in the end accurate, because we can still use NUTS. Using gibbs sampler to sample from discrete variables is possible, but is not fast and it can result in completely inaccurate posteriors.  

y = intercept + intercept_prod + alpha_prod * price + intercept_country + alpha_country * price  
prob = logit^-1(y)  
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

For simple models such as this, even weaker priors would probably be informative enough. Adding terms for other attributes, like industry or period, will make it more complex, and harder to sample. Also, in cases where noise is significant and our observations are not providing a clear signal for the model to pick up, encoding knowledge in priors helps the sampler significantly.  

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/posterior_predictive.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/test_posterior.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>
---

Linear models extrapolate better, but of course, the extrapolations follow a linear relation. This is not realistic of course - we can imagine that there are strong non-linear relations if unit price get close to nothing, and also when they get several times higher than the base price. That said, they're still helpful within the vicinities of the reasonable values.   


{% capture fig_img %}
![Foo]({{ "/assets/images/bayesian_simulation/simulation.png" | relative_url }})
{% endcapture %}
<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }} 
</figure>

