---
title: 'Blog Post 6: Campaign Ads and Spending'
author: Alex Heuss
date: '2024-10-14'
slug: blog-post-6-campaign-ads-and-spending
categories: []
tags: []
---




This week in class, we discussed the air war in campaigns, particularly the possible impact of advertising over television and radio on the outcome of elections. In section, we also discussed candidate contributions at the state level and how they may be a way to predict election outcomes. 

## Campaign Contribution Visualization

Visualizing campaign contributions per state and that state's popular vote, there does appear to be a positive correlation, although certainly nothing conclusive, as most of the points are centered on one point of the graph (most candiadtes do not receive a ton of contributions from any one state or another). Thus, it is hard to be certain about any trends we may be seeing. 

<img src="{{< blogdown/postref >}}index_files/figure-html/contribution data and basic national visualization-1.png" width="672" />

Looking at that relationship in individual swing states, the relationship is inconclusive. One takeaway from this graph is that the relationship between contributions and popular vote varies between states, highlighting the importance of including state fixed effects in any regression analysis. 

<img src="{{< blogdown/postref >}}index_files/figure-html/swing states and contributions-1.png" width="672" />


```
## 
## Call:
## lm(formula = D_pv ~ contribution_receipt_amount + factor(state), 
##     data = d_campaign_spending)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -8.3469 -1.9696  0.0773  1.9113  9.0506 
## 
## Coefficients:
##                               Estimate Std. Error t value Pr(>|t|)    
## (Intercept)                  3.686e+01  1.825e+00  20.192  < 2e-16 ***
## contribution_receipt_amount  5.327e-08  2.959e-08   1.800 0.073869 .  
## factor(state)Alaska          2.576e+00  2.579e+00   0.999 0.319483    
## factor(state)Arizona         8.750e+00  2.584e+00   3.386 0.000906 ***
## factor(state)Arkansas       -9.433e-01  2.579e+00  -0.366 0.715032    
## factor(state)California      1.730e+01  4.808e+00   3.599 0.000435 ***
## factor(state)Colorado        1.440e+01  2.605e+00   5.529 1.41e-07 ***
## factor(state)Connecticut     2.057e+01  2.597e+00   7.920 5.06e-13 ***
## factor(state)Delaware        2.117e+01  2.579e+00   8.210 9.68e-14 ***
## factor(state)Florida         1.063e+01  2.718e+00   3.910 0.000140 ***
## factor(state)Georgia         9.431e+00  2.592e+00   3.639 0.000377 ***
## factor(state)Hawaii          2.942e+01  2.579e+00  11.409  < 2e-16 ***
## factor(state)Idaho          -4.617e+00  2.579e+00  -1.790 0.075453 .  
## factor(state)Illinois        1.968e+01  2.716e+00   7.245 2.16e-11 ***
## factor(state)Indiana         6.020e+00  2.580e+00   2.334 0.020956 *  
## factor(state)Iowa            1.105e+01  2.579e+00   4.286 3.26e-05 ***
## factor(state)Kansas          2.334e+00  2.579e+00   0.905 0.366864    
## factor(state)Kentucky       -7.378e-02  2.579e+00  -0.029 0.977215    
## factor(state)Louisiana       2.689e+00  2.579e+00   1.043 0.298745    
## factor(state)Maine           1.597e+01  2.579e+00   6.191 5.51e-09 ***
## factor(state)Maryland        2.422e+01  2.660e+00   9.106 5.22e-16 ***
## factor(state)Massachusetts   2.282e+01  2.735e+00   8.346 4.44e-14 ***
## factor(state)Michigan        1.493e+01  2.591e+00   5.763 4.59e-08 ***
## factor(state)Minnesota       1.401e+01  2.587e+00   5.417 2.38e-07 ***
## factor(state)Mississippi     5.078e+00  2.579e+00   1.969 0.050829 .  
## factor(state)Missouri        6.110e+00  2.581e+00   2.367 0.019197 *  
## factor(state)Montana         4.429e+00  2.579e+00   1.717 0.088045 .  
## factor(state)Nebraska        1.191e+00  2.579e+00   0.462 0.644870    
## factor(state)Nevada          1.430e+01  2.579e+00   5.546 1.29e-07 ***
## factor(state)New Hampshire   1.436e+01  2.579e+00   5.570 1.16e-07 ***
## factor(state)New Jersey      1.918e+01  2.628e+00   7.300 1.60e-11 ***
## factor(state)New Mexico      1.593e+01  2.581e+00   6.171 6.10e-09 ***
## factor(state)New York        1.806e+01  3.514e+00   5.140 8.51e-07 ***
## factor(state)North Carolina  1.068e+01  2.595e+00   4.114 6.41e-05 ***
## factor(state)North Dakota   -1.301e+00  2.580e+00  -0.504 0.614762    
## factor(state)Ohio            1.029e+01  2.590e+00   3.974 0.000110 ***
## factor(state)Oklahoma       -4.809e+00  2.579e+00  -1.865 0.064167 .  
## factor(state)Oregon          1.696e+01  2.589e+00   6.550 8.76e-10 ***
## factor(state)Pennsylvania    1.309e+01  2.638e+00   4.963 1.87e-06 ***
## factor(state)Rhode Island    2.287e+01  2.579e+00   8.869 2.11e-15 ***
## factor(state)South Carolina  6.209e+00  2.579e+00   2.407 0.017291 *  
## factor(state)South Dakota    1.100e+00  2.580e+00   0.427 0.670308    
## factor(state)Tennessee       1.094e+00  2.581e+00   0.424 0.672177    
## factor(state)Texas           5.065e+00  2.732e+00   1.854 0.065716 .  
## factor(state)Utah           -5.934e+00  2.579e+00  -2.301 0.022785 *  
## factor(state)Vermont         2.678e+01  2.579e+00  10.385  < 2e-16 ***
## factor(state)Virginia        1.382e+01  2.648e+00   5.218 5.96e-07 ***
## factor(state)Washington      1.787e+01  2.665e+00   6.705 3.90e-10 ***
## factor(state)West Virginia  -3.341e+00  2.579e+00  -1.295 0.197237    
## factor(state)Wisconsin       1.404e+01  2.581e+00   5.439 2.14e-07 ***
## factor(state)Wyoming        -9.864e+00  2.579e+00  -3.824 0.000192 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 3.647 on 149 degrees of freedom
##   (4 observations deleted due to missingness)
## Multiple R-squared:  0.9053,	Adjusted R-squared:  0.8736 
## F-statistic:  28.5 on 50 and 149 DF,  p-value: < 2.2e-16
```

