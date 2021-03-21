---
title: Comparing high and low variance models with noisy data  
excerpt: "Exploration on the performance of machine learning models learning when predicting from noisy data. How gradient boosted machines compare with linear regression and other low variance models"
header:
  image: /assets/images/hyperparam_sampling/header.jpg  
tags:
    - machine learning 
share: true
subscribe: true
comments: true
--- 


This post is an exploration based on this [quora answer](https://www.quora.com/What-are-the-advantages-of-logistic-regression-over-decision-trees-Are-there-any-cases-where-its-better-to-use-logistic-regression-instead-of-decision-trees/answer/Claudia-Perlich?ch=10&share=ef233af4&srid=28C3J) by Claudia Perlich. The post will try to explore a but further in what circumstances some low variance models outperform high variance models.  

[experiment setup]


[conclusions]  

```YAML
---
title: "Splash Page"
layout: splash
permalink: /splash-page/
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/splash/coffee.jpeg
  actions:
    - label: "Download"
      url: "#test-link"
excerpt: "Bacon ipsum dolor sit amet salami ham hock ham, hamburger corned beef short ribs kielbasa biltong t-bone drumstick tri-tip tail sirloin pork chop."
---
```





```python
def firstUniqChar(: str) -> int:     
    for i in range(len(s)-1):
        unique = True
        for j in range(i+1, len(s)):
          # loop through all other characters
          # if character is no match for all of them we found a unique one
          # if character does match, not unique, continue with next
          # print(f"Comparing {s[i]} with {s[j]} ")
          if s[i] == s[j]:
            unique = False
        if unique == True:
          return i
      # No unique chars found
    return -1 
```


