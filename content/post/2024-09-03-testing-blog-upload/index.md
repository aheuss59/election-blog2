---
title: Testing Blog Upload
author: Alex Heuss
date: '2024-09-05'
slug: testing-blog-upload
categories: [election-prediction]
tags: [president]
---


This is my first blog post, for the week of September 2nd. The primary method of prediction for this week is a model based on the results of the past two elections. 



``` r
nat_wide <- 
  nat_data |> 
  select(year, party, pv2p) |>
  pivot_wider(names_from = party, values_from = pv2p) |>
  mutate(winner = ifelse(republican > democrat, "republican", "democrat"))
```


``` r
nat_wide |> 
  group_by(winner) |>
  summarize(races_won = n())
```

```
## # A tibble: 2 × 2
##   winner     races_won
##   <chr>          <int>
## 1 democrat          11
## 2 republican         8
```
One thing I take away from this chart is how little data we actually have to train prediction models on. There have only been 19 presidential elections since 1948.


``` r
my_theme <- theme_bw() + theme(legend.position = "none")

options(repr.plot.width=20, repr.plot.height=8)

nat_data |>
  ggplot(aes(x = year, y = pv2p, color = party)) +
  geom_line() +
  scale_color_manual(values = c("#00AEF3", "#E81B23")) + 
  labs(x = "", y = "% Two Party Vote Share", title = "Presidential Two Party Vote Share") + 
  my_theme
```

<img src="{{< blogdown/postref >}}index_files/figure-html/bar chart-1.png" width="672" />







