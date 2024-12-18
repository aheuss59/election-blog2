---
title: 'Blog Post 8: Shocks and Game Changing Events'
author: Alex Heuss
date: '2024-10-24'
slug: blog-post-8-shocks-and-game-changing-events
categories: []
tags: []
---












## Discussion of Shocks and Game Changing Events

This week in class, we discussed shocks that sometimes are theorized to have played a role in election outcomes. These can be non-political shocks like natural disasters, or more political ones like a truly awful debate performance. 

In this election cycle, it seems like hardly anything can truly move the polls much. (My theory is that we are numb to crazy things happening now and it just doesn't phase us anymore). This election cycle, unpredictable shocks have almost been the norm. There have been two attempted assassination attempts on Former President Trump and President Biden dropped his re-election campaign extremely late in the game. Trump has said and done some very strange or alarming things. Two serious hurricanes hit the Southern coast in a matter of two weeks. Yet, almost none of these "game-changing" events have made a significant or lasting impact on the polls. 

The one shock that did make a clear difference was Biden's dropping out in late July. The Democrats went from polling barely above 40% to 45% in a matter of days. Looking at the graph below too, it does look like the first assassination attempt on Former President Trump also had an impact, but was masked somewhat by Harris' entrance into the race as the new Democratic nominee.

<img src="{{< blogdown/postref >}}index_files/figure-html/plot Biden dropout-1.png" width="672" />

<img src="{{< blogdown/postref >}}index_files/figure-html/plot other shocks-1.png" width="672" />

One shock that may have been less predictable are the hurricanes that slammed Florida and North Carolina earlier this month. There are two different theories of voter behavior in situations like this. First, the idea that voters will punish the incumbent no matter their response, simply because it happened and it reduced their well-being. Theories like this are backed up by research like that of Achen and Bartels who found that voters punish the incumbent for shark attacks. On the other hand, another theory is that voters will reward incumbents who respond promptly and efficiently, which is supported by research like the Healy et al paper on tornados and economic impact, which found that voters punished incumbents when economic damage results from tornados, but only with strong effects when a state of emergency was not declared. 





<img src="{{< blogdown/postref >}}index_files/figure-html/look at polls in NC and Georgia to see if there are clear effects-1.png" width="1152" />

If we had to draw conclusions from a these two graphs, we would probably conclude that the hurricanes reduced support for the Democrats in these two states, specifically Helene. That said, it doesn't make a whole lot of sense to draw those conclusions from this evidence alone given confounding variables. Communities that were hit hard by the hurricanes or their aftermath probably don't have a lot of people in them right now who are just sitting at home answering poll questions. They are out there trying to help build back their communities. It is unlikely we will be able to truly look at the impact of these events until after election day. 





Looking at historical data for the effects of hurricanes on state-level popular vote, effects are unclear. Below is the coefficient breakdown for a simple linear model predicting state-level popular vote share for Democratic candidates based on their interaction terms between incumbency status or incumbent party status and whether a hurricane hit the state or how many hurricanes hit the state between July and October of that year (4 separate interaction terms). 


```
## 
## Call:
## lm(formula = D_pv ~ D_pv_lag1 + D_pv_lag2 + incumbent_total_interaction + 
##     incumbent_any_interaction + party_total_interaction + party_any_interaction + 
##     state, data = pop_hurricanes)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -8.0171 -2.1104 -0.0268  1.8362  9.0436 
## 
## Coefficients: (1 not defined because of singularities)
##                             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)                 21.57183    3.87110   5.573 2.90e-07 ***
## D_pv_lag1                    0.38702    0.09532   4.060 0.000109 ***
## D_pv_lag2                    0.04504    0.08366   0.538 0.591710    
## incumbent_total_interaction  1.09092    1.96972   0.554 0.581139    
## incumbent_any_interaction    2.50258    2.45686   1.019 0.311279    
## party_total_interaction     -1.87564    1.81054  -1.036 0.303160    
## party_any_interaction             NA         NA      NA       NA    
## stateArkansas                0.62808    1.75031   0.359 0.720606    
## stateDelaware               11.30072    2.14180   5.276 9.92e-07 ***
## stateFlorida                 7.07906    1.93638   3.656 0.000443 ***
## stateGeorgia                 4.39665    1.79797   2.445 0.016535 *  
## stateLouisiana               1.96362    1.77716   1.105 0.272312    
## stateMaine                   8.76159    2.03881   4.297 4.58e-05 ***
## stateMaryland               13.10823    2.40257   5.456 4.72e-07 ***
## stateMississippi             2.21724    1.70546   1.300 0.197088    
## stateNew Hampshire           7.67852    1.92987   3.979 0.000145 ***
## stateNew Jersey             11.13578    2.12901   5.230 1.20e-06 ***
## stateNorth Carolina          5.43516    1.83687   2.959 0.003998 ** 
## stateSouth Carolina          3.09701    1.77583   1.744 0.084778 .  
## stateTexas                   2.92751    1.69591   1.726 0.087942 .  
## stateVirginia                7.00646    1.86158   3.764 0.000307 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 3.162 on 85 degrees of freedom
## Multiple R-squared:  0.8307,	Adjusted R-squared:  0.7928 
## F-statistic: 21.94 on 19 and 85 DF,  p-value: < 2.2e-16
```

We can see that none of the hurricane relevant variables were statistically significant predictors for incumbent vote share. This finding held true when using all states or just the states in which hurricanes typically impact. It also held true for both predictions of Democratic and Republican popular vote share. 

For a visual of the relationship, we see a very slight negative relationship between interaction of number of hurricanes and incumbency and Democratic popular vote share, but with a very large standard error. 

<img src="{{< blogdown/postref >}}index_files/figure-html/a graph about hurricanes-1.png" width="672" />

The next graph gives the same visualization but for the interaction between incumbency and the binary variable of whether a state was hit by a hurricane. It too shows virtually no relationship. 

<img src="{{< blogdown/postref >}}index_files/figure-html/another graph for hurricanes-1.png" width="672" />

There are a few reasons this might be the case. I would expect that the most prominent is a lack of training data. The data for hurricanes only goes back to 1996, encompassing only seven elections and only a few instances of hurricanes in each. It also may be the case that my analysis just wasn't granular enough and really needed to be at the county-level. 

## National Popular Vote Prediction

I did not change anything in my model for predicting the national popular vote this week, but the national polling averages were updated.


```
## 54 x 1 sparse Matrix of class "dgCMatrix"
##                            s0
## (Intercept)       13.66702333
## party              .         
## incumbent          .         
## incumbent_party    .         
## prev_admin         .         
## deminc             .         
## juneapp            .         
## percent            .         
## two_party_percent  .         
## ind_percent       -0.04382826
## year_prior         .         
## year_prior_2p      .         
## swing1             0.14046105
## swing1_2p          .         
## prior_election     .         
## prior_election_2p  .         
## swing4             .         
## swing4_2p          .         
## pv_lag1            0.07091508
## pv_lag2            .         
## nat_weeks_left_3   0.25133117
## nat_weeks_left_4   .         
## nat_weeks_left_5   0.19292073
## nat_weeks_left_6   .         
## nat_weeks_left_7   .         
## nat_weeks_left_8   .         
## nat_weeks_left_9   .         
## nat_weeks_left_10  .         
## nat_weeks_left_11  .         
## nat_weeks_left_12  .         
## nat_weeks_left_13  .         
## nat_weeks_left_14  .         
## nat_weeks_left_15  .         
## nat_weeks_left_16  .         
## nat_weeks_left_17  .         
## nat_weeks_left_18  0.27481302
## nat_weeks_left_19  .         
## nat_weeks_left_20  .         
## nat_weeks_left_21  .         
## nat_weeks_left_22  .         
## nat_weeks_left_23  .         
## nat_weeks_left_24  .         
## nat_weeks_left_25  .         
## nat_weeks_left_26  .         
## nat_weeks_left_27  .         
## nat_weeks_left_28  .         
## nat_weeks_left_29  .         
## nat_weeks_left_30  .         
## q2_gdp_growth      .         
## q2_rdpi_growth     .         
## GDP                .         
## RDPI               .         
## nat_unemployment   .         
## stock_adj_close    .
```

This week, I wanted to take a closer look at which variables are chosen as significant by my LASSO model. Percentage of independent voters, party identification swing from the previous year, popular vote share from the last election, and polls at weeks 3, 5, and 18 were chosen as the most important predictors.


```
##            s1
## [1,] 49.17162
## [2,] 48.04352
```

This week's national vote prediction predicts an even tighter popular vote margin for Kamala Harris, who would win 49.17% of the popular vote compared to Trump's 48.04%. Trump gained on Harris from last week's prediction by 0.03 percentage points. 

## Electoral College Prediction

This week, I again did not make major changes to my electoral college prediction model. 538 has not updated it's polling averages from the ones I used last week, so those were held constant in this week's model as well. We were given access to estimated voter roll party identification, so I was able to update my data to use a more accurate value for party identification swing. 






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











