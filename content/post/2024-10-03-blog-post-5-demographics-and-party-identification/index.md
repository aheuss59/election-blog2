---
title: 'Blog Post 5: Demographics and Party Identification'
author: Alex Heuss
date: '2024-10-03'
slug: blog-post-5-demographics-and-party-identification
categories: []
tags: []
---



## Discussion of the Predicitive Power of Demographics and Party ID

In class this week, we discussed the power of demographic variables in predicting election outcomes. The paper we read this week, Kim & Zilinsky's "Division does not imply predictability: Demographics
continue to reveal little about voting and partisanship", provided empirical evidence that demographic data can predict vote choice with an accuracy of approximately 63%. They also found though that party is more predictive, especially when combined with demographics. This motivates my own theory of the importance of partisan identification.

My theory around election prediction involves a rather pessimistic belief that a person's vote, especially in recent elections, can likely be fairly accurately predicted by partisan identification alone. I believe that the country has become increasingly polarized and that people vote based on their party more than other factors like the economy or a candidate's particular policies. 

I found and cleaned data for both national (Gallup and Pew Research) and state (ANES estimates) party identification historically. The graph below shows the relationship between national party ID "swing" between the year before an election and election year and the national popular vote. The "swing" measure attempts to get a feel for party momentum going into the election year. 




```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
## One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```





<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />

This graph shows, intuitively, a rough positive correlation. Generally, when party identification is changing in a positive direction between the year prior to the election and the election itself (momentum), the vote share for that party is higher. 

Looking at the relationship between partisan identification and popular vote on the state level, the relationship between party identification swing and popular vote in the state is much less conclusive.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

Trends between partisan swing and state popular vote differ a lot between states. Michigan and Ohio would imply that there might be a small positive correlation, while Georgia would suggest just the opposite. This would imply that perhaps party identification is more predictive of national popular vote than state popular vote. 



## National Popular Vote Predictions

For predictions this week, I make an effort to predict both national popular vote share and the electoral college outcome. 

For national popular vote, I used lasso to make a prediction based on the predictors that we've discussed in previous classes (the economy, incumbency, polling) and this week I added national party identification. 


```
##            s1
## [1,] 48.91190
## [2,] 48.07179
```
The lasso regression found the popular vote to be extremely tight, with Kamala Harris receiving 48.91% and Donald Trump receiving 48.07%. 


```
## 50 x 1 sparse Matrix of class "dgCMatrix"
##                             s1
## (Intercept)       19.049104982
## party              .          
## incumbent          .          
## incumbent_party    .          
## prev_admin         .          
## deminc             .          
## juneapp            .          
## percent            .          
## two_party_percent  .          
## ind_percent       -0.078484476
## year_prior         .          
## year_prior_2p      .          
## swing1             0.198030467
## swing1_2p          .          
## prior_election     .          
## prior_election_2p -0.004282676
## swing4             .          
## swing4_2p          .          
## nat_weeks_left_5   0.415767672
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
## nat_weeks_left_18  0.286791505
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

In the national popular vote predictions, Lasso selected the percent of independents in the country, the swing in party ID from the year prior to the election to the election year, the two party party identification from the previous election, the most recent week of polling, and one earlier week of polling as the most valuable predictors for national popular vote. This would support my theory that party identification may be very important in predicting election outcomes. 

Unfortunately, I spent a lot of time this week compiling and cleaning party identification data and analyzing it's possible impact. Despite many attempts, I was unsuccessful in incorporating it into a state-level model to predict the electoral college this week. I look forward to incorporating party into my state prediction model next week, now that I have the data wrangled and cleaned. 










