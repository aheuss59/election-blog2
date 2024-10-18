---
title: 'Blog Post 7: The Ground Game'
author: Alex Heuss
date: '2024-10-21'
slug: blog-post-7-the-ground-game
categories: []
tags: []
---






```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```






``` r
d_state_party_id <- 
  d_state_party_id |>
  group_by(state) |>
  arrange(year) |>
  mutate(dem_perc_lag4 = lag(dem_perc, 1),
         rep_perc_lag4 = lag(rep_perc, 1),
         dem_perc_swing = dem_perc - dem_perc_lag4,
         rep_perc_swing = rep_perc - rep_perc_lag4)

open_primaries <- 
  d_state_party_id |>
  filter(year == 2024) |>
  mutate(open_primary_2024 = ifelse(ind_perc > dem_perc + rep_perc, TRUE, FALSE)) |>
  select(state, open_primary_2024)
```

## National Popular Vote Prediction

This week, I started by re-running my national popular vote prediction model from past weeks with updated poll numbers from this week. 


``` r
# Subset to the weeks_left we have polling data for
nat_data_subset <- 
  nat_data |>
  select(-c(paste0("nat_weeks_left_", 0:3)),
         -candidate, -winner)
# Train and Test splits
nat_train <- 
  nat_data_subset |> 
  filter(year <= 2020)
nat_test <- 
  nat_data_subset |>
  filter(year == 2024)
x.train <- nat_train |>
  ungroup() |> 
  select(-pv, -pv2p, -year) |>
  as.matrix()
y.train <- nat_train$pv
x.test <- nat_test |>
  ungroup() |> 
  select(-pv, -pv2p, -year) |>
  as.matrix()

# Use Lasso for National Popular Vote
lasso.nat <- glmnet(x = x.train, y = y.train, alpha = 1)
```

```
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
```

``` r
set.seed(02138)
cv.lasso.nat <- cv.glmnet(x = x.train, y = y.train, alpha = 1)
```

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

``` r
lambda.min.lasso <- cv.lasso.nat$lambda.min
mse.lasso <- mean((predict(lasso.nat, s = lambda.min.lasso, newx = x.train) - y.train)^2)
```

```
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
```

``` r
(lasso.nat.pred <- predict(lasso.nat, s = lambda.min.lasso, newx = x.test))
```

```
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
```

```
##            s1
## [1,] 49.06439
## [2,] 47.90759
```

The model's predictions have not changed much from last week, Kamala Harris' popular vote share shrank by about 0.02 percentage points and Donald Trump's grew by 0.001 percentage points. It seems like if I continue to hold my LASSO model constant, the two candidates will probably remain about the same in the popular vote share prediction unless there are significant polling shifts. 

## Electoral College Predictions

In my electoral prediction model this week, I updated the polling data with polls from this week and changed the value I use to represent partisan identification. Last week, I made a mistake in my model and instead of using swing in party identification from one election to the next, I used the partisan identification of the state during the last election. I corrected it in this week's model. I also took a minute to try to find ways to correct for states with inaccurate party identification data for 2024, specifically states that have a very large proportion of voters registered as independent due to open state primaries. 


``` r
# Merge data.
d <- d_pollav_state |>
  left_join(d_state_party_id, by = c("year", "state")) |>
  left_join(d_state_popvote, by = c("year", "state")) |>
  left_join(d_popvote |> filter(party == "democrat"), by = "year") |>
  left_join(d_turnout, by = c("year", "state")) |>
  left_join(d_state_econ, by = c("state", "year")) |>
  left_join(open_primaries, by = c("state")) |>
  filter(year >= 1980) |>
  ungroup()

# Take a minute to figure out an imputation method for states with open primaries whose 2024 partisan identification is flawed

# Sequester states for which we have polling data for 2024.

states.2024 <- unique(d$state[d$year == 2024])
states.2024 <- states.2024[-which(states.2024 == "Nebraska Cd 2")]

d <- d |>
  filter(state %in% states.2024)

# Separate into training and testing for simple poll prediction model. 
d.train <- d |> filter(year < 2024) |> select(year, state, D_pv, latest_pollav_DEM, mean_pollav_DEM, 
                                              D_pv_lag1, D_pv_lag2, incumbent_party, avg_state_unemployment, q2_gdp_growth, dem_perc, rep_perc, ind_perc, dem_perc_lag4, rep_perc_lag4, dem_perc_swing, rep_perc_swing, open_primary_2024) |> drop_na()

d.test <- d |> filter(year == 2024) |> select(year, state, D_pv, latest_pollav_DEM, mean_pollav_DEM, 
                                              D_pv_lag1, D_pv_lag2, incumbent_party, avg_state_unemployment, q2_gdp_growth, dem_perc, rep_perc, ind_perc, dem_perc_lag4, rep_perc_lag4, dem_perc_swing, rep_perc_swing, open_primary_2024)

# Add back in lagged vote share for 2024. 
t <- d |> 
  filter(year >= 2016) |> 
  arrange(year) |> 
  group_by(state) |> 
  mutate(
    D_pv_lag1 = lag(D_pv, 1),
    R_pv_lag1 = lag(R_pv, 1), 
    D_pv_lag2 = lag(D_pv, 2),
    R_pv_lag2 = lag(R_pv, 2)) |> 
  filter(year == 2024) |> 
  select(state, year, D_pv, R_pv, D_pv_lag1, R_pv_lag1, D_pv_lag2, R_pv_lag2)

# Subset testing data to only relevant variables for our simple model. 
d.test <- d.test |> 
  select(-c(D_pv, D_pv_lag1, D_pv_lag2)) |> 
  left_join(t, by = c("state", "year"))

# Standard frequentist linear regression. 
reg.ols <- lm(D_pv ~ latest_pollav_DEM + mean_pollav_DEM + D_pv_lag1 + D_pv_lag2 + incumbent_party + q2_gdp_growth + avg_state_unemployment + dem_perc_swing + rep_perc_swing + open_primary_2024 + state, 
              data = d.train)
summary(reg.ols)
```

```
## 
## Call:
## lm(formula = D_pv ~ latest_pollav_DEM + mean_pollav_DEM + D_pv_lag1 + 
##     D_pv_lag2 + incumbent_party + q2_gdp_growth + avg_state_unemployment + 
##     dem_perc_swing + rep_perc_swing + open_primary_2024 + state, 
##     data = d.train)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -5.5408 -1.0362  0.0233  1.0171  5.7929 
## 
## Coefficients: (1 not defined because of singularities)
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
## open_primary_2024TRUE   1.398172   1.031982   1.355  0.17758    
## stateCalifornia         2.177988   1.077782   2.021  0.04514 *  
## stateFlorida           -0.856639   1.012201  -0.846  0.39877    
## stateGeorgia           -1.520657   0.857962  -1.772  0.07843 .  
## stateMaryland           2.850547   1.116590   2.553  0.01172 *  
## stateMichigan           0.559056   0.878045   0.637  0.52532    
## stateMinnesota         -0.217135   0.820400  -0.265  0.79164    
## stateMissouri          -1.893639   0.870406  -2.176  0.03121 *  
## stateMontana           -4.020406   1.563750  -2.571  0.01115 *  
## stateNebraska          -3.887828   1.226623  -3.170  0.00186 ** 
## stateNevada             0.178781   1.329981   0.134  0.89325    
## stateNew Hampshire      0.248870   1.101654   0.226  0.82159    
## stateNew Mexico         1.055267   1.314682   0.803  0.42347    
## stateNew York           1.557901   1.091553   1.427  0.15566    
## stateNorth Carolina    -1.233812   1.042764  -1.183  0.23866    
## stateOhio              -1.989490   0.840027  -2.368  0.01919 *  
## statePennsylvania       1.188599   1.036660   1.147  0.25345    
## stateTexas             -2.080623   0.863282  -2.410  0.01720 *  
## stateVirginia          -0.536227   0.835256  -0.642  0.52189    
## stateWisconsin                NA         NA      NA       NA    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 1.915 on 145 degrees of freedom
## Multiple R-squared:  0.9291,	Adjusted R-squared:  0.9155 
## F-statistic: 67.91 on 28 and 145 DF,  p-value: < 2.2e-16
```

