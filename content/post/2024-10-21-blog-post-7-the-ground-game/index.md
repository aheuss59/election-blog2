---
title: 'Blog Post 7: The Ground Game'
author: Alex Heuss
date: '2024-10-21'
slug: blog-post-7-the-ground-game
categories: []
tags: []
---













## National Popular Vote Prediction

This week, I started by re-running my national popular vote prediction model from past weeks with updated poll numbers from this week. 


```
##            s1
## [1,] 49.06439
## [2,] 47.90759
```

The model's predictions have not changed much from last week, Kamala Harris' popular vote share shrank by about 0.02 percentage points and Donald Trump's grew by 0.001 percentage points. It seems like if I continue to hold my LASSO model constant, the two candidates will probably remain about the same in the popular vote share prediction unless there are significant polling shifts. 

## Electoral College Predictions

In my electoral prediction model this week, I updated the polling data with polls from this week and changed the value I use to represent partisan identification. Last week, I made a mistake in my model and instead of using swing in party identification from one election to the next, I used the partisan identification of the state during the last election. I corrected it in this week's model. I also added a variable for open primaries (states that, in 2024, have a lot more registered independent voters than democrats and republicans combined), and controlled for it in an attempt to minimize the issues with the party identification variable for 2024. 







|Winner     | States Won| Electors|
|:----------|----------:|--------:|
|Democrat   |         21|      263|
|Republican |         29|      272|

Taking a look at the full election results, once again Kamala Harris loses the electoral college. DC is also not included in my model this week, but will almost certainly go to Harris, which would bring teh vote totals to 266 for Harris and 272 for Trump. 

The next table visualizes the swing state breakdown. 


|State          |Winner     |     Margin|
|:--------------|:----------|----------:|
|Michigan       |Democrat   |  3.9852186|
|Pennsylvania   |Democrat   |  1.5026237|
|Wisconsin      |Democrat   |  2.6973706|
|Arizona        |Republican | -2.6033523|
|Georgia        |Republican | -1.3832750|
|Nevada         |Republican | -0.9808848|
|North Carolina |Republican | -4.8247507|

My model predicts Harris to win Michigan, Pennsylvania and Wisconsin while Trump wins Arizona, Georgia, Nevada and North Carolina. 

Finally, here's a look at the full map. 

<img src="{{< blogdown/postref >}}index_files/figure-html/map-1.png" width="672" />

## An Attempt at Lasso Regression for Electoral College Predictions

This week, I also wanted to try using a more sophisticated method for model selection and tried to run a LASSO prediction on my state-level data. After struggling with imputation and matrices for awhile, my model promptly predicted that Kamala Harris would win at least -35,000 percent of the vote share and Donald Trump at least -81,000. Due to the highly inaccurate nature of these predictions, I instead took the features LASSO suggested and fed them back into a linear model. 

This model spit out some possible, but not necessarily realistic estimates for the states that currently have polling data (mostly toss up states or states that lean one way or another). 




|state          | simp_pred_dem| simp_pred_rep|winner     |
|:--------------|-------------:|-------------:|:----------|
|Arizona        |      44.78957|      55.21043|Republican |
|California     |      59.64728|      40.35272|Democrat   |
|Florida        |      42.96216|      57.03784|Republican |
|Georgia        |      45.07681|      54.92319|Republican |
|Maryland       |      61.60806|      38.39194|Democrat   |
|Michigan       |      46.54002|      53.45998|Republican |
|Minnesota      |      48.64447|      51.35553|Republican |
|Missouri       |      38.67503|      61.32497|Republican |
|Montana        |      36.69100|      63.30900|Republican |
|Nebraska       |      35.22582|      64.77418|Republican |
|Nevada         |      46.49182|      53.50818|Republican |
|New Hampshire  |      49.12235|      50.87765|Republican |
|New Mexico     |      50.71686|      49.28314|Democrat   |
|New York       |      54.84929|      45.15071|Democrat   |
|North Carolina |      44.82439|      55.17561|Republican |
|Ohio           |      41.54360|      58.45640|Republican |
|Pennsylvania   |      46.04213|      53.95787|Republican |
|Texas          |      42.15289|      57.84711|Republican |
|Virginia       |      49.65644|      50.34356|Republican |
|Wisconsin      |      45.65095|      54.34905|Republican |

These results would suggest a pretty rough outcome for the Democrats in November. I unfortunately was unable to secure a possible prediction for vote share using the LASSO linear regression coefficients for states without polling data (the Democrats managed negative vote share and the Republicans more than 100). I hope to correct the error in my LASSO model for next week, but this week will have to stick with last week's model detailed in the previous section. 












