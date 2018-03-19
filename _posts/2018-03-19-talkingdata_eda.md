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

```text
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
```

## Variables

Looking at the columns, we have total of 8 variables: 

```text
[1] "ip"              "app"             "device"          "os"              "channel"        
[6] "click_time"      "attributed_time" "is_attributed"  
```

I am also curious on the total number of unique values each variables have in placed: 

```text
             ip             app          device              os         channel 
         277396             706            3475             800             202 
     click_time attributed_time   is_attributed 
         259620          182058               2 
```
             
Let us take into account what kaggle has posted:  


```text 
Each row of the training data contains a click record, with the following features.

* ip: ip address of click.
* app: app id for marketing.
* device: device type id of user mobile phone (e.g., iphone 6 plus, iphone 7, huawei mate 7, etc.)
* os: os version id of user mobile phone
* channel: channel id of mobile ad publisher
* click_time: timestamp of click (UTC)
* attributed_time: if user download the app for after clicking an ad, this is the time of the app download
* is_attributed: the target that is to be predicted, indicating the app was downloaded

Note that ip, app, device, os, and channel are encoded
```


## Missing Data 

This is a good data set since most / all of the variable do not seem to have NA values.

```text 
                       variable count
ip                           ip     0
app                         app     0
device                   device     0
os                           os     0
channel                 channel     0
click_time           click_time     0
attributed_time attributed_time     0
is_attributed     is_attributed     0
```

Let us also check from blanks; based on the initial glimpse of the data, we can directly check that attributed_time contains lots of empty entries, total of `r  (184447044 / nrow(df)) *100` %. We can definitely drop this variable off.  


