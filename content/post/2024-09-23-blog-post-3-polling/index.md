---
title: 'Blog Post 3: Polling'
author: Alex Heuss
date: '2024-09-23'
slug: blog-post-3-polling
categories: []
tags: []
---




## Historic Accuracy of Polls

Poll averages seem like an intuitive way to predict elections - intuitively, if I walk around and ask everyone who they are going to vote for, I should get a pretty good idea of how many people are voting for each candidate. However, historically, polls become more accurate as the election approaches, often converging near the correct value within a week or so of the election. Several theories attempt to explain this, including the "enlightened blah blah" theory expressed by so and so in their book *book*.

The following graph shows differences between polls and actual popular vote over the thirty-six weeks leading up the election from 2000-2020. 




<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-1.png" width="672" />
Interpreting this graph, a perfect poll prediction would be at the line y = 0, which marks no difference between the poll predictions and the true popular vote. A difference above the line means that the winner was over-predicted to win and below marks an under-prediction. We can see that, in general, poll estimates are approaching zero as the election draws near. Another trend is that winners are often under-predicted. Notably, many polls, especially in recent years are also fairly accurate to begin with, with starting measures ending up very close to the end measure and variation in the middle. One reason for this may be that, because Americans are increasingly partisan, their views may change less over the course of the campaign.

The following graph visualizes the last poll prediction prior to the election and it's correlation with the actual result.


```
## `geom_smooth()` using formula = 'y ~ x'
```

<img src="{{< blogdown/postref >}}index_files/figure-html/graph last poll preds and the actual result-1.png" width="672" />
In general, the final poll result is very similar to the true election popular vote. This graph also shows the tendency of polls to under-predict the true popular vote, which may be due to the influence of third parties. Perhaps, voters who are questioned by pollsters are more likely to say they will be voting for a third party candidate than to actually do it. 

# 2024 Polls Thus Far

In predicting the 2024 election, we in some ways have less polling data to work with, owing to Biden's late-in-the-game dropout.

<img src="{{< blogdown/postref >}}index_files/figure-html/2024 nat polls graph-1.png" width="672" />


## State Level




