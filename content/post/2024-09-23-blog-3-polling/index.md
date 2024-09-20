---
title: 'Blog 3: Polling'
author: Alex Heuss
date: '2024-09-23'
slug: blog-3-polling
categories: []
tags: []
---




## Historic Accuracy of Polls

Poll averages seem like an intuitive way to predict elections - intuitively, if I walk around and ask everyone who they are going to vote for, I should get a pretty good idea of how many people are voting for each candidate. However, historically, polls become more accurate as the election approaches, often converging near the correct value within a week or so of the election. Several theories attempt to explain this, including the "enlightened blah blah" theory expressed by so and so in their book *book*.

[insert a graph of this if possible (picturing a scatterplot with weeks_left on the bottom and difference between poll and actual on the y)]






```
## `geom_smooth()` using formula = 'y ~ x'
```

<img src="{{< blogdown/postref >}}index_files/figure-html/graph last poll preds and the actual result-1.png" width="672" />

## Visualize 2024 Polls

<img src="{{< blogdown/postref >}}index_files/figure-html/2024 nat polls graph-1.png" width="672" />
## State Level



```{r. state data wrangling, echo=FALSE, message=FALSE}
clean_state_polls <- 
  state_av_poll_data |>
  mutate(party = ifelse(party == "DEM", "democrat", "republican"),
         dem_support = ifelse(party == "democrat", poll_support, 0),
         rep_support = ifelse(party == "republican", poll_support, 0)) |>
  select(-party, -candidate, -days_left, -poll_support) |>
  group_by(year, weeks_left, state, poll_date) |>
  summarize(dem_support = sum(dem_support),
            rep_support = sum(rep_support))

merged_state_data <- 
  state_pop_data |>
  filter(year >= 1972) |>
  left_join(clean_state_polls, by = c("state", "year")) |>
  select(year, state, D_pv, R_pv, D_pv2p, R_pv2p, weeks_left, poll_date, dem_support, rep_support) |>
  left_join(ec, by = c("state", "year"))

average_state_data <- 
  merged_state_data |>
  group_by(year, state) |>
  summarize(av_d_pv = mean(D_pv),
            av_r_pv = mean(R_pv),
            av_d_2pv = mean(D_pv2p),
            av_r_2pv = mean(R_pv2p),
            av_d_poll = mean(dem_support, na.rm = TRUE),
            av_r_poll = mean(rep_support, na.rm = TRUE))
  
weekly_state_data <- 
  merged_state_data |>
  group_by(year, state, weeks_left) |>
  summarize(av_d_pv = mean(D_pv),
            av_r_pv = mean(R_pv),
            av_d_2pv = mean(D_pv2p),
            av_r_2pv = mean(R_pv2p),
            av_d_poll = mean(dem_support, na.rm = TRUE),
            av_r_poll = mean(rep_support, na.rm = TRUE))

```







