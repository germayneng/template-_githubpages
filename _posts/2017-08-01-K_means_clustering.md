---
layout: single
title: 'K Means Clustering'
category: tutorial
tags: [r, machine, learning, unsupervised, kmeans ]
comments: true
---

Today, we will be exploring and discussing k means clustering.





K Means Clustering is a form of  unsupervised learning algorithm which cluster observations based on the variable similarity. 
Recall, when we talk about unsupervised learning, this means that unlike supervised learning, we are not defining an output given an input. Instead, the algorithm will find a pattern with the dataset and return the finding. In this case, the algorithm will attempt to group (cluster) datasets together.  


# How does it works? 

In k means clustering, we define the number of clusters we want the data to be grouped into. K clusters is the general form. 

Suppose we have n number of data points, and we define: 

$$
x_{i}
\\
i = 1,2... n
$$

Suppose in a simplified example, we define our clusters to be 2. The algorithm will assign 2 random centroids at random locations 

$$
c_{1} , c_{2} 
\\
general \ form : c_{k}
$$

<br>
<center><img src="/images/k_means_image/k_means_1.JPG?style=centerme"></center>
<br>

Now, we will begin each iteration until convergence/ within cluster variation (sum of euclidean distance between data points and its cluster centroids) cannot be reduced. 


* step 1: Reassign data points to the cluster whose centroid is closest. (For each point x, find the nearest centroid and assign that point to that centroid.)
* step 2: Calculate new centroid of each cluster. (For each cluster, compute new centroid value , which is a mean of all points x that was assigned in cluster in previous step)


What this means is that we will group the data points to the 2 clusters. The assignment will be based on for example, the nearest euclidean distance. 

$$
arg \ min \ D(x_{i},c_k)
$$



<br>
<center><img src="/images/k_means_image/k_means_2.JPG?style=centerme"></center>
<br>

And with that, we will have them group in the clusters. Now, we will begin step 2, to compute the new centroid based on the mean of the cluster. So now, we have 2 new centroids. 


<br>
<center><img src="/images/k_means_image/k_means_3.JPG?style=centerme"></center>
<br>


This will be repeated till  none of the cluster assignments change. The next iteration will begin repeating the 2 steps above, where we again, assign the data points to the new centroids and compute the new centroids again. 

<br>
<center><img src="images/k_means_image/k_means_4.JPG?style=centerme"></center>
<br>


Now that we have the basic concept 

# Load in libraries

```R
library(factoextra)
library(FactoMineR)
library(tidyverse)
```

# Example 1: Iris Data 

Let us load the data, 

```R
data("iris")
```

So, based on the original data set, you can see the distinct grouping.

```R
library(ggplot2)
ggplot(iris, aes(Petal.Length, Petal.Width, color = Species)) + geom_point()
```

<br>
<center><img src="/images/k_means_image/unnamed-chunk-3-1.png?style=centerme"></center>
<br>

So, will clustering techniques allow us to get the same grouping?

We know that there will be 3 groupings, so let us get kmeans to split into 3 clusters. Nstart denotes the number of iterations of starting assignments and return the lowest within cluster variation.
```R
set.seed(123)
iris_cluster <- kmeans(iris[1:4], 3, nstart = 20)
```

we can obtain:

* clusteroids (cluster means)
* cluster assignment 
* within cluster variation

{% highlight r %}
iris_cluster
{% endhighlight %}



{% highlight text %}
    ## K-means clustering with 3 clusters of sizes 50, 38, 62
    ## 
    ## Cluster means:
    ##   Sepal.Length Sepal.Width Petal.Length Petal.Width
    ## 1     5.006000    3.428000     1.462000    0.246000
    ## 2     6.850000    3.073684     5.742105    2.071053
    ## 3     5.901613    2.748387     4.393548    1.433871
    ## 
    ## Clustering vector:
    ##   [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1
    ##  [36] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 3 3 2 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3
    ##  [71] 3 3 3 3 3 3 3 2 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 3 2 3 2 2 2
    ## [106] 2 3 2 2 2 2 2 2 3 3 2 2 2 2 3 2 3 2 3 2 2 3 3 2 2 2 2 2 3 2 2 2 2 3 2
    ## [141] 2 2 3 2 2 2 3 2 2 3
    ## 
    ## Within cluster sum of squares by cluster:
    ## [1] 15.15100 23.87947 39.82097
    ##  (between_SS / total_SS =  88.4 %)
    ## 
    ## Available components:
    ## 
    ## [1] "cluster"      "centers"      "totss"        "withinss"    
    ## [5] "tot.withinss" "betweenss"    "size"         "iter"        
    ## [9] "ifault"
{% endhighlight %}



Let us plot the cluster grouping:

{% highlight r %}
iris_cluster$cluster <- as.factor(iris_cluster$cluster)
{% endhighlight %}

```R
ggplot(iris, aes(Petal.Length, Petal.Width, color = iris_cluster$cluster)) + geom_point()
```

<br>
<center><img src="/images/k_means_image/unnamed-chunk-7-1.png?style=centerme"></center>
<br>

