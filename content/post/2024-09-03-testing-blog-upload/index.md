---
title: Election Forecast 1
author: Alex Heuss
date: '2024-09-05'
slug: testing-blog-upload
categories: [election-prediction]
tags: [president]
---


## General Exploration

This is my first blog post, for the week of September 2nd. The primary method of prediction for this week is a simple model based on the results of the past two presidential elections, 2016 and 2020. 






Table: <span id="tab:unnamed-chunk-1"></span>Table 1: Presidential races won by each party since 1948

|Party      | Races Won|
|:----------|---------:|
|Democrat   |        11|
|Republican |         8|

As shown in the table, Democratic presidential candidates have won the popular vote in 11 of the past 19 elections, and Republican candidates 8. Another takeaway from this exploratory table is how little data there actually is to train models on. There have only been 19 presidential elections since 1948, which means that the impacts of outliers in the data may be extra large. 

The graph below maps the two-party vote share for the Democratic and Republican parties since 1948. 

<img src="{{< blogdown/postref >}}index_files/figure-html/bar chart-1.png" width="672" />

Two-party vote share as a statistic measures the percentage of the vote that either party gets among only voters who voted for the Democratic or Republican candidate (and as such does not include third part votes). A key takeaway from this graph is that the difference in vote shares has narrowed since the 1990s; elections have become a lot closer. 

## 2020 Electoral Maps




<img src="{{< blogdown/postref >}}index_files/figure-html/map of popular vote winner-1.png" width="672" />



``` r
pv_map_margin <- 
  pv_map_winner |>
  mutate(margin = R_pv2p-D_pv2p)

pv_map_margin |>
  ggplot(aes(long, lat, group = group)) +
  geom_polygon(aes(fill = margin), color = "gray") +
  scale_fill_gradient2(high = rep_red,
                       mid = "white",
                       name = "Win Margin",
                       low = dem_blue,
                       breaks = c(-50,-25,0,25,50),limits=c(-50,50)) +
  labs(title = "2020 Two-Party Popular Vote Margin by State") +
  my_map_theme 
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />

``` r
state_2p <- 
  state_data |> 
  filter(year == 2020) |>
  group_by(state) |> 
  summarise(D_2024_2p = 0.75*D_pv2p + 0.25*D_pv2p_lag1,
            R_2024_2p = 0.75*R_pv2p + 0.25*R_pv2p_lag1) |>
  mutate(margin_2024 = R_2024_2p - D_2024_2p,
         region = tolower(state))

state_2p |>
  left_join(states_map, by = "region") |>
  ggplot(aes(long, lat, group = group)) +
  geom_polygon(aes(fill = margin_2024), color = "grey") +
  labs(title = "Simple 2024 Election Forecast") + 
  scale_fill_gradient2(high = rep_red, 
                       mid = "white",
                       name = "Win Margin",
                       low = dem_blue, 
                       breaks = c(-50,-25,0,25,50), 
                       limits=c(-50,50)) + 
  my_map_theme
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />












