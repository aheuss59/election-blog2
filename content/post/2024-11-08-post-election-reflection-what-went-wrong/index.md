---
title: "Post-Election Reflection: What Went Wrong?"
author: "Alex Heuss"
date: "2024-11-08"
output: pdf_document
categories: []
tags: []
slug: "post-election-reflection-what-went-wrong"
---




```
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
```

```
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
```

```
## Warning: Option grouped=FALSE enforced in cv.glmnet, since < 3 observations per
## fold
```

```
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
```

```
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
```

Since the election on November 5th, many Democrats across the country have been asking themselves one question: what happened? The presidential election was essentially over by 3:00 a.m. on November 6th, when the Associated Press formally called Pennsylvania for Trump, who now looks posed to win every swing state and the national popular vote. So what did happen? Here is an overview of how my model differed from the actual election results and why that might be. 

## A Refresher

In case you missed it, or in case you need a refresher, my model predicted a 270-268 Harris victory in the Electoral College and a 49% to 48% Harris victory for the national popular vote.

My national popular vote model used LASSO to select from a large number of potential predictive variables and ended up using a series of eight: percent of the country identifying as independent, the change in party identification for either party from the year preceding the election, vote share from the previous election, and five different weeks of polling, including the week just prior to the election.

I made two separate models for predicting the electoral college, one for states with significant polling aggregate data on FiveThirtyEight, and one for those without. Predictive variables for both models included: state-level lagged vote share for the two prior elections, whether the candidate is a member of the incumbent party, national Q2 GDP growth, average state-level unemployment, the change in partisan identification for either party from the last election, and state fixed effects. For states with polling aggregates, the mean polling average and latest polling average are included in my model.

Below is a breakdown of my predictions for each state. 


Table: (\#tab:print out prediction table)State Level Two-Party Predictions for Kamala Harris (%)

|State          | Lower Bound| Prediction| Upper Bound|
|:--------------|-----------:|----------:|-----------:|
|Alabama        |       25.22|      34.47|       43.71|
|Alaska         |       30.58|      39.83|       49.07|
|Arizona        |       44.58|      48.33|       52.08|
|Arkansas       |       25.99|      35.24|       44.48|
|California     |       57.18|      60.93|       64.68|
|Colorado       |       52.86|      56.61|       60.36|
|Connecticut    |       46.20|      55.44|       64.68|
|Delaware       |       45.75|      54.99|       64.24|
|Florida        |       41.86|      45.61|       49.36|
|Georgia        |       44.56|      48.31|       52.06|
|Hawaii         |       49.84|      59.08|       68.33|
|Idaho          |       19.00|      28.24|       37.48|
|Illinois       |       45.56|      54.80|       64.05|
|Indiana        |       29.33|      38.58|       47.82|
|Iowa           |       33.00|      42.24|       51.48|
|Kansas         |       28.71|      37.96|       47.20|
|Kentucky       |       23.01|      32.25|       41.49|
|Louisiana      |       29.83|      39.07|       48.32|
|Maine          |       51.92|      55.67|       59.42|
|Maryland       |       60.34|      64.09|       67.84|
|Massachusetts  |       60.21|      63.96|       67.71|
|Michigan       |       47.45|      51.20|       54.95|
|Minnesota      |       48.55|      52.30|       56.06|
|Mississippi    |       30.24|      39.48|       48.72|
|Missouri       |       39.49|      43.24|       46.99|
|Montana        |       35.28|      39.03|       42.78|
|Nebraska       |       34.25|      38.00|       41.75|
|Nevada         |       45.25|      49.00|       52.75|
|New Hampshire  |       47.74|      51.49|       55.24|
|New Jersey     |       44.70|      53.94|       63.19|
|New Mexico     |       48.84|      52.59|       56.35|
|New York       |       52.89|      56.64|       60.40|
|North Carolina |       43.28|      47.03|       50.78|
|North Dakota   |       17.60|      26.85|       36.09|
|Ohio           |       41.05|      44.80|       48.55|
|Oklahoma       |       20.31|      29.55|       38.79|
|Oregon         |       42.64|      51.88|       61.12|
|Pennsylvania   |       46.41|      50.16|       53.91|
|Rhode Island   |       48.15|      57.39|       66.64|
|South Carolina |       31.66|      40.90|       50.15|
|South Dakota   |       19.37|      28.61|       37.86|
|Tennessee      |       27.13|      36.37|       45.61|
|Texas          |       41.22|      44.97|       48.72|
|Utah           |       23.29|      32.54|       41.78|
|Vermont        |       49.58|      58.82|       68.07|
|Virginia       |       48.19|      51.94|       55.69|
|Washington     |       53.97|      57.72|       61.47|
|West Virginia  |       21.25|      30.49|       39.74|
|Wisconsin      |       46.82|      50.57|       54.32|
|Wyoming        |       15.13|      24.37|       33.61|

## Assessment of Accuracy


```
## New names:
## Rows: 52 Columns: 42
## ── Column specification
## ──────────────────────────────────────────────────────── Delimiter: "," chr
## (42): FIPS, Geographic Name, Geographic Subtype, Total Vote, Kamala D. H...
## ℹ Use `spec()` to retrieve the full column specification for this data. ℹ
## Specify the column types or set `show_col_types = FALSE` to quiet this message.
## • `0` -> `0...31`
## • `0` -> `0...32`
## • `0` -> `0...33`
## • `0` -> `0...34`
## • `0` -> `0...35`
## • `0` -> `0...36`
## • `0` -> `0...37`
## • `0` -> `0...38`
## • `0` -> `0...39`
## • `0` -> `0...40`
## • `0` -> `0...41`
## • `0` -> `0...42`
```

The confusion matrix below shows how my predictions played out. 


```
##       Prediction
## Actual DEM REP
##    DEM  19   0
##    REP   3  28
```

I correctly predicted 28 states to go to Trump and 19 to go to Harris. I only got three states wrong, which I predicted to go to Harris, but actually went to Trump. Unfortunately those states were the key swing states of Michigan, Pennsylvania and Wisconsin, which decided the outcome of the election.

Here's a further breakdown of every state, and it's prediction, true outcome, and error. Positive errors show an error in favor of Harris, and negative for Trump. 


|State          | Prediction| True Value| Error|
|:--------------|----------:|----------:|-----:|
|Vermont        |      58.82|      66.39| -7.56|
|Utah           |      32.54|      39.41| -6.87|
|South Dakota   |      28.61|      35.05| -6.44|
|Oregon         |      51.88|      57.30| -5.42|
|North Dakota   |      26.85|      31.28| -4.43|
|Kansas         |      37.96|      41.78| -3.82|
|Idaho          |      28.24|      31.24| -3.00|
|Oklahoma       |      29.55|      32.53| -2.98|
|Hawaii         |      59.08|      61.79| -2.71|
|Delaware       |      54.99|      57.48| -2.49|
|Alaska         |      39.83|      42.15| -2.32|
|Kentucky       |      32.25|      34.41| -2.16|
|Wyoming        |      24.37|      26.52| -2.15|
|Washington     |      57.72|      59.85| -2.13|
|Connecticut    |      55.44|      57.44| -2.00|
|Indiana        |      38.58|      40.34| -1.77|
|Nebraska       |      38.00|      39.38| -1.38|
|North Carolina |      47.03|      48.30| -1.27|
|Iowa           |      42.24|      43.33| -1.09|
|Virginia       |      51.94|      52.85| -0.91|
|Montana        |      39.03|      39.64| -0.60|
|Georgia        |      48.31|      48.88| -0.57|
|New Mexico     |      52.59|      53.00| -0.41|
|Alabama        |      34.47|      34.55| -0.08|
|South Carolina |      40.90|      40.94| -0.03|
|New Hampshire  |      51.49|      51.41|  0.08|
|Minnesota      |      52.30|      52.17|  0.14|
|Illinois       |      54.80|      54.62|  0.18|
|California     |      60.93|      60.73|  0.20|
|Louisiana      |      39.07|      38.81|  0.26|
|Rhode Island   |      57.39|      56.92|  0.47|
|Ohio           |      44.80|      44.27|  0.53|
|Nevada         |      49.00|      48.38|  0.62|
|Maryland       |      64.09|      63.31|  0.78|
|New York       |      56.64|      55.83|  0.82|
|Colorado       |      56.61|      55.69|  0.92|
|Arkansas       |      35.24|      34.30|  0.94|
|Wisconsin      |      50.57|      49.53|  1.04|
|New Jersey     |      53.94|      52.78|  1.16|
|Pennsylvania   |      50.16|      48.98|  1.18|
|Arizona        |      48.33|      47.15|  1.18|
|Massachusetts  |      63.96|      62.66|  1.30|
|Tennessee      |      36.37|      34.94|  1.43|
|Mississippi    |      39.48|      37.91|  1.57|
|Michigan       |      51.20|      49.30|  1.90|
|Texas          |      44.97|      42.98|  1.99|
|West Virginia  |      30.49|      28.49|  2.00|
|Maine          |      55.67|      53.48|  2.19|
|Florida        |      45.61|      43.38|  2.23|
|Missouri       |      43.24|      40.64|  2.59|



My average bias across all my state predictions was 0.74 percentage points for Trump, while among swing states, my average bias was 0.58 percentage points for Harris. 

For error, my MSE across all states was 6.34, and my RMSE was 2.52 percentage points. This error was lower among swing states, where the MSE was 1.40 and the RMSE was 1.18. While this is still a pretty large MSE for swing states that can sometimes come down to fractions of percentage points, the fact that the error is less speaks to the value that polling still holds, even though it can be biased (the model for many non-swing states did not include any polling). 


```
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
```

```
## Warning in geom_abline(slope = 1, intercept = 0, label = "Perfect Prediction"):
## Ignoring unknown parameters: `label`
```

```
## Warning: Removed 1 row containing missing values or values outside the scale range
## (`geom_point()`).
```

<img src="{{< blogdown/postref >}}index_files/figure-html/visualize errors nat pop vote-1.png" width="672" />



[text about which states were the furthest off, did any fall outside their confidence intervals?]

## What went wrong? A few theories

### National Popular Vote Specific

- For popular vote, Democratic bias in the lagged vote share
- Maybe because her campaign was so much shorter, she didn’t get as much support in Democratic strongholds because she didn’t have the time to make many visits there. 

### State-Level Specific

- Split ballots
- Hispanic shifts

### General

- Harris is a woman
- polls under weighted Trump again
- maybe the assassination attempt actually did matter

## Here's What I Would Change For Next Time

1. I would use ensembling to combine predictions based on fundamentals and predictions based on the polls. I expect that a lot of people in the class are questioning their model's reliance on polls right now, and whether they should even be included. I think my model for Electoral College predictions offers an especially interesting perspective in this area because there were actually several states for which my predictions did not factor in polls at all, and these states were usually the states with the largest prediction errors. Luckily, these states were usually also safe states (which is why they didn't have much polling), so errors in vote margin during the prediction process did not have serious consequences for my overall predictions. However, these larger errors convince me to not give up incorporating polling altogether, just to down weight them more. 

2. I would include interaction effects in a future model. I suspect that the economic factors would have more predictive power if they were more specifically in relationship with incumbency. I believe the same would be true for approval rating and incumbency/incumbent party. I think including interaction effects like these may have given my model the opportunity to account for the influence of the Biden Administration on Harris' ultimate loss.














