---
layout: single
title: 'Kaggle: Talkingdata Exploratory Data Analysis'
category: eda
theme: cosmo
tags: [kaggle, R, notebook, exploratory, data, analysis, eda ]
comments: true
---

Before jumping straight into the competition, let us understand the what we are given!

<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>


<center><img src="https://kaggle2.blob.core.windows.net/competitions/kaggle/5340/logos/front_page.png"></center>


Kaggle recently launched a new competition, sponsored by talkingdata. Talkingdata is based in China, 

> TalkingData, China’s largest independent big data service platform, covers over 70% of active mobile devices nationwide.

For this competition, we are tasked with a creating a classification model, to predict if the users will download the app if they are to click on the mobile app ad. I have decided to share the EDA that I will be first doing before jumping into the modelling process. 

# Table of Contents

* [Data Exploratory](#data-exploratory)
    + [Basic look of Dataset](#basic-look-of-dataset)
    + [Variables](#variables)
    + [Missing Data](#missing-data)
* [Visualizations](#visualizations)
    + [Proportion of Target variable](#proportion-of-target-variable)
    + [Time-period](#time-period)
    + [Click Time](#click-time)
        - [Day](#day)
        - [Hourly](#hourly) 
    + [Parallel Set Charts](#parallel-set)
    + [Installation Rates](#installation-rates)
        - [By IP]()
        
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

Let us also check from blanks; based on the initial glimpse of the data, we can directly check that attributed_time contains lots of empty entries, total of **99,7 %.** We can definitely drop this variable off.  

# Visualizations


## Proportion of Target variable 

I believe one important concern we have would be the class distribution of the dataset, but how unbalance will this data set be? Seems like there is a case of severe imbalance of data.

<center><img src="/images/talkingdata_charts/chart1.png?style=centerme"></center>

## Time period 

We can see that the train data span across 4 days, as mentioned in kaggle's introduction of this competition: 

>
    To support your modeling, they have provided a generous dataset covering approximately 200 million clicks over 4 days!


Data collected takes place between 06/11 to 09/11. 

We can also see that the data span across every sec. 
So from the start of  "2017-11-06 14:32:21" till the end of "2017-11-09 16:00:00"

## Click time


### Day

Interestingly, 06/11 is a Monday. Does this mean that there is some form of Monday blues? Most of the 0s probably came from 06/11. 

<center><img src="/images/talkingdata_charts/chart2.png?style=centerme"></center>

### Hourly

Note that this data set is based in China, and time in China is **8 hours ahead**. Highest click time hovers around UTC 1-4 am.

UTC | China 
--- | ---
1 | 9am
2 | 10 am
3 | 11 am
4 | 12 am

next batch will be: 

UTC | China 
--- | ---
11 | 7pm
12 | 8pm
13 | 9pm

It seems that the popular timing (since the data set given is on weekdays) are during the morning as well as the night period. One hypothesis will be that people are surfing websites as they commute to work up till lunch break or back from work. 

<center><img src="/images/talkingdata_charts/chart3.png?style=centerme"></center>

## Parallel Set 

Let us first do a split, by filtering for groups (unique device-os-app-channel) that are more than 9 and also split the channels by colors so we can have a better visualization. We can see a huge proportion comes from channel 213, and they also installed app 19 as well as 29. Also, majority of these people use device 0. **Some naive hypothesis would be that, channel 213 seems to be where people found out about app 19 and 29. Also, could it be the device 0 version of this app is better done since most people who installed it are on device 0**

<center><img src="/images/talkingdata_charts/chart4.png?style=centerme"></center>

Filtering for the smaller groups, we can see:

* there are less device 0 users. Majority are using device 1,2...etc
* Again, people who installed app 19 comes from channel 213

<center><img src="/images/talkingdata_charts/chart5.png?style=centerme"></center>

## Installation Rates 


### By IP 

This is inspired by [CPMP](https://www.kaggle.com/cpmpml/ip-download-rates), which i think is very very insightful. So i decide to include this insight here as well. 


Let's compute the rate of installation by ip to see the average installation rate, from 0-1. 

```text 
# A tibble: 10 x 2
      ip installation_rate
   <int>             <dbl>
 1     1      0.1914893617
 2     5      0.0000000000
 3     6      0.0013755158
 4     9      0.0014892033
 5    10      0.0025423729
 6    19      0.0047281324
 7    20      0.0006699045
 8    25      0.0044843049
 9    27      0.0015977631
10    31      0.0028873917
``` 


Computing the rolling mean and plotting the moving average: I decide to alter the window to 10,000 to make the lines thinner.

<center><img src="/images/talkingdata_charts/rolling_1.png?style=centerme"></center>

Zooming in, let us identify the sudden spike of mean.

<center><img src="/images/talkingdata_charts/rolling_2.png?style=centerme"></center>

One more level of zoom, between 126400 to 126500, we can see a spike from the start of around ip 126400++

<center><img src="/images/talkingdata_charts/rolling_3.png?style=centerme"></center>
