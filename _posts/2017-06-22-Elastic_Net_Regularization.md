---
layout: single
title: 'Elastic net, LASSO and ridge'
category: tutorial
tags: [r, machine, learning, penalized, regression ]
comments: true
---

Elastic net, marriage of statistics and machine learning 

<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>


# "if you are using regression without regularization, you have to be very special!" - Owen Zhang, NYC data science academy 

## 

Penalized regression helps to deal with 2 major issue in regression: feature selection and multi collinearity. It helps to prevent overfitting and give a model that fits the training data less well as compared to OLS but able to capture the generalization better and less sensitive to variation from outliers.
Elastic net is a general form of ridge and lasso. Think of it as a combination of both.
Recall in usual regression, we make use of OLS -  minimizing the sum of squares of the difference between actual and predicted values. 
<br>
<br>
Assuming we have M number of features and N number of data points:

$$
RSS(\beta) = \sum_{j = 1}^N ( \hat{y_j} - y_j)^2 
\\
\hat{y_j} = \sum_{i = 1}^M \Big(    B_i * x_{ij} \Big)
\\
\\
\therefore RSS(\beta) = \sum_{j = 1}^N \Big( \sum_{i = 1}^M \Big(    B_i * x_{ij} \Big) - y \Big)^2
$$

Whereas the elastic net regularization estimate process will minize the sum of squares and a penalty based on the size of the estimated coefficient. We call this penalties the L1 / L2 Norm  

The hyperparameter lambda controls the weight of the penalty. The optimal value of alpha and lambda is obtained using a grid search method for the best cv value (k-fold cv)



## Ridge regression

* Ridge helps to deal with the instability of estimates of coefficient of linear models when they are collinear.
* Coefficients of unimportant features will shrink to **near zero**  
* Hyperparameter alpha = 0 
* Minimize the objective (RSS + L2 regularization)
* As lambda increases, RSS increases and model complexity decreases


$$
objective =  RSS (\beta) + \lambda \sum_{i = 1}^{M} \beta_i ^2 
$$ 


## Lasso regression 

* Lasso perform feature selection that forces coefficents for some variables to be zero.
* Hyperparamter alpha = 1
* Minimize the objective (RSS + L1 Norm)
* As lambda increases, RSS increases and model complexity decreases 
* Note that LASSO will remove variables (giving coefficient 0) so as lambda increases, expect high sparsity.

$$objective = RSS (\beta) + \lambda \sum_{i = 1}^{M} | \beta_i | $$ 





Theoritically, if lambda = 0, then it will be minimizing only the RSS and this will be the regular regression that we know. However, as pointed out by [peter](http://ellisp.github.io/blog/2016/08/13/fitbit-lasso), the result output by `glmnet` will be different due to numerical calculation issues.






## Elastic Net 

Combining both concept together, gives us the elastic net regualrization. (2005)


$$ objective = RSS (\beta) + \lambda \Bigg[ (1-\alpha) \sum_{i = 1}^{M} \beta_i ^2 +  (\alpha)\sum_{i = 1}^{M} | \beta_i |  \Bigg] $$ 










# References 
[http://ellisp.github.io/blog/2016/08/13/fitbit-lasso]()
<br> 
