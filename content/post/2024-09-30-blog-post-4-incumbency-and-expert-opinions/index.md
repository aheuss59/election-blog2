---
title: 'Blog Post 4: Incumbency and Expert Opinions'
author: Alex Heuss
date: '2024-09-30'
slug: blog-post-4-incumbency-and-expert-opinions
categories: []
tags: []
---


This week, we discussed incumbency, federal spending and expert opinions as they relate to election forecasting.

## How does incumbency influence presidential races?

The question of how incumbency will play into the 2024 election is a complicated one. Historically, the advantage or disadvantage of running as a presidential candidate for the incumbent party, but not the incumbent president has been rather unclear. To narrow in on Harris' situation a little further, the graph below shows the elections where a member of the incumbent administration has run for president, but not the incumbent themselves. 



<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-1.png" width="672" />

We can see in the graph that since 1948, this has only happened 6 times. In 4/5, the candidate from the incumbent administration has lost the electoral college. Interestingly, 3/5 have won the popular vote. Additionally, elections involving candidates from incumbent administrations have often been very close. 

Kamala Harris' case is a little different than the standard one. She is runnning as a member of the incumbent administration (the VP), but in the wake of a one-term incumbent president stepping down. 6 other US Presidents have made the decision to [not run](https://www.britannica.com/story/have-any-us-presidents-decided-not-to-run-for-a-second-term) for a second term: Lyndon B. Johnson, James K. Polk, James Buchanan, Rutherford B. Hayes, Calvin Coolidge, Harry S. Truman and Theodore Roosevelt (although he later changed his mind and ran in the following election). 4 of those presidents' parties lost re-election (Polk, Buchanan, Truman and LBJ), while 3 won (Hayes, Roosevelt and Coolidge). There is no clear advantage or disadvantage in this alone. The most recent example of this situation was in 1968, when Hubert Humphrey (the incumbent VP) lost to Richard Nixon following LBJ's stepping down. 

