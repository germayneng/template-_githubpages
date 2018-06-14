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
    + [Download Rates](#download-rates)
        - [By IP](#by-ip)
        
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

This makes sense because:

1. attributed_time follows is_attributed == 1
2. Knowing that we have heavy class imbalance (which we will see later), largely will be missing (blanks)


Checking the number of blanks in `attributed_time` leads to: 

```text 
[1] 184447044
``` 

<br>

---

<br>

# Visualizations


## Proportion of Target variable 

I believe one important concern we have would be the class distribution of the dataset, but how unbalance will this data set be? Seems like there is a case of severe imbalance of data.

<center><img src="/images/talkingdata_charts/chart1.png?style=centerme"></center>



<br>

---

<br>

## Proportion of variables 


### App

From the dataset, we can see the top 10 most popular app are as follows, regardless if there are downloaded or not. Popularity of app could be due to the channel since we are not considering if there are downloaded.

Comparing the 2 charts, we can see that there are some differences between the 2. For example, app3 is being clicked on the most, but yet not the top app when it comes to number of downloads. In fact, none of the top 10 apps clicked except 3 and 9 appears in the top 10 most downloaded app list.

Some naive hypthosis would be that perhaps the channels that the other apps are in, contains heavy traffic but not apps that people would like? Or perhaps these apps frequently pop up (and users just cancelled them?)

Regardless, something holds: **that is the total number of app clicked does not correlate to whether an app will be downloaded**. (If you want your app to be downloaded, spamming people does not mean that you will get more downloads)

Let us verify this later with a correlation plot.


<center><img src="/images/talkingdata_charts/pov_app_1.png?style=centerme"></center>

### IP 

It seems like naively, the higher the ip click count, the more apps downloaded from the particular IP address, except for some IPs which may be spamming. There could be some pattern between click count and possibility of download from a particular IP. As such, **we may be able to use this information for modelling. Maybe something like - historical number of clicks from IP?**

<center><img src="/images/talkingdata_charts/pov_ip_1.png?style=centerme"></center>

<br>

---

<br>

## Time period 

We can see that the train data span across 4 days, as mentioned in kaggle's introduction of this competition: 

>
    To support your modeling, they have provided a generous dataset covering approximately 200 million clicks over 4 days!


Data collected takes place between 06/11 to 09/11. 

We can also see that the data span across every sec. 
So from the start of  "2017-11-06 14:32:21" till the end of "2017-11-09 16:00:00"

<br>

---

<br>

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


<br>

---

<br>

## Parallel Set 

Let us first do a split, by filtering for groups (unique device-os-app-channel) that are more than 9 and also split the channels by colors so we can have a better visualization. We can see a huge proportion comes from channel 213, and they also download app 19 as well as 29. Also, majority of these people use device 0. **Some naive hypothesis would be that, channel 213 seems to be where people found out about app 19 and 29. Also, could it be the device 0 version of this app is better done since most people who downloaded them are on device 0**

<center><img src="/images/talkingdata_charts/chart4.png?style=centerme"></center>

Filtering for the smaller groups, we can see:

* there are less device 0 users. Majority are using device 1,2...etc
* Again, people who downloaded app 19 comes from channel 213

<center><img src="/images/talkingdata_charts/chart5.png?style=centerme"></center>


<br>

---

<br>

## Download Rates 


### By IP 

This is inspired by [CPMP](https://www.kaggle.com/cpmpml/ip-download-rates), which i think is very very insightful. So i decide to include this insight here as well. 


Let's compute the rate of Download by ip to see the average download rate, from 0-1. 

```text 
# A tibble: 10 x 2
      ip download_rate
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

<center><img src="/images/talkingdata_charts/rolling_main.png?style=centerme"></center>

Zooming in, let us identify the sudden spike of mean.

<center><img src="/images/talkingdata_charts/rolling_2.png?style=centerme"></center>

One more level of zoom, between 126400 to 126500, we can see a spike from the start of around ip 126400++

<center><img src="/images/talkingdata_charts/rolling_3.png?style=centerme"></center>

Comparing to the test set (Thank you CPMP, as well as [Julia](https://www.kaggle.com/yuliagm/be-careful-about-ips-as-a-signal/comments#latest-301610))
we can see that most of the test ip belong to < 126413

Here is the printed result of the tail of the test set arranged by ip:

```text
         click_id     ip app device os channel          click_time
18790460 18453009 126411  18      1  8     265 2017-11-10 14:53:19
18790461 18453172 126411   2      1  8     237 2017-11-10 14:53:19
18790462 18453284 126411  11      1  8     137 2017-11-10 14:53:20
18790463 18453492 126411  12      1  8     259 2017-11-10 14:53:20
18790464  1653413 126412  18      1 16     379 2017-11-10 04:29:05
18790465  6553650 126412  12      1 13     265 2017-11-10 09:06:43
18790466  7640395 126412  12      1 13     105 2017-11-10 09:28:49
18790467 17991861 126412  29      2 19     210 2017-11-10 14:44:28
18790468 16820930 126413  19    168  0     282 2017-11-10 14:23:18
18790469 16922809 126413  19    168  0     282 2017-11-10 14:25:03
```
Knowing this, it seems that training from the train set, the is_attributed is at the lower end for ips in test set.

<center><img src="/images/talkingdata_charts/rolling_4.png?style=centerme"></center>
