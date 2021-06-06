---
layout: single
permalink: /src_model_simulation/
title: "src_model_simulation"
subscribe: true
--- 


```
quantity_discount = SortedDict({0: 0,
                                10: 0.05, 
                                20: 0.10, 
                                40: 0.20, 
                                80:0.30, 
                                160: 0.40
                               })

product_std_price = {
                    1: 5,
                    2: 10,
                    3: 20,
                    4: 40,
                    5: 80    
                    }

country_uncertainty = {'a':0.10, 'b':0.05, 'c':0.01} 
country_ratio = ['a']*5 + ['b']*30 + ['c']*65

product_uncertainty = {1:0.10, 2:0.08, 3:0.07, 4:0.01, 5:0.0} 
product_ratio = [1]*15 + [2]*5 + [3]*5 + [4]*50 + [5]*25 


def invlogit(x):
    return np.exp(x) / (1 + np.exp(x))  


def discounted_price(p_id, quantity): 
    for key in quantity_discount:
        if key > quantity: 
            continue
        else: 
            discount = quantity_discount[key]
    unknown_component = random.random()*0.05 # additinal discount,... things that are not contained in data
    return product_std_price[p_id] * (1 - discount) - product_std_price[p_id]*unknown_component


def determine_success(p_id, unit_price, country, noise):
    ratio = unit_price/ product_std_price[p_id]  
    score = invlogit(ratio*3 - 2) - country_uncertainty[country] - product_uncertainty[p_id]
    if score < 0.5 + noise*random.random():
        return 1
    else: 
        return 0

    
def generate_opportunity(id_num, noise=0.15):
    country = random.choice(country_ratio) 
    p_id = random.choice(product_ratio)
    amount = random.expovariate(0.01)
    
    unit_price = discounted_price(p_id, amount)
    status = determine_success(p_id, unit_price, country, noise)
    
    return [id_num, unit_price, p_id, amount, country, status]  


N=500
opportunities = list()
for i in range(N):
    opp = generate_opportunity(i, 0.15)
    opportunities.append(opp)

opps = pd.DataFrame(opportunities)
opps.columns = ['id', 'unit_price', 'p_id', 'amount', 'country', 'status']
opps['p_cty'] = opps['p_id'].astype(str) + opps.country

print(sum(opps.status)/len(opps))


status = np.array(opps['status']) 
unit_price = np.array(opps['unit_price']) #euro  

labels_country, _ = pd.factorize(opps['country'], sort=True) 
country = np.array(labels_country)

labels_products, _ = pd.factorize(opps['p_id'], sort=True) 
product_id = np.array(labels_products)

labels_p_cty, _ = pd.factorize(opps['p_cty'], sort=True) 
p_cty = np.array(labels_p_cty)

normalized_offers = opps.groupby(['p_id']).unit_price.transform(lambda x : zscore(x, ddof=0))



N_test = int(len(opps)*0.2) 

def train_test(array, N_test=N_test):
    return array[N_test:,], array[:N_test,]

train_status, test_status = train_test(status)
train_product_id, test_product_id = train_test(product_id) 
train_country, test_country = train_test(country)  
train_p_cty, test_p_cty = train_test(p_cty)
train_normalized_offers, test_normalized_offers = train_test(normalized_offers)   


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


with shared_data_model:
    pp_y = pm.sample_posterior_predictive(trace)["y"]
print('Accuracy:', accuracy_score(train_status, np.where(pp_y.mean(0) > 0.5, 1, 0)))

plt.plot(train_normalized_offers, train_status, "k.", alpha=0.15)

plt.scatter(train_normalized_offers, pp_y.mean(0), s=1 )
az.plot_hdi(train_normalized_offers, pp_y, hdi_prob=0.6, fill_kwargs={"alpha": 0.5})
az.plot_hdi(train_normalized_offers, pp_y, fill_kwargs={"alpha": 0.2}) 


multiplier_lst = [i/1000 for i in range(1, 100) if i%3==0] + [i/100 for i in range(1, 300) if i%20==0]
won_opps_lst = list()
with tqdm(total=len(multiplier_lst)) as pbar:
    for multiplier in multiplier_lst:
        predictions = list()
        with shared_data_model:
            pm.set_data({"train_cty": test_country, "train_p": test_product_id, "train_p_cty": test_p_cty,"train_offers": test_normalized_offers*multiplier})
            pp_y_new = pm.sample_posterior_predictive(trace, 1000, progressbar=False) 
        
        won_opps_lst.append(sum(np.where(pp_y_new['y'].mean(0) > 0.5, 1, 0)))
        pbar.update(1)

plt.scatter(multiplier_lst , won_opps_lst )
plt.ylabel('won opportunities')
plt.xlabel('discount(0-1); mark-up(1-10)')
plt.axvline(1)  


```
