---
title: Testing Blog Upload
author: Alex Heuss
date: '2024-09-05'
slug: testing-blog-upload
categories: [election-prediction]
tags: [president]
---

``` r
library(ggplot2)
library(tidyverse)
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.4     ✔ readr     2.1.5
## ✔ forcats   1.0.0     ✔ stringr   1.5.1
## ✔ lubridate 1.9.3     ✔ tibble    3.2.1
## ✔ purrr     1.0.2     ✔ tidyr     1.3.1
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

This is my first blog post, for the week of September 2nd. The primary method of prediction for this week is a model based on the results of the past two elections. 


``` r
# The code for this post is heavily based on the code that was introduced in section this week. 

nat_data <- read_csv("popvote_1948-2020.csv")
```

```
## Rows: 38 Columns: 9
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (2): party, candidate
## dbl (3): year, pv, pv2p
## lgl (4): winner, incumbent, incumbent_party, prev_admin
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

``` r
state_data <- read_csv("clean_wide_state_2pv_1948_2020.csv")
```

```
## Rows: 959 Columns: 14
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): state
## dbl (13): year, D_pv, R_pv, D_pv2p, R_pv2p, D_pv_lag1, R_pv_lag1, D_pv2p_lag...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

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
my_theme <- theme_bw()

nat_data |>
  ggplot(aes(x = year, y = pv2p, color = party)) +
  geom_line() +
  scale_color_manual(values = c("#00AEF3", "#E81B23")) + 
  labs(x = "", y = "% Two Party Vote Share", title = "Presidential Two Party Vote Share") + 
  my_theme
```

<img src="{{< blogdown/postref >}}index_files/figure-html/bar chart-1.png" width="672" />