```
## 
## Call:
## lm(formula = D_pv ~ log(contribution_receipt_amount) + factor(state), 
##     data = d_campaign_spending)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -8.4074 -2.1273  0.1057  1.8874  9.7412 
## 
## Coefficients:
##                                  Estimate Std. Error t value Pr(>|t|)    
## (Intercept)                        0.8159    12.0533   0.068 0.946120    
## log(contribution_receipt_amount)   2.4420     0.8043   3.036 0.002829 ** 
## factor(state)Alaska                4.2876     2.5973   1.651 0.100887    
## factor(state)Arizona               6.4501     2.6698   2.416 0.016906 *  
## factor(state)Arkansas             -0.5393     2.5335  -0.213 0.831723    
## factor(state)California           15.1284     4.0185   3.765 0.000239 ***
## factor(state)Colorado             11.0099     2.8619   3.847 0.000177 ***
## factor(state)Connecticut          17.4151     2.8083   6.201 5.24e-09 ***
## factor(state)Delaware             21.9221     2.5422   8.623 8.90e-15 ***
## factor(state)Florida               6.2710     3.1906   1.965 0.051221 .  
## factor(state)Georgia               6.4667     2.7703   2.334 0.020917 *  
## factor(state)Hawaii               29.4045     2.5297  11.624  < 2e-16 ***
## factor(state)Idaho                -2.8521     2.6010  -1.097 0.274615    
## factor(state)Illinois             15.3483     3.1832   4.822 3.48e-06 ***
## factor(state)Indiana               4.7607     2.5704   1.852 0.065992 .  
## factor(state)Iowa                 10.7887     2.5314   4.262 3.58e-05 ***
## factor(state)Kansas                2.8087     2.5350   1.108 0.269670    
## factor(state)Kentucky             -0.3147     2.5311  -0.124 0.901214    
## factor(state)Louisiana             2.5954     2.5299   1.026 0.306602    
## factor(state)Maine                15.7602     2.5307   6.228 4.59e-09 ***
## factor(state)Maryland             20.0725     3.0764   6.525 1.00e-09 ***
## factor(state)Massachusetts        18.4482     3.2128   5.742 5.08e-08 ***
## factor(state)Michigan             12.0270     2.7598   4.358 2.43e-05 ***
## factor(state)Minnesota            11.4768     2.7045   4.244 3.85e-05 ***
## factor(state)Mississippi           7.4131     2.6531   2.794 0.005889 ** 
## factor(state)Missouri              4.3124     2.6128   1.650 0.100952    
## factor(state)Montana               6.0958     2.5937   2.350 0.020074 *  
## factor(state)Nebraska              2.8531     2.5935   1.100 0.273073    
## factor(state)Nevada               13.6415     2.5408   5.369 2.98e-07 ***
## factor(state)New Hampshire        13.9050     2.5350   5.485 1.73e-07 ***
## factor(state)New Jersey           15.3878     2.9667   5.187 6.87e-07 ***
## factor(state)New Mexico           14.3679     2.5935   5.540 1.34e-07 ***
## factor(state)New York             14.1120     3.7107   3.803 0.000208 ***
## factor(state)North Carolina        7.5762     2.7966   2.709 0.007538 ** 
## factor(state)North Dakota          3.7015     3.0426   1.217 0.225690    
## factor(state)Ohio                  7.4367     2.7531   2.701 0.007709 ** 
## factor(state)Oklahoma             -4.8534     2.5297  -1.919 0.056949 .  
## factor(state)Oregon               14.2587     2.7295   5.224 5.81e-07 ***
## factor(state)Pennsylvania          9.1872     3.0027   3.060 0.002629 ** 
## factor(state)Rhode Island         23.2334     2.5327   9.173 3.50e-16 ***
## factor(state)South Carolina        5.6123     2.5387   2.211 0.028580 *  
## factor(state)South Dakota          4.9169     2.8423   1.730 0.085717 .  
## factor(state)Tennessee            -0.5135     2.5963  -0.198 0.843484    
## factor(state)Texas                 0.6800     3.2117   0.212 0.832600    
## factor(state)Utah                 -5.7113     2.5308  -2.257 0.025480 *  
## factor(state)Vermont              26.6028     2.5304  10.513  < 2e-16 ***
## factor(state)Virginia              9.7776     3.0415   3.215 0.001601 ** 
## factor(state)Washington           13.8421     3.0609   4.522 1.24e-05 ***
## factor(state)West Virginia        -1.1641     2.6375  -0.441 0.659588    
## factor(state)Wisconsin            12.3482     2.6035   4.743 4.89e-06 ***
## factor(state)Wyoming              -7.1046     2.6995  -2.632 0.009387 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 3.577 on 149 degrees of freedom
##   (4 observations deleted due to missingness)
## Multiple R-squared:  0.9089,	Adjusted R-squared:  0.8783 
## F-statistic: 29.73 on 50 and 149 DF,  p-value: < 2.2e-16
```

