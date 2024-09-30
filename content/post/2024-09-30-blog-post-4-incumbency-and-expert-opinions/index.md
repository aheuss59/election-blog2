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


```
## Warning: One or more parsing issues, call `problems()` on your data frame for details,
## e.g.:
##   dat <- vroom(...)
##   problems(dat)
```




```
## 
##  iter imp variable
##   1   1  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20*  poll_weeks_left_21*  poll_weeks_left_22*  poll_weeks_left_23*  poll_weeks_left_24*  poll_weeks_left_25*  poll_weeks_left_26*  poll_weeks_left_27*  poll_weeks_left_28*  poll_weeks_left_29*  poll_weeks_left_30*  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   1   2  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20*  poll_weeks_left_21*  poll_weeks_left_22*  poll_weeks_left_23*  poll_weeks_left_24*  poll_weeks_left_25*  poll_weeks_left_26  poll_weeks_left_27*  poll_weeks_left_28*  poll_weeks_left_29*  poll_weeks_left_30*  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   1   3  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22*  poll_weeks_left_23*  poll_weeks_left_24*  poll_weeks_left_25*  poll_weeks_left_26*  poll_weeks_left_27*  poll_weeks_left_28*  poll_weeks_left_29*  poll_weeks_left_30*  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   1   4  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20*  poll_weeks_left_21*  poll_weeks_left_22*  poll_weeks_left_23*  poll_weeks_left_24*  poll_weeks_left_25*  poll_weeks_left_26*  poll_weeks_left_27*  poll_weeks_left_28*  poll_weeks_left_29*  poll_weeks_left_30*  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   1   5  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20*  poll_weeks_left_21  poll_weeks_left_22*  poll_weeks_left_23*  poll_weeks_left_24*  poll_weeks_left_25*  poll_weeks_left_26*  poll_weeks_left_27*  poll_weeks_left_28*  poll_weeks_left_29*  poll_weeks_left_30*  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   2   1  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   2   2  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   2   3  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   2   4  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   2   5  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
##   3   1  poll_weeks_left_1  poll_weeks_left_2  poll_weeks_left_3  poll_weeks_left_4  poll_weeks_left_5  poll_weeks_left_6  poll_weeks_left_7  poll_weeks_left_8  poll_weeks_left_9  poll_weeks_left_10  poll_weeks_left_11  poll_weeks_left_12  poll_weeks_left_13  poll_weeks_left_14  poll_weeks_left_15  poll_weeks_left_16  poll_weeks_left_17  poll_weeks_left_18  poll_weeks_left_19  poll_weeks_left_20  poll_weeks_left_21  poll_weeks_left_22  poll_weeks_left_23  poll_weeks_left_24  poll_weeks_left_25  poll_weeks_left_26  poll_weeks_left_27  poll_weeks_left_28  poll_weeks_left_29  poll_weeks_left_30  pv  two_party_vote_share  pv_lag1  pv_lag2  two_party_lag1  two_party_lag2  avg_state_unemployment
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
## Warning: Number of logged events: 979
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


```
##             s1
##  [1,] 54.22644
##  [2,] 58.06758
##  [3,] 59.88113
##  [4,] 53.29359
##  [5,] 83.19077
##  [6,] 64.23696
##  [7,] 65.15550
##  [8,] 65.49650
##  [9,] 59.63305
## [10,] 61.67520
## [11,] 68.17131
## [12,] 53.15172
## [13,] 64.67791
## [14,] 56.37092
## [15,] 58.20438
## [16,] 56.73672
## [17,] 54.07557
## [18,] 55.86345
## [19,] 61.80430
## [20,] 68.80147
## [21,] 68.14579
## [22,] 61.25555
## [23,] 63.63441
## [24,] 56.44319
## [25,] 56.59660
## [26,] 56.88310
## [27,] 55.52649
## [28,] 62.54096
## [29,] 63.87904
## [30,] 64.10425
## [31,] 63.84917
## [32,] 66.96763
## [33,] 60.82926
## [34,] 51.76517
## [35,] 52.11842
## [36,] 52.11345
## [37,] 64.95087
## [38,] 60.49852
## [39,] 65.28104
## [40,] 57.69631
## [41,] 53.67712
## [42,] 54.68842
## [43,] 58.78626
## [44,] 55.59886
## [45,] 68.41521
## [46,] 65.37937
## [47,] 65.69137
## [48,] 50.81583
## [49,] 60.88042
## [50,] 49.76052
```

In my model, I took a shot at imputations for missing values and, as can be seen in the map below, I likely made some poor decisions. Namely, for missing state polling values in the year 2024, I imputed the average polling score for that week in the state's region (Northeast, Midwest, South, and West). There is definitely more variety to a state's polling averages than just what is common in their region. Geographical regions alone were definitely not a sound imputation technique. In the future, I hope to be able to perform something similar, but maybe by blocking states together based on voting history, as opposed to geographic proximity. 

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />








