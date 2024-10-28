---
title: 'Blog Post 8: Shocks and Game Changing Events'
author: Alex Heuss
date: '2024-10-24'
slug: blog-post-8-shocks-and-game-changing-events
categories: []
tags: []
---












## Discussion of Shocks and Game Changing Events

<img src="{{< blogdown/postref >}}index_files/figure-html/plot Biden dropout-1.png" width="672" />

<img src="{{< blogdown/postref >}}index_files/figure-html/plot other shocks-1.png" width="672" />






Table: (\#tab:explore the hurricane data)Counties in Each State Impacted by a Hurricanes in Election Years

|State          | 1996| 2000| 2004| 2008| 2012|
|:--------------|----:|----:|----:|----:|----:|
|Alabama        |    0|    0|   14|    0|    0|
|Arkansas       |    0|    0|    0|    0|    0|
|Delaware       |    0|    0|    0|    0|    0|
|Florida        |    4|   25|   71|    0|    0|
|Georgia        |    8|    0|    0|    0|    0|
|Louisiana      |    0|    0|   14|   39|   31|
|Maine          |    8|    0|    0|    0|    0|
|Maryland       |   10|    0|    0|    0|    0|
|Mississippi    |    0|    0|   25|    8|    0|
|New Hampshire  |    1|    0|    0|    0|    0|
|New Jersey     |    0|    0|    0|    0|    0|
|North Carolina |  124|    0|   33|    0|    0|
|South Carolina |   15|    0|    4|    0|    0|
|Texas          |    0|    0|    0|   24|    0|
|Virginia       |    4|    0|    0|    0|    0|


```
## Warning: There were 2 warnings in `mutate()`.
## The first warning was:
## ℹ In argument: `damage_property = case_when(...)`.
## Caused by warning:
## ! NAs introduced by coercion
## ℹ Run `dplyr::last_dplyr_warnings()` to see the 1 remaining warning.
```

```
## # A tibble: 138 × 13
## # Groups:   state [15]
##    state    ymd       year month   day counties_affected injuries_direct
##    <chr>    <chr>    <dbl> <dbl> <dbl>             <int>           <dbl>
##  1 Alabama  07092005  2005     7     9                15               0
##  2 Alabama  07102005  2005     7    10                 3               0
##  3 Alabama  07181997  1997     7    18                 4               0
##  4 Alabama  07211997  1997     7    21                 1               0
##  5 Alabama  08272005  2005     8    27                 6               0
##  6 Alabama  09011998  1998     9     1                 4               0
##  7 Alabama  09132004  2004     9    13                14               0
##  8 Alabama  09251998  1998     9    25                13               0
##  9 Alabama  10022002  2002    10     2                 4               0
## 10 Arkansas 08292005  2005     8    29                 2               0
## # ℹ 128 more rows
## # ℹ 6 more variables: injuries_indirect <dbl>, deaths_direct <dbl>,
## #   deaths_indirect <dbl>, magnitude <dbl>, damage_property <dbl>,
## #   damage_crops <dbl>
```

## National Popular Vote Prediction


```
##            s1
## [1,] 49.17162
## [2,] 48.04352
```

This week's national vote prediction predicts an even tighter popular vote margin for Kamala Harris, who would win 49.17% of the popular vote compared to Trump's 48.04%. Trump gained on Harris from last week's prediction by 0.03 percentage points. 

## Electoral College Prediction

This week, I again did not make major changes to my electoral college prediction model. 538 has not updated it's polling averages from the ones I used last week, so those were held constant in this week's model as well. This week though, we were given access to estimated voter roll party identification, so I was able to use a more accurate value for party identification swing. 






```
## 
## Call:
## lm(formula = D_pv ~ latest_pollav_DEM + mean_pollav_DEM + D_pv_lag1 + 
##     D_pv_lag2 + incumbent_party + q2_gdp_growth + avg_state_unemployment + 
##     dem_perc_swing + rep_perc_swing + state, data = d.train)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -5.5408 -1.0362  0.0233  1.0171  5.7929 
## 
## Coefficients:
##                         Estimate Std. Error t value Pr(>|t|)    
## (Intercept)             8.306930   1.816310   4.574 1.02e-05 ***
## latest_pollav_DEM       0.616738   0.052720  11.698  < 2e-16 ***
## mean_pollav_DEM         0.063562   0.048479   1.311  0.19189    
## D_pv_lag1               0.195739   0.036966   5.295 4.32e-07 ***
## D_pv_lag2              -0.036238   0.028423  -1.275  0.20437    
## incumbent_partyTRUE     0.322553   0.384381   0.839  0.40277    
## q2_gdp_growth           0.019680   0.017310   1.137  0.25746    
## avg_state_unemployment  0.073149   0.108590   0.674  0.50162    
## dem_perc_swing         -0.006492   0.015633  -0.415  0.67858    
## rep_perc_swing         -0.012703   0.017954  -0.708  0.48037    
## stateCalifornia         2.177988   1.077782   2.021  0.04514 *  
## stateFlorida           -0.856639   1.012201  -0.846  0.39877    
## stateGeorgia           -0.122485   1.023893  -0.120  0.90494    
## stateMaryland           2.850547   1.116590   2.553  0.01172 *  
## stateMichigan           1.957228   1.067834   1.833  0.06887 .  
## stateMinnesota          1.181037   1.054475   1.120  0.26456    
## stateMissouri          -0.495467   1.041583  -0.476  0.63501    
## stateMontana           -2.622234   1.620572  -1.618  0.10782    
## stateNebraska          -3.887828   1.226623  -3.170  0.00186 ** 
## stateNevada             0.178781   1.329981   0.134  0.89325    
## stateNew Hampshire      0.248870   1.101654   0.226  0.82159    
## stateNew Mexico         1.055267   1.314682   0.803  0.42347    
## stateNew York           1.557901   1.091553   1.427  0.15566    
## stateNorth Carolina    -1.233812   1.042764  -1.183  0.23866    
## stateOhio              -0.591318   1.016899  -0.581  0.56181    
## statePennsylvania       1.188599   1.036660   1.147  0.25345    
## stateTexas             -0.682451   0.998613  -0.683  0.49545    
## stateVirginia           0.861945   1.006164   0.857  0.39304    
## stateWisconsin          1.398172   1.031982   1.355  0.17758    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 1.915 on 145 degrees of freedom
## Multiple R-squared:  0.9291,	Adjusted R-squared:  0.9155 
## F-statistic: 67.91 on 28 and 145 DF,  p-value: < 2.2e-16
```

```
## 
## Call:
## lm(formula = D_pv ~ D_pv_lag1 + D_pv_lag2 + incumbent_party + 
##     q2_gdp_growth + avg_state_unemployment + dem_perc_swing + 
##     rep_perc_swing + state, data = d.train.nopolls)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -13.2984  -2.7599   0.3756   2.7032  11.9703 
## 
## Coefficients:
##                         Estimate Std. Error t value Pr(>|t|)    
## (Intercept)            12.734526   3.752205   3.394 0.000869 ***
## D_pv_lag1               0.576522   0.065993   8.736 3.08e-15 ***
## D_pv_lag2               0.137987   0.059070   2.336 0.020731 *  
## incumbent_partyTRUE    -2.955940   0.869224  -3.401 0.000849 ***
## q2_gdp_growth          -0.033747   0.035776  -0.943 0.346958    
## avg_state_unemployment -0.156092   0.248376  -0.628 0.530605    
## dem_perc_swing          0.003842   0.026542   0.145 0.885097    
## rep_perc_swing         -0.027601   0.030073  -0.918 0.360101    
## stateAlaska             1.421865   3.776920   0.376 0.707073    
## stateArkansas           1.719450   2.294599   0.749 0.454749    
## stateColorado           3.217016   2.122020   1.516 0.131488    
## stateConnecticut        5.074723   2.212030   2.294 0.023082 *  
## stateDelaware           4.789288   4.016458   1.192 0.234864    
## stateHawaii             3.944937   4.328694   0.911 0.363484    
## stateIdaho             -2.941307   3.916447  -0.751 0.453747    
## stateIllinois           5.548963   2.213423   2.507 0.013176 *  
## stateIndiana            1.203410   2.144776   0.561 0.575522    
## stateIowa               1.857766   2.320936   0.800 0.424644    
## stateKansas             0.424366   2.338639   0.181 0.856238    
## stateKentucky          -1.936348   3.810060  -0.508 0.611999    
## stateLouisiana          1.689429   2.276987   0.742 0.459201    
## stateMaine              1.140744   3.317248   0.344 0.731386    
## stateMassachusetts      6.185258   2.383919   2.595 0.010350 *  
## stateMississippi        1.889383   3.014746   0.627 0.531740    
## stateNew Jersey         4.855351   2.167009   2.241 0.026430 *  
## stateNorth Dakota      -4.639883   3.319237  -1.398 0.164085    
## stateOklahoma          -1.847581   2.759580  -0.670 0.504132    
## stateOregon             4.302667   2.141969   2.009 0.046246 *  
## stateRhode Island       6.181425   3.520643   1.756 0.081042 .  
## stateSouth Carolina     2.066335   2.697532   0.766 0.444799    
## stateSouth Dakota      -3.924156   3.412644  -1.150 0.251906    
## stateTennessee          1.206913   2.147205   0.562 0.574844    
## stateUtah              -1.809775   3.093335  -0.585 0.559334    
## stateVermont            5.056064   4.260626   1.187 0.237107    
## stateWashington         4.905970   2.151008   2.281 0.023881 *  
## stateWest Virginia      0.905971   2.347768   0.386 0.700094    
## stateWyoming           -1.492020   2.611267  -0.571 0.568545    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 4.859 on 160 degrees of freedom
## Multiple R-squared:  0.7747,	Adjusted R-squared:  0.724 
## F-statistic: 15.28 on 36 and 160 DF,  p-value: < 2.2e-16
```

Looking at the models for states with and without polls, we see that the most statistically significant predictors are latest polls (if applicable), a state's recent vote share, incumbency, and some state fixed effects. The adjusted R squared for my model with polls is very high at 0.9155, which suggests that it fits the observed data very well, but definitely might be overfitting. On the other hand, my model without polls has an adjusted R squared of 0.724, which is lower and might encourage me to look for another variable that could explain more of the variance. 


|Winner     | States Won| Electors|
|:----------|----------:|--------:|
|Democrat   |         21|      263|
|Republican |         29|      272|

My electoral college prediction remains the same this week, with Trump winning the electoral college 272-266. (Reminder that DC is not included in my model, but will almost certainly go blue)


|State          |Winner     |    Margin|
|:--------------|:----------|---------:|
|Michigan       |Democrat   |  2.747673|
|Pennsylvania   |Democrat   |  0.962253|
|Wisconsin      |Democrat   |  1.579654|
|Arizona        |Republican | -3.272327|
|Georgia        |Republican | -3.000735|
|Nevada         |Republican | -1.599029|
|North Carolina |Republican | -5.603819|

Looking at the specific state-level predictions for swing states this week, most of the states are further red than last week with the correction of my partisan swing variable. 

A full look at the electoral college mapping of predictions is below. 

<img src="{{< blogdown/postref >}}index_files/figure-html/map-1.png" width="672" />











