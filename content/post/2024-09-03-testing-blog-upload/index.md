---
title: Election Forecast 1
author: Alex Heuss
date: '2024-09-05'
slug: testing-blog-upload
categories: [election-prediction]
tags: [president]
---


## General Exploration

This is my first blog post, for the week of September 2nd. The primary method of prediction for this week is a model based on the results of the past two presidential elections, 2016 and 2020. 





Table: <span id="tab:unnamed-chunk-1"></span>Table 1: Presidential races won by each party since 1948

|Party      | Races Won|
|:----------|---------:|
|Democrat   |        11|
|Republican |         8|

As shown in the table, Democratic presidential candidates have won the popular vote in 11 of the past 19 elections, and Republican candidates 8. Another takeaway from this exploratory table is how little data there actually is to train models on. There have only been 19 presidential elections since 1948, which means that the impacts of outliers in the data may be extra large. 

The graph below maps the two-party vote share for the Democratic and Republic parties since 1948. 

<img src="{{< blogdown/postref >}}index_files/figure-html/bar chart-1.png" width="672" />

## 2020 State Maps and Predictions Based on Them


``` r
states_map <- map_data("state")
state_data <- 
  state_data |>
  mutate(region = tolower(state))

pv_map <- 
  state_data |>
  filter(year == 2020) |>
  left_join(states_map, by = "region")

pv_map |> 
  ggplot(aes(long, lat, group = group)) +
  geom_polygon(aes(fill = R_pv2p), color = "white")+
  scale_fill_gradient(low = "white", high = rep_red) +
  theme_void()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />

``` r
pv_map_winner <- 
  pv_map |>
  mutate(winner = ifelse(R_pv > D_pv, "republican", "democrat"))

pv_map_winner |>  
  ggplot(aes(long, lat, group = group)) +
  geom_polygon(aes(fill = winner), color = "white") +
  scale_fill_manual(values=dem_rep) +
  theme_void()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

``` r
pv_map_margin <- 
  pv_map_winner |>
  mutate(margin = R_pv2p-D_pv2p)

pv_map_margin |>
  ggplot(aes(long, lat, group = group)) +
  geom_polygon(aes(fill = margin), color = "black") +
  scale_fill_gradient2(high = rep_red,
                       mid = "white",
                       name = "win margin",
                       low = dem_blue,
                       breaks = c(-50,-25,0,25,50),limits=c(-50,50)) +
  theme_void()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />

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
  geom_polygon(aes(fill = margin_2024), color = "black") +
  ggtitle("2024 Presidential Forecast (Simplified Electoral Cycle Model)") + 
  scale_fill_gradient2(high = rep_red, 
                       mid = "white",
                       name = "win margin",
                       low = dem_blue, 
                       breaks = c(-50,-25,0,25,50), 
                       limits=c(-50,50)) + 
  theme_void()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />












