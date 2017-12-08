---
layout: single
title: 'Target Encoding'
category: tutorial
tags: [python, feature, engineering, machine, learning, R ]
comments: true
---


<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

I was first introduced to target encoding from the [Mercedes kaggle competition](). There were a few problems with some of the categorical variables. 

1. For variable $$ X_{i} $$, there are some categories that are present in the test set, which the train set does not have. 
2. Some categorical variables are so sparse (number of uniques) that traditional OHE methods does not seem that useful here. 

For 2, numerical mapping can be used to resolve the problem. Check out my custom package `dog encode` at my github. The label encoding function will work as such. If you are using python, sklearn.preprocessing has this label encoder that does the same (you can fit the transformation to both the train and test). 
The main drawback to this is that you will introduce an artifical ordinal ordering to these variables. 

Cat | label 
--- | ---
car | 2
dog | 1
cat | 3

As you can see, this gives the order that cat > car > dog. 

## The magic 

As such, there must be a better way to deal with this. There are many tricks that can handle this problem. But for today, let us talk about target encoding. Target encoding basically maps the target variable to each category. Mathematically, you can think of it as the probability of the target, conditional on the category. One context will be what is the probability that it is a 1 given you are a dog / car / cat. 

$$
P(Y | X_{i} ) 
$$ 

Target encoding is very strong. Because you can think of it as an classifier / estimator. And using it in a model is similar to stacking. As such, wrong implementation of it will result in heavy leakage. 

## Proper Implementation 

Since you are mapping your target variable onto your categorical variables, if you are not doing it correctly, you are basically leaking your target variable as your features. The consequences will be that you are predicting your target variable using your target variable. A recipe for disaster. 

As such, one method will be to include it as part of the cv fold during your modelling process. By encoding it this way, you are limiting the leakage from going onto the test set. You compute the target encoding using only the validation set. Also, notice that if you are including the target encoding with your cv fold, you are ensuring that **the cv fold is aligned with your target encoding fold**. If you think target encoding like a classifier, then it is stacking and hence, it is important to align the **cv folds** as you move from layer to layer to **minimize leakage**. (we will talk more about this in another article) 

Another way is to include random noise to cover the impact of leakage. In other words, this noise is a parameter you can tune for your "target encoding" classifier. 

