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

<link href="scripts/highlightjs/styles/github-gist.css" rel="stylesheet" />
<script src="scripts/highlightjs/highlight.pack.js"></script>

<!--<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.11.0/styles/default.min.css">-->
<!--<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.11.0/highlight.min.js"></script>-->

<script>
function highlightCode() {
    var pres = document.querySelectorAll("pre>code");
    for (var i = 0; i < pres.length; i++) {
        hljs.highlightBlock(pres[i]);
    }
}
highlightCode();
</script>

</body>
</html>
