
<!-- README.md is generated from README.Rmd. Please edit that file -->
sugrrants
=========

[![Travis-CI Build Status](https://travis-ci.org/earowang/sugrrants.svg?branch=master)](https://travis-ci.org/earowang/sugrrants) [![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version/sugrrants)](https://cran.r-project.org/package=sugrrants)

Overview
--------

The goal of *sugrrants* is to provide supporting graphics with R for analysing time series data. It aims to fit into the *tidyverse* and grammar of graphics framework for handling temporal data. The package is under development and highly experimental at this stage. Bug reporting and feature suggestions are welcome.

Installation
------------

You could install the development version from Github using

``` r
# install.packages("devtools")
devtools::install_github("earowang/sugrrants", build_vignettes = TRUE)
```

Usage
-----

### Calendar-based graphics

``` r
library(dplyr)
library(sugrrants)

calendar_df <- pedestrian %>%
  filter(Sensor_ID == 9, Year == 2016) %>%
  mutate(
    Weekend = if_else(Day %in% c("Saturday", "Sunday"), "Weekend", "Weekday")
  ) %>%
  frame_calendar(
    x = Time, y = Hourly_Counts, date = Date, calendar = "monthly"
  )
calendar_df
#> # A tibble: 8,780 x 15
#>          .cx       .cy           Date_Time  Year   Month Mdate    Day
#>  *     <dbl>     <dbl>              <dttm> <int>   <ord> <int>  <ord>
#>  1 0.1842593 0.9648148 2016-01-01 00:00:00  2016 January     1 Friday
#>  2 0.1842593 0.9648148 2016-01-01 01:00:00  2016 January     1 Friday
#>  3 0.1842593 0.9648148 2016-01-01 02:00:00  2016 January     1 Friday
#>  4 0.1842593 0.9648148 2016-01-01 03:00:00  2016 January     1 Friday
#>  5 0.1842593 0.9648148 2016-01-01 04:00:00  2016 January     1 Friday
#>  6 0.1842593 0.9648148 2016-01-01 05:00:00  2016 January     1 Friday
#>  7 0.1842593 0.9648148 2016-01-01 06:00:00  2016 January     1 Friday
#>  8 0.1842593 0.9648148 2016-01-01 07:00:00  2016 January     1 Friday
#>  9 0.1842593 0.9648148 2016-01-01 08:00:00  2016 January     1 Friday
#> 10 0.1842593 0.9648148 2016-01-01 09:00:00  2016 January     1 Friday
#> # ... with 8,770 more rows, and 8 more variables: Time <int>,
#> #   Sensor_ID <int>, Sensor_Name <chr>, Hourly_Counts <int>,
#> #   Weekend <chr>, Date <date>, .Time <dbl>, .Hourly_Counts <dbl>
```

``` r
p <- calendar_df %>%
  ggplot(aes(x = .Time, y = .Hourly_Counts, group = Date, colour = Weekend)) +
  geom_line() +
  theme(legend.position = "none")
prettify(p)
```

![](man/figure/calendar-plot-1.png)

Miscellaneous
-------------

The acronym of *sugrrants* is **SU**pporting **GR**aphics with **R** for **AN**alysing **T**ime **S**eries, pronounced as "sugar ants" that are a species of ant endemic to Australia.
