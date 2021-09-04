---
title: "CASE STUDY TITLE"
author: "YOUR NAME"
date: "March 02, 2021"
output:
  html_document:  
    keep_md: true
    toc: true
    toc_float: true
    code_folding: hide
    fig_height: 6
    fig_width: 12
    fig_align: 'center'
---






```r
# Use this R-Chunk to import all your datasets!
waitlist <- read_csv("https://byuistats.github.io/M335/data/waitlist_DP_108.csv")

waitlist108 <- waitlist %>%
  mutate(date = lubridate::mdy_hms(`Registration Date`)) %>%
  filter(`Course Sec` == "FDMAT108-18")

current_waitlisted <- function(data) {
  x1 <- data %>% filter(Status == "Registered") %>% count()
  x2 <- data %>% filter(`Waitlist Reason` == "Waitlist Registered") %>% count()
  return(x2/x1)
}

waitlist_registered <- function(data) {
  x1 <- data %>% filter(Status == "Registered" & !is.na(`Waitlist Reason`)) %>% count()
  x2 <- data %>% filter(!is.na(`Waitlist Reason`)) %>% count()
  return(x1/x2)
}

current_waitlisted(waitlist108)
```

```
##           n
## 1 0.2077922
```

```r
waitlist_registered(waitlist108)
```

```
##          n
## 1 0.238806
```

## Background

_Place Task Background Here_

## Data Wrangling


```r
# Use this R-Chunk to clean & wrangle your data!
```

## Data Visualization


```r
# Use this R-Chunk to plot & visualize your data!
```

## Conclusions