Briefly analyzing the results from those regressions, state level contributions may be a predictive variable in election forecasts, when controlling for state. Further, that predictor holds more significance when in logarithmic form. 

## National Popular Vote Prediction

This week I kept my national popular vote prediction model largely the same as last week's, but included also the popular vote for the two prior elections as predictors and updated polling data with the most recent polls. 


```
##            s1
## [1,] 49.08123
## [2,] 47.90600
```

This week's updated model finds Kamala Harris winning the popular vote with 49.08% and Donald Trump getting 47.91%. The race is still very close, but popular vote totals have diverged a little from last week's predictions with this week's updates.

## Electoral College Prediction

My electoral college model this week includes a number of predictive variables, the most predictive of which are: the latest poll results, the state's results from the past two presidential elections and incumbency. Other variables included in the model are swing in party ID and the economy. 








```
## 
## Call:
## lm(formula = D_pv ~ latest_pollav_DEM + mean_pollav_DEM + D_pv_lag1 + 
##     D_pv_lag2 + incumbent_party + q2_gdp_growth + avg_state_unemployment + 
##     dem_perc_lag4 + rep_perc_lag4 + state, data = d.train)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -5.3891 -0.9621 -0.0061  1.0568  5.8905 
## 
## Coefficients:
##                         Estimate Std. Error t value Pr(>|t|)    
## (Intercept)             8.840583   2.866358   3.084  0.00246 ** 
## latest_pollav_DEM       0.619397   0.054280  11.411  < 2e-16 ***
## mean_pollav_DEM         0.060106   0.049399   1.217  0.22573    
## D_pv_lag1               0.198497   0.037734   5.260 5.23e-07 ***
## D_pv_lag2              -0.042844   0.029079  -1.473  0.14288    
## incumbent_partyTRUE     0.210530   0.391978   0.537  0.59205    
## q2_gdp_growth           0.020254   0.017821   1.137  0.25765    
## avg_state_unemployment  0.070833   0.112077   0.632  0.52841    
## dem_perc_lag4           0.003739   0.022429   0.167  0.86785    
## rep_perc_lag4          -0.011446   0.027218  -0.421  0.67475    
## stateCalifornia         2.138878   1.091549   1.959  0.05203 .  
## stateFlorida           -0.872559   1.016075  -0.859  0.39193    
## stateGeorgia           -0.320180   1.051600  -0.304  0.76122    
## stateMaryland           2.687116   1.148004   2.341  0.02065 *  
## stateMichigan           1.938597   1.072536   1.807  0.07282 .  
## stateMinnesota          1.015591   1.100740   0.923  0.35777    
## stateMissouri          -0.664331   1.081675  -0.614  0.54009    
## stateMontana           -2.739940   1.649093  -1.661  0.09884 .  
## stateNevada             0.175914   1.365480   0.129  0.89768    
## stateNew Hampshire      0.153772   1.278629   0.120  0.90445    
## stateNew Mexico         0.928517   1.320735   0.703  0.48320    
## stateNew York           1.441742   1.111288   1.297  0.19663    
## stateNorth Carolina    -1.478425   1.112963  -1.328  0.18620    
## stateOhio              -0.657506   1.025251  -0.641  0.52236    
## statePennsylvania       1.094280   1.052762   1.039  0.30038    
## stateTexas             -0.858501   1.025282  -0.837  0.40382    
## stateVirginia           0.727469   1.035138   0.703  0.48335    
## stateWisconsin          1.320400   1.048960   1.259  0.21019    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 1.937 on 141 degrees of freedom
## Multiple R-squared:  0.9182,	Adjusted R-squared:  0.9025 
## F-statistic: 58.58 on 27 and 141 DF,  p-value: < 2.2e-16
```