Similarly, it is uncommon for a former president to lose re-election and actually be a viable candidate in the next election. Only six others [tried](https://www.pewresearch.org/short-reads/2022/11/16/few-former-presidents-have-run-for-their-old-jobs-or-anything-else-after-leaving-office/) and only one, Grover Cleveland succeeded. Ulysses S. Grant and Herbert Hoover were both unsuccessful in gaining their party's nomination and Martin Van Buren, Millard Fillmore, and Theodore Roosevelt ran unsuccessfully as third party candidates. It is unclear whether there is any sort of advantage or disadvantage in the case of Trump because, usually, the candidate's party alone presents enough of a barrier to a former president seeking non-consecutive terms. That being said, the one time a former president did secure their party's official nomination, they won the election. 

Given all of this, I don't really believe that either candidate will have much of an incumbency advantage. I would anticipate that Trump gains no advantage or disadvantage based on his prior term as president. Similarly, the jury is still out on whether Harris' role as VP in the Biden administration will help or hurt her. In this election, I think both partisan identification and administration favorability would be more predictive than incumbency. 

## What is the value of expert opinions in election forecasts?

In class this week, we also briefly discussed the value of expert opinions and their accuracy in predicting elections. Based on our discussions, I don't anticipate using expert opinions very much in my own forecast, primarily because they do not include an estimate of popular vote. While expert opinions are typically accurate, they are too wishy-washy for my personal taste (yes, that is the technical term). Most expert opinions, operate on a scale of sorts that in essence is of the style solid Democrat, lean Democrat, toss-up, lean Republican or strong Republican. These categories are, in my opinion, much too broad to be helpful as I attempt to predict state-level popular vote share. However, we did discuss that expert opinions may be valuable in helping to decide which states to build more complicated models for. 

The following map shows an average of expert ratings for 2024 thus far: 



Based on that map, it would follow that I should spend the most time on predictions for [insert states here].

## Incorporating 2024 Expert Opinions and Incumbency into my Predictions 

In past weeks, I have done some state-level modeling, but this week I really want to take the time to work more comprehensively on my state-level predictions. So far, we have discussed past voting patterns, the economy, weekly polling averages, federal spending, incumbency, and expert ratings as possible predictive variables to include in forecasting models. 

In my model, I'm not going to incorporate expert opinions, but I will try to factor in incumbency, just to give it a try. 


``` r
# Attend office hours next week to see if there's a reasonable way to loop through every state to create an individual model -- could try some experimental code in this week's too if you have time.

# Load in EC
ec <- 
  read_csv("data/corrected_ec_1948_2024.csv")
```

```
## Rows: 1010 Columns: 4
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (2): state, stateab
## dbl (2): year, electors
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
# Load and clean initial pop vote data
state_pop_vote <- 
  read_csv("data/state_2pv_1948_2020.csv") |>
  select(year, state, party, vote_share, two_party_vote_share) |>
  rename(pv = vote_share) |>
  mutate(party = ifelse(party == "Democrat", "DEM", "REP"))
```

```
## Rows: 1918 Columns: 10
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (3): state, candidate, party
## dbl (7): year, state_fips, candidatevotes, totalvotes, vote_share, two_party...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
nat_polls <- 
  read_csv("data/polls/national_polls_1968-2024.csv") |>
  select(year, weeks_left, party, poll_support) |>
  filter(weeks_left <= 30) |>
  group_by(year, weeks_left, party) |>
  summarize(nat_poll_av = mean(poll_support)) |>
  pivot_wider(names_from = weeks_left, values_from = nat_poll_av)
```

```
## Rows: 7378 Columns: 9
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (3): state, party, candidate
## dbl  (4): year, weeks_left, days_left, poll_support
## lgl  (1): before_convention
## date (1): poll_date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
## `summarise()` has grouped output by 'year', 'weeks_left'. You can override using the `.groups` argument.
```

``` r
colnames(nat_polls)[3:33] <- paste0("nat_weeks_left_", 0:30)

# Load and clean poll data
state_polls_wider <- 
  read_csv("data/polls/state_polls_1968-2024.csv") |>
  filter(weeks_left <= 30) |>
  group_by(year, state, weeks_left, party) |>
  summarize(poll_support = mean(poll_support)) |>
  pivot_wider(names_from = weeks_left, values_from = poll_support)
```

```
## Rows: 204634 Columns: 9
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (4): state, party, candidate, poll_date
## dbl (4): year, weeks_left, days_left, poll_support
## lgl (1): before_convention
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
## `summarise()` has grouped output by 'year', 'state', 'weeks_left'. You can override using the `.groups` argument.
```

``` r
colnames(state_polls_wider)[4:34] <- paste0("poll_weeks_left_", 0:30)

# Combine Poll and Pop Data
state_combo_data <- state_polls_wider |>
  left_join(state_pop_vote, by = c("year", "state", "party")) 

state_combo_data <- state_combo_data |> 
  arrange(state, party, year) |>
  group_by(state, party) |>
  mutate(pv_lag1 = lag(pv, 1),
         pv_lag2 = lag(pv, 2),
         two_party_lag1 = lag(two_party_vote_share, 1),
         two_party_lag2 = lag(two_party_vote_share, 2))

# Load, clean and combine econ data
nat_econ_data <- 
  read_csv("data/fred_econ.csv") 
```

```
## Rows: 387 Columns: 14
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## dbl (14): year, quarter, GDP, GDP_growth_quarterly, RDPI, RDPI_growth_quarte...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
ann_nat_econ <- 
  nat_econ_data |>
  filter(year >= 1948) |>
  group_by(year) |>
  select(-quarter) |>
  summarize(ann_gdp = mean(GDP, na.rm=TRUE),,
            ann_rdpi = mean(RDPI, na.rm=TRUE),,
            ann_nat_unemployment = mean(unemployment, na.rm=TRUE),
            ann_stock_close = mean(sp500_adj_close, na.rm=TRUE))
q2_econ <- 
  nat_econ_data |>
  filter(quarter == 2) |>
  mutate(q2_gdp = GDP_growth_quarterly, 
         q2_rdpi = RDPI_growth_quarterly) |>
  select(year, q2_gdp, q2_rdpi)

state_econ_data <- 
  read_csv("data/Historical_State_Unemployment.csv") |>
  mutate(year = format(as.Date(date), "%Y")) |>
  mutate(year = as.double(year)) |>
  group_by(state, year) |>
  summarize(avg_state_unemployment = mean(unemployment))
```

```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```

```
## Rows: 29733 Columns: 3
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): state
## dbl  (1): unemployment
## date (1): date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
## `summarise()` has grouped output by 'state'. You can override using the `.groups` argument.
```

``` r
state_combo_data <- 
  state_combo_data |>
  left_join(ann_nat_econ, by = "year") |>
  left_join(q2_econ, by = "year") |>
  left_join(state_econ_data, by = c("state", "year"))

# Merge with incumbency info
state_combo_data <- state_combo_data |>
  mutate(party = ifelse(party == "DEM", "democrat", "republican")) |>
  left_join(nat_pop_vote |> select(year, party, candidate, incumbent, incumbent_party, prev_admin), by = c("year", "party")) 

# do you want do the fed grants even though you really don't want to lol
```





``` r
# Alex's Intuition Model - 

state_combo_no2024 <- 
  state_combo_data |>
  filter(year != 2024)

alex_intuition <- lm(pv ~ pv_lag1 + pv_lag2 + poll_weeks_left_0 + q2_gdp + incumbent + incumbent_party + avg_state_unemployment + state, state_combo_no2024)

summary(alex_intuition)
```

```
## 
## Call:
## lm(formula = pv ~ pv_lag1 + pv_lag2 + poll_weeks_left_0 + q2_gdp + 
##     incumbent + incumbent_party + avg_state_unemployment + state, 
##     data = state_combo_no2024)
## 
## Residuals:
##      Min       1Q   Median       3Q      Max 
## -10.0519  -1.7494  -0.1698   1.5788   9.9579 
## 
## Coefficients:
##                         Estimate Std. Error t value Pr(>|t|)    
## (Intercept)            -0.199491   0.962619  -0.207   0.8359    
## pv_lag1                 0.234465   0.018738  12.513  < 2e-16 ***
## pv_lag2                 0.011870   0.014369   0.826   0.4090    
## poll_weeks_left_0       0.866220   0.015810  54.788  < 2e-16 ***
## q2_gdp                  0.018094   0.009986   1.812   0.0703 .  
## incumbentTRUE           1.663344   0.288609   5.763 1.15e-08 ***
## incumbent_partyTRUE    -1.895858   0.277634  -6.829 1.62e-11 ***
## avg_state_unemployment -0.307940   0.072908  -4.224 2.66e-05 ***
## stateAlaska             0.354561   1.029361   0.344   0.7306    
## stateArizona           -0.692711   0.947065  -0.731   0.4647    
## stateArkansas          -0.985468   0.945577  -1.042   0.2976    
## stateCalifornia        -0.011875   0.878118  -0.014   0.9892    
## stateColorado          -0.229421   0.877569  -0.261   0.7938    
## stateConnecticut        0.825708   0.877767   0.941   0.3471    
## stateDelaware           0.475619   0.951881   0.500   0.6174    
## stateFlorida           -1.188452   0.917515  -1.295   0.1956    
## stateGeorgia           -0.558051   0.917555  -0.608   0.5432    
## stateHawaii             0.090629   0.948990   0.096   0.9239    
## stateIdaho              0.355607   0.948759   0.375   0.7079    
## stateIllinois          -0.161826   0.876581  -0.185   0.8536    
## stateIndiana           -0.401658   0.918891  -0.437   0.6621    
## stateIowa              -0.510479   0.903191  -0.565   0.5721    
## stateKansas             0.183119   0.882806   0.207   0.8357    
## stateKentucky          -0.591059   0.917213  -0.644   0.5195    
## stateLouisiana          0.946053   0.945645   1.000   0.3174    
## stateMaine             -0.870418   0.921429  -0.945   0.3451    
## stateMaryland          -0.597856   0.897747  -0.666   0.5056    
## stateMassachusetts      0.496963   0.877231   0.567   0.5712    
## stateMichigan           1.296248   0.899111   1.442   0.1498    
## stateMinnesota         -0.380738   0.880821  -0.432   0.6657    
## stateMississippi        0.447090   0.980678   0.456   0.6486    
## stateMissouri          -0.262504   0.875239  -0.300   0.7643    
## stateMontana           -0.618533   0.985079  -0.628   0.5302    
## stateNebraska          -0.678093   0.917159  -0.739   0.4599    
## stateNevada            -0.789810   0.948693  -0.833   0.4053    
## stateNew Hampshire     -1.269759   0.928039  -1.368   0.1716    
## stateNew Jersey         0.916355   0.874778   1.048   0.2951    
## stateNew Mexico        -0.380003   0.945573  -0.402   0.6879    
## stateNew York          -1.364412   0.876142  -1.557   0.1198    
## stateNorth Carolina    -0.772898   0.875140  -0.883   0.3774    
## stateNorth Dakota      -0.687434   0.968124  -0.710   0.4779    
## stateOhio              -0.642565   0.875159  -0.734   0.4630    
## stateOklahoma          -1.351890   0.922891  -1.465   0.1433    
## stateOregon            -0.261688   0.876040  -0.299   0.7652    
## statePennsylvania      -0.626631   0.894220  -0.701   0.4836    
## stateRhode Island       0.679337   0.917729   0.740   0.4594    
## stateSouth Carolina    -0.058016   0.917213  -0.063   0.9496    
## stateSouth Dakota      -0.499108   0.939504  -0.531   0.5954    
## stateTennessee         -0.689690   0.945899  -0.729   0.4661    
## stateTexas             -0.897126   0.917292  -0.978   0.3283    
## stateUtah              -1.071845   0.929962  -1.153   0.2494    
## stateVermont           -0.879748   0.993648  -0.885   0.3762    
## stateVirginia          -1.059015   0.925018  -1.145   0.2526    
## stateWashington        -0.345176   0.894939  -0.386   0.6998    
## stateWest Virginia      0.935928   0.920708   1.017   0.3097    
## stateWisconsin         -1.171028   0.922773  -1.269   0.2048    
## stateWyoming           -0.058645   1.093164  -0.054   0.9572    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 2.751 on 861 degrees of freedom
##   (240 observations deleted due to missingness)
## Multiple R-squared:  0.9187,	Adjusted R-squared:  0.9134 
## F-statistic: 173.7 on 56 and 861 DF,  p-value: < 2.2e-16
```


``` r
# Try MICE 

mice_impute <- mice(state_combo_no2024, m=5, method="pmm")
```

```
## 
##  iter imp variable
##   1   1  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20*  poll_weeks_left_21*  poll_weeks_left_22*  poll_weeks_left_23*  poll_weeks_left_24*  poll_weeks_left_25*  poll_weeks_left_26*  poll_weeks_left_27*  poll_weeks_left_28*  poll_weeks_left_29*  poll_weeks_left_30*  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   1   2  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20*  poll_weeks_left_21*  poll_weeks_left_22*  poll_weeks_left_23*  poll_weeks_left_24*  poll_weeks_left_25*  poll_weeks_left_26*  poll_weeks_left_27*  poll_weeks_left_28*  poll_weeks_left_29*  poll_weeks_left_30*  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   1   3  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22*  poll_weeks_left_23*  poll_weeks_left_24*  poll_weeks_left_25*  poll_weeks_left_26  poll_weeks_left_27*  poll_weeks_left_28*  poll_weeks_left_29*  poll_weeks_left_30*  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   1   4  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20*  poll_weeks_left_21*  poll_weeks_left_22*  poll_weeks_left_23*  poll_weeks_left_24*  poll_weeks_left_25*  poll_weeks_left_26*  poll_weeks_left_27*  poll_weeks_left_28*  poll_weeks_left_29*  poll_weeks_left_30*  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   1   5  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20*  poll_weeks_left_21  poll_weeks_left_22*  poll_weeks_left_23*  poll_weeks_left_24*  poll_weeks_left_25*  poll_weeks_left_26  poll_weeks_left_27*  poll_weeks_left_28*  poll_weeks_left_29*  poll_weeks_left_30*  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   2   1  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   2   2  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   2   3  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   2   4  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   2   5  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   3   1  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28*  poll_weeks_left_29*  poll_weeks_left_30*  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   3   2  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   3   3  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   3   4  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   3   5  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   4   1  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   4   2  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   4   3  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   4   4  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   4   5  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   5   1  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   5   2  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   5   3  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   5   4  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   5   5  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
```

```
## Warning: Number of logged events: 981
```

``` r
complete_mice_no2024 <- complete(mice_impute)

region_data <- 
  state_combo_data |>
  filter(year == 2024) |>
  select(-poll_weeks_left_0, -poll_weeks_left_1, -poll_weeks_left_2, -poll_weeks_left_3, 
         -poll_weeks_left_4, -poll_weeks_left_5, -poll_weeks_left_6) |>
  mutate(region = case_when(state %in% c("Connecticut", "Maine", "Massachusetts", "New Hampshire", "Rhode Island", "Vermont", "New Jersey", "New York", "Pennsylvania") ~ "Northeast",
                            state %in% c("Indiana", "Illinois", "Michigan", "Ohio", "Wisconsin", "Iowa", "Nebraska", "Kansas",	"North Dakota", "Minnesota", "South Dakota", "Missouri") ~ "Midwest",
                            state %in% c("Delaware", "Florida", "Georgia", "Maryland", "North Carolina", "South Carolina", "Virginia", "West Virginia", "Alabama", "Kentucky", "Mississippi", "Tennessee", "Arkansas", "Louisiana", "Oklahoma", "Texas") ~ "South",
                            state %in% c("Arizona", "Colorado", "Idaho", "New Mexico", "Montana", "Utah", "Nevada", "Wyoming", "Alaska", "California", "Hawaii", "Oregon", "Washington") ~ "West"))

region_avs_2024 <- 
  region_data |>
  select(-pv, -two_party_vote_share) |>
  group_by(region) |>
  summarize(across(where(is.numeric), mean, na.rm=TRUE))
```

```
## Warning: There was 1 warning in `summarize()`.
## ℹ In argument: `across(where(is.numeric), mean, na.rm = TRUE)`.
## ℹ In group 1: `region = "Midwest"`.
## Caused by warning:
## ! The `...` argument of `across()` is deprecated as of dplyr 1.1.0.
## Supply arguments directly to `.fns` through an anonymous function instead.
## 
##   # Previously
##   across(a:b, mean, na.rm = TRUE)
## 
##   # Now
##   across(a:b, \(x) mean(x, na.rm = TRUE))
```

``` r
colnames(region_avs_2024)[3:26] <- paste0("poll_weeks_left_", 7:30, "_av")
  
imputed_test <- 
  region_data |>
  select(-pv, -two_party_vote_share) |>
  filter(party == "democrat") |>
  left_join(region_avs_2024, by = c("region")) |>
  mutate(across(where(is.numeric), ~ ifelse(is.na(.), get(paste0(cur_column(), "_av")), .)))

# 4-52
```



``` r
# Seperate into training and test
x.train <- complete_mice_no2024 |>
  filter(party == "democrat") |>
  select(state, all_of(paste0("poll_weeks_left_", 7:30)), pv_lag1, pv_lag2, 41:47, incumbent, incumbent_party, prev_admin) |>
  as.matrix()

mice_impute_no2024_dems <- 
  complete_mice_no2024 |>
  filter(party == "democrat")

y.train <- mice_impute_no2024_dems$pv

# Make Ridge, Lasso and Elastic Net
ridge_model <- glmnet(x = x.train, y = y.train, alpha = 0)
```

```
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
```

``` r
lasso_model <- glmnet(x = x.train, y = y.train, alpha = 1)
```

```
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
```

``` r
elastic_model <- glmnet(x = x.train, y = y.train, alpha = 0.5)
```

```
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
```

``` r
# Find Lambda
cv_ridge <- cv.glmnet(x = x.train, y = y.train, alpha = 0)
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

``` r
cv_lasso <- cv.glmnet(x = x.train, y = y.train, alpha = 1)
```

```
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
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

``` r
cv_elastic <- cv.glmnet(x = x.train, y = y.train, alpha = 0.5)
```

```
## Warning in storage.mode(xd) <- "double": NAs introduced by coercion
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

``` r
lambda_ridge <- cv_ridge$lambda.min
lambda_lasso <- cv_lasso$lambda.min
lambda_elastic <- cv_elastic$lambda.min

mse_ridge <- mean((predict(ridge_model, s = lambda_ridge, newx = x.train) - y.train)^2)
```

```
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
```

``` r
mse_lasso <- mean((predict(lasso_model, s = lambda_lasso, newx = x.train) - y.train)^2)
```

```
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
```

``` r
mse_elastic <- mean((predict(elastic_model, s = lambda_elastic, newx = x.train) - y.train)^2)
```

```
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
```

``` r
# Predict Based on Lasso
x.test <- imputed_test |>
  ungroup() |>
  select(state, all_of(paste0("poll_weeks_left_", 7:30)), pv_lag1.x, pv_lag2.x, 32:38, incumbent, incumbent_party, prev_admin) |>
  as.matrix()

(lasso_pred <- predict(lasso_model, s = lambda_lasso, newx = x.test))
```

```
## Warning in cbind2(1, newx) %*% nbeta: NAs introduced by coercion
```

```
##             s1
##  [1,] 41.83713
##  [2,] 45.60474
##  [3,] 46.59710
##  [4,] 41.06774
##  [5,] 68.12996
##  [6,] 51.53312
##  [7,] 53.23382
##  [8,] 52.88124
##  [9,] 45.40468
## [10,] 46.68903
## [11,] 55.64800
## [12,] 40.64393
## [13,] 53.28533
## [14,] 44.80911
## [15,] 46.49194
## [16,] 44.86862
## [17,] 41.84447
## [18,] 43.67264
## [19,] 49.67699
## [20,] 55.99967
## [21,] 56.03615
## [22,] 48.49331
## [23,] 50.15949
## [24,] 44.11851
## [25,] 44.99848
## [26,] 44.36682
## [27,] 43.61105
## [28,] 48.36436
## [29,] 50.59507
## [30,] 52.52036
## [31,] 51.23518
## [32,] 57.18693
## [33,] 46.26312
## [34,] 39.92839
## [35,] 43.19598
## [36,] 39.73707
## [37,] 52.31933
## [38,] 48.19639
## [39,] 53.39552
## [40,] 45.32680
## [41,] 41.82678
## [42,] 42.27562
## [43,] 42.31858
## [44,] 42.64192
## [45,] 55.81922
## [46,] 52.80916
## [47,] 53.22460
## [48,] 38.59206
## [49,] 47.85968
## [50,] 37.29438
```

``` r
# Create a state-level map based on predictions
```

``` r
ec_nodc <- 
  ec |>
  filter(year == 2024 & stateab != "DC")
```








