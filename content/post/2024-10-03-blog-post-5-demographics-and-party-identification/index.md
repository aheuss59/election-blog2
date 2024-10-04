---
title: 'Blog Post 5: Demographics and Party Identification'
author: Alex Heuss
date: '2024-10-03'
slug: blog-post-5-demographics-and-party-identification
categories: []
tags: []
---


``` r
library(tidyverse)
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.4     ✔ readr     2.1.5
## ✔ forcats   1.0.0     ✔ stringr   1.5.1
## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
## ✔ purrr     1.0.2     
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

## Discussion of the Predicitive Power of Demographics and Party ID

In class this week, we discussed the power of demographic variables in predicting election outcomes. The paper we read this week, la la la la la, provided some empirical evidence that demographic data can predict vote choice with an accuracy of approximately 63%

## Thinking About Party ID

Historical data on state-level partisan identification is not readily available. National-level party identification data can be compiled through Pew Research Center data (1939-2014). [find through 2024]. 

State-level data however is not as easily obtained




```
## Warning: Removed 2 rows containing non-finite outside the scale range
## (`stat_smooth()`).
```

```
## Warning: Removed 2 rows containing missing values or values outside the scale range
## (`geom_point()`).
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />



``` r
# Ask about different methods of estimating Party-ID for each state
# we can use the voter files for 2024
# you can try to look for a historical data set for party
# to weight party ID you can train a model only on party ID and then use ensembling
# super learning would helo make weights that empirically are better worse
```

## Building a State-Level Model and Explaining Decisions and Assumptions


``` r
# Ask about a proper format
```


``` r
# Ask about value imputation and what assumptions follow when we impute values
# state's historical deviation from national popular vote or from total outcome
# could create a separate model for states without polling
```


``` r
# Does it make sense to actually run each state's regression model separately or does that reduce the statistical power of results too much? 
# When I use random forest, does that actually make a model that I could then hypothetically use to bootstrap a bunch of election simulations
# A lot of my theory revolves around weighting partisan ID really high, how exactly can I incorporate that into the model?
# Is there anyway to make it so that when it predicts Dems and Reps it won't be more than 100 or should I re-weight based on percentage (ex. Harris at 52 and Trump at 50, then Harris % of pop vote is 52/102)

# People usually do simulationd for values of the polls
# the bootstrap in gov51 is different than what we do here
```
