---
title: "Exploratory Analysis of Several Datasets"
excerpt: "Describes several reports of different exploratory data analysis."
header:
  teaser: exploratory.png
---

This page gathers several exploratory data analysis and their respective reports created using R Markdown.

Currently we describe three main data analysis:

1. Analysis and Modeling of Breast Cancer Data
2. Time Series Analysis of Milk Production
3. Exploratory Analysis of Auto Data

As other explorations became available, this page will be updated.

---

## Analysis and Modeling of Breast Cancer Data

This first analysis uses a dataset containing information about breast cancer. The idea is to perform an exploratory analysis of the information contained in the dataset, figuring out ways of making the dataset tidier. The ultimate objective is to build and compare models to predict if a given tumor is benign or malignant (breast cancer).

The analysis show that, with a Random Forest model, we can predict if a given tumor is malignant with 97.86% of Accuracy. This result is 1.96% higher than the Accuracy of 95.90% reported in the UCI Machine Learning as the highest for this dataset. We also conclude that the most important information for this prediction is the ‘uniformity of the cell size’.

* Report: <a href="http://rpubs.com/ricardosc/breast-cancer" target='_blank' class="btn btn--info btn--small">Analysis and Modeling of Breast Cancer Data</a>

---

## Time Series Analysis of Milk Production

This work is intended to explain a Time Series analysis performed on a dataset containing information about Milk Production. The idea is to analyze trend and seasonality of the production of Milk from 1995 until 2013, decomposing the time series and analysing the remainder. After that we also create a model to forecast the production of 2014.

The analysis show that the time series is not stationary, as it has a trend, and that after removing trend and season efftects, the remainder of the decomposition is ARMA(1,0). The forecasting for 2014 showed good results with milk production data with confidence intervals reasonably small compared to the means.

* Report: <a href="http://rpubs.com/ricardosc/milk-timeseries" target='_blank' class="btn btn--info btn--small">Time Series Analysis of Milk Production</a>

---

## Exploratory Analysis of Auto Data

To explore a dataset containing information about cars, three reports were created. The idea is to show some findings regarding information related to the price of the cars. The reports go from data loading/cleaning, hypothesis testing, to some basic modeling for exploration. Some categorical variables of the dataset are extensively explored in the second report below.

* Report 1: <a href="http://rpubs.com/ricardosc/auto-hypothesis-testing" target='_blank' class="btn btn--info btn--small">Hypothesis Testing of Auto Data</a>
* Report 2: <a href="http://rpubs.com/ricardosc/auto-categorical-variables" target='_blank' class="btn btn--info btn--small">Analysis of Categorical Variables of Auto Data</a>
* Report 3: <a href="http://rpubs.com/ricardosc/auto-exploration" target='_blank' class="btn btn--info btn--small">Exploratory Analysis of Auto Data</a>