```R
iris$species_cluster <- iris_cluster$cluster
```


```R
tbl_df(iris)
```

{% highlight text %}
    ## # A tibble: 150 x 6
    ##    Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ##           <dbl>       <dbl>        <dbl>       <dbl>  <fctr>
    ##  1          5.1         3.5          1.4         0.2  setosa
    ##  2          4.9         3.0          1.4         0.2  setosa
    ##  3          4.7         3.2          1.3         0.2  setosa
    ##  4          4.6         3.1          1.5         0.2  setosa
    ##  5          5.0         3.6          1.4         0.2  setosa
    ##  6          5.4         3.9          1.7         0.4  setosa
    ##  7          4.6         3.4          1.4         0.3  setosa
    ##  8          5.0         3.4          1.5         0.2  setosa
    ##  9          4.4         2.9          1.4         0.2  setosa
    ## 10          4.9         3.1          1.5         0.1  setosa
    ## # ... with 140 more rows, and 1 more variables: species_cluster <fctr>
{% endhighlight %}


# Example 2: using Facto packages 

```R
iris2 <- iris
iris2$species_cluster <- NULL
iris2$Species <- NULL
set.seed(123)
iris_cluster_facto <- kmeans(scale(iris[1:4]), 3, nstart = 20)
fviz_cluster(iris_cluster_facto, data = scale(iris2),
             palette = c("#00AFBB","#2E9FDF", "#E7B800"),
             ggtheme = theme_minimal(),
             main = "Just another k-means cluster")
```


<br>
<center><img src="/images/k_means_image/unnamed-chunk-10-1.png?style=centerme"></center>
<br>

# US Arrest dataset 


```R
data("USArrests")
df <- scale(USArrests)
set.seed(123)
km.res <- kmeans(scale(USArrests), 4, nstart = 25)
km.res

group.colors <- c("#00AFBB","#2E9FDF", "#E7B800", "#FC4E07")
USArrests$group <- as.factor(km.res$cluster)

ggplot(USArrests, aes(Murder, Assault, color = USArrests$group) ) + geom_point() 
```
   >
    ## K-means clustering with 4 clusters of sizes 13, 16, 13, 8
    ## 
    ## Cluster means:
    ##       Murder    Assault   UrbanPop        Rape
    ## 1 -0.9615407 -1.1066010 -0.9301069 -0.96676331
    ## 2 -0.4894375 -0.3826001  0.5758298 -0.26165379
    ## 3  0.6950701  1.0394414  0.7226370  1.27693964
    ## 4  1.4118898  0.8743346 -0.8145211  0.01927104
    ## 
    ## Clustering vector:
    ##        Alabama         Alaska        Arizona       Arkansas     California 
    ##              4              3              3              4              3 
    ##       Colorado    Connecticut       Delaware        Florida        Georgia 
    ##              3              2              2              3              4 
    ##         Hawaii          Idaho       Illinois        Indiana           Iowa 
    ##              2              1              3              2              1 
    ##         Kansas       Kentucky      Louisiana          Maine       Maryland 
    ##              2              1              4              1              3 
    ##  Massachusetts       Michigan      Minnesota    Mississippi       Missouri 
    ##              2              3              1              4              3 
    ##        Montana       Nebraska         Nevada  New Hampshire     New Jersey 
    ##              1              1              3              1              2 
    ##     New Mexico       New York North Carolina   North Dakota           Ohio 
    ##              3              3              4              1              2 
    ##       Oklahoma         Oregon   Pennsylvania   Rhode Island South Carolina 
    ##              2              2              2              2              4 
    ##   South Dakota      Tennessee          Texas           Utah        Vermont 
    ##              1              4              3              2              1 
    ##       Virginia     Washington  West Virginia      Wisconsin        Wyoming 
    ##              2              2              1              1              2 
    ## 
    ## Within cluster sum of squares by cluster:
    ## [1] 11.952463 16.212213 19.922437  8.316061
    ##  (between_SS / total_SS =  71.2 %)
    ## 
    ## Available components:
    ## 
    ## [1] "cluster"      "centers"      "totss"        "withinss"    
    ## [5] "tot.withinss" "betweenss"    "size"         "iter"        
    ## [9] "ifault"



<br>
<center><img src="/images/k_means_image/unnamed-chunk-11-1.png?style=centerme"></center>
<br>

```R

library("factoextra")
fviz_cluster(km.res, data = df,
             palette = c("#00AFBB","#2E9FDF", "#E7B800", "#FC4E07"),
             ggtheme = theme_minimal(),
             main = "Partitioning Clustering Plot"
             )
```


<br>
<center><img src="/images/k_means_image/unnamed-chunk-12-1.png?style=centerme"></center>
<br>


# Pros and Cons 


## Pros 

* Very efficient. 

$$
O(no.iteration * no.clusters * no.instances * no.data \ dimensions)
$$

* Make use of all the data 

## Cons 

* Prone to outliers

* Cannot have categorical variables (since we are computing means, must be numerical)


# References 

<br>
[Credit to Victor Lavrenko for the images](https://www.youtube.com/watch?v=_aWzGGNrcic)





