---
title: 'Blog Post 2: The Economy'
author: Alex Heuss
date: '2024-09-13'
slug: blog-post-2-the-economy
categories: []
tags: []
---




## The Influence of the Economy on Elections

[Discussion of the predictive power of the fundamentals and the economy - could mention the bread and peace model]. Especially talk about Q2 econ power.






```
## Warning: Using `size` aesthetic for lines was deprecated in ggplot2 3.4.0.
## ℹ Please use `linewidth` instead.
## This warning is displayed once every 8 hours.
## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
## generated.
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

We can see that the correlations between Q2 GDP growth and the incumbent party's popular vote share are very different depending on whether or not 2020 is included. Brief analysis about whether either correlation is actually strong. 

```
## [1] 0.4336956
```

```
## [1] 0.569918
```
Let's take a look at the linear regression results: 

```
## 
## Call:
## lm(formula = pv2p ~ GDP_growth_quarterly, data = incumbent_econ_data)
## 
## Coefficients:
##          (Intercept)  GDP_growth_quarterly  
##              51.2580                0.2739
```

```
## 
## Call:
## lm(formula = pv2p ~ GDP_growth_quarterly, data = incumbent_econ_data_no2020)
## 
## Coefficients:
##          (Intercept)  GDP_growth_quarterly  
##              49.3751                0.7366
```
We can interpret these results to mean that for each percentage change in Q2 GDP growth, the popular vote for the incumbent party would grow by 0.27 percentage points when looking at all data from 1948-2020, or by 0.74 percentage points when 2020 is excluded. In close elections, that approximately 0.5 percentage point difference between the two models can make a big difference. 

All that said, I also want to highlight one stark trend in the data. Let's look at the graph from 1948-2020 again:



<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" />

## Economic Influence at the State Level


``` r
# State-level data wrangling, historical trends, also just 2000s, correlations between available state economic data to consider multi-variable approach
```

## Testing our Models


``` r
#summary statistics and model checking for both national and state models
```