``` r
pred.ols.dem <- predict(reg.ols, newdata = d.test)

# Create dataset to summarize winners and EC vote distributions. 
win_pred <- data.frame(state = d.test$state,
                       year = rep(2024, length(d.test$state)),
                       simp_pred_dem = pred.ols.dem,
                       simp_pred_rep = 100 - pred.ols.dem) |> 
            mutate(winner = ifelse(simp_pred_dem > simp_pred_rep, "Democrat", "Republican")) |>
            left_join(d_ec, by = c("state", "year"))
```



```
## 
## Call:
## lm(formula = D_pv ~ D_pv_lag1 + D_pv_lag2 + incumbent_party + 
##     q2_gdp_growth + avg_state_unemployment + dem_perc_swing + 
##     rep_perc_swing + open_primary_2024 + state, data = d.train.nopolls)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -13.2984  -2.7599   0.3756   2.7032  11.9703 
## 
## Coefficients: (1 not defined because of singularities)
##                         Estimate Std. Error t value Pr(>|t|)    
## (Intercept)            11.242507   3.318757   3.388 0.000888 ***
## D_pv_lag1               0.576522   0.065993   8.736 3.08e-15 ***
## D_pv_lag2               0.137987   0.059070   2.336 0.020731 *  
## incumbent_partyTRUE    -2.955940   0.869224  -3.401 0.000849 ***
## q2_gdp_growth          -0.033747   0.035776  -0.943 0.346958    
## avg_state_unemployment -0.156092   0.248376  -0.628 0.530605    
## dem_perc_swing          0.003842   0.026542   0.145 0.885097    
## rep_perc_swing         -0.027601   0.030073  -0.918 0.360101    
## open_primary_2024TRUE   1.492020   2.611267   0.571 0.568545    
## stateAlaska             1.421865   3.776920   0.376 0.707073    
## stateArkansas           1.719450   2.294599   0.749 0.454749    
## stateColorado           3.217016   2.122020   1.516 0.131488    
## stateConnecticut        6.566743   2.847709   2.306 0.022396 *  
## stateDelaware           6.281308   4.495867   1.397 0.164309    
## stateHawaii             3.944937   4.328694   0.911 0.363484    
## stateIdaho             -1.449288   4.056046  -0.357 0.721327    
## stateIllinois           5.548963   2.213423   2.507 0.013176 *  
## stateIndiana            1.203410   2.144776   0.561 0.575522    
## stateIowa               3.349785   2.869590   1.167 0.244810    
## stateKansas             1.916385   2.675392   0.716 0.474850    
## stateKentucky          -0.444328   4.024211  -0.110 0.912220    
## stateLouisiana          3.181448   2.797735   1.137 0.257175    
## stateMaine              2.632764   3.753576   0.701 0.484071    
## stateMassachusetts      6.185258   2.383919   2.595 0.010350 *  
## stateMississippi        1.889383   3.014746   0.627 0.531740    
## stateNew Jersey         6.347371   2.828948   2.244 0.026223 *  
## stateNorth Dakota      -4.639883   3.319237  -1.398 0.164085    
## stateOklahoma          -0.355561   2.987124  -0.119 0.905400    
## stateOregon             5.794687   2.814363   2.059 0.041118 *  
## stateRhode Island       7.673444   4.140826   1.853 0.065707 .  
## stateSouth Carolina     2.066335   2.697532   0.766 0.444799    
## stateSouth Dakota      -2.432136   3.670942  -0.663 0.508580    
## stateTennessee          1.206913   2.147205   0.562 0.574844    
## stateUtah              -0.317756   3.207927  -0.099 0.921220    
## stateVermont            5.056064   4.260626   1.187 0.237107    
## stateWashington         4.905970   2.151008   2.281 0.023881 *  
## stateWest Virginia      2.397990   2.994258   0.801 0.424399    
## stateWyoming                  NA         NA      NA       NA    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 4.859 on 160 degrees of freedom
## Multiple R-squared:  0.7747,	Adjusted R-squared:  0.724 
## F-statistic: 15.28 on 36 and 160 DF,  p-value: < 2.2e-16
```


|Winner     | States Won| Electors|
|:----------|----------:|--------:|
|Democrat   |         21|      263|
|Republican |         29|      272|

<img src="{{< blogdown/postref >}}index_files/figure-html/visualize electoral college results-1.png" width="672" />



