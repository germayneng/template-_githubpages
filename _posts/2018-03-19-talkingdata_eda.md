---
layout: single
title: 'Kaggle: Talkingdata Exploratory Data Analysis'
category: eda
tags: [kaggle, R, notebook, exploratory, data, analysis, eda ]
comments: true
---

Before jumping straight into the competition, let us dwell into the data using EDA!

<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>


<center><img src="https://kaggle2.blob.core.windows.net/competitions/kaggle/5340/logos/front_page.png"></center>


Kaggle recently launched a new competition, sponsored by talkingdata. Talkingdata is based in China, 

> TalkingData, China’s largest independent big data service platform, covers over 70% of active mobile devices nationwide.

For this competition, we are tasked with a creating a classification model, to predict if the users will download the app if they are to click on the mobile app ad. I have decided to share the EDA that I will be first doing before jumping into the modelling process. 

# Data Exploratory 

## Basic look of Dataset 

>
       ip app device os channel          click_time attributed_time
1:  83230   3      1 13     379 2017-11-06 14:32:21                
2:  17357   3      1 19     379 2017-11-06 14:33:34                
3:  35810   3      1 13     379 2017-11-06 14:34:12                
4:  45745  14      1 13     478 2017-11-06 14:34:52                
5: 161007   3      1 13     379 2017-11-06 14:35:08                
6:  18787   3      1 16     379 2017-11-06 14:36:26                
   is_attributed
1:             0
2:             0
3:             0
4:             0
5:             0
6:             0