```
## 
## Call:
## lm(formula = D_pv ~ D_pv_lag1 + D_pv_lag2 + incumbent_party + 
##     q2_gdp_growth + avg_state_unemployment + dem_perc_lag4 + 
##     rep_perc_lag4 + state, data = d.train.nopolls)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -13.1320  -2.8713  -0.2031   2.6336  11.5496 
## 
## Coefficients:
##                        Estimate Std. Error t value Pr(>|t|)    
## (Intercept)            12.73828    4.26684   2.985 0.003266 ** 
## D_pv_lag1               0.56269    0.06582   8.549 8.32e-15 ***
## D_pv_lag2               0.14288    0.05854   2.441 0.015722 *  
## incumbent_partyTRUE    -3.28823    0.86803  -3.788 0.000213 ***
## q2_gdp_growth          -0.03853    0.03571  -1.079 0.282225    
## avg_state_unemployment -0.24985    0.25442  -0.982 0.327522    
## dem_perc_lag4           0.03338    0.03528   0.946 0.345562    
## rep_perc_lag4          -0.01618    0.03807  -0.425 0.671433    
## stateAlaska             3.20322    3.99770   0.801 0.424137    
## stateArkansas           1.51727    2.29923   0.660 0.510243    
## stateColorado           3.67862    2.14483   1.715 0.088215 .  
## stateConnecticut        5.33317    2.26969   2.350 0.019978 *  
## stateDelaware           4.48952    4.03227   1.113 0.267168    
## stateHawaii             4.63674    4.36147   1.063 0.289294    
## stateIdaho             -2.18769    3.92042  -0.558 0.577589    
## stateIllinois           5.65773    2.21566   2.554 0.011576 *  
## stateIndiana            1.71629    2.16975   0.791 0.430082    
## stateIowa               2.37066    2.34118   1.013 0.312747    
## stateKansas             0.98219    2.37801   0.413 0.680124    
## stateKentucky          -1.94592    3.81109  -0.511 0.610321    
## stateLouisiana          1.29691    2.29769   0.564 0.573224    
## stateMaine              1.90442    3.41328   0.558 0.577643    
## stateMassachusetts      6.34953    2.42891   2.614 0.009778 ** 
## stateMississippi        2.66505    2.95282   0.903 0.368092    
## stateNebraska          -1.13923    2.83634  -0.402 0.688461    
## stateNew Jersey         5.32483    2.18861   2.433 0.016050 *  
## stateNorth Dakota      -3.51384    3.39753  -1.034 0.302550    
## stateOklahoma          -2.15634    2.76496  -0.780 0.436585    
## stateOregon             4.66970    2.14390   2.178 0.030824 *  
## stateRhode Island       6.71831    3.60903   1.862 0.064459 .  
## stateSouth Carolina     2.03364    2.70950   0.751 0.453995    
## stateSouth Dakota      -1.92483    3.52308  -0.546 0.585568    
## stateTennessee          1.74922    2.16787   0.807 0.420902    
## stateUtah              -1.02329    3.08880  -0.331 0.740847    
## stateVermont            4.51818    4.27455   1.057 0.292068    
## stateWashington         5.33051    2.17840   2.447 0.015461 *  
## stateWest Virginia      1.18315    2.35931   0.501 0.616704    
## stateWyoming           -1.68178    2.65130  -0.634 0.526755    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 4.861 on 164 degrees of freedom
## Multiple R-squared:  0.7789,	Adjusted R-squared:  0.729 
## F-statistic: 15.61 on 37 and 164 DF,  p-value: < 2.2e-16
```

Looking at the results below, my state-level model predicts that Donald Trump will win 272 votes and Kamala Harris will win 263. The District of Columbia was not included in my model, but it's 3 electoral college votes will almost certainly go to Harris, bringing her total to 266 and the presidential race results within 6 electoral college votes. 


|Winner     | States Won| Electors|
|:----------|----------:|--------:|
|Democrat   |         21|      263|
|Republican |         28|      267|

<img src="{{< blogdown/postref >}}index_files/figure-html/visualize results-1.png" width="672" />

## Conclusion

I'm finally close to being happy with my prediction models this week. Next week, I hope to incorporate more Lasso regression or machine learning techniques into my models to make my predictions more sophisticated and help to keep my model from being overfitted. 


