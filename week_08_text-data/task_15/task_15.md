---
title: "TASK 15"
author: "Adam Nielsen"
date: "February 23, 2021"
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
rletters <- read_lines("https://byuistats.github.io/M335/data/randomletters.txt")
rletters_plus <- read_lines("https://byuistats.github.io/M335/data/randomletters_wnumbers.txt")
```

## Background

_Place Task Background Here_

## Data Wrangling


```r
# Use this R-Chunk to clean & wrangle your data!
seq1700 <- seq(0, str_length(rletters), 1700)
seq1700[1] = 1
every1700 <- rletters %>%
  str_sub(start = seq1700, end = seq1700)

every1700
```

```
##  [1] "t" "h" "e" " " "p" "l" "u" "r" "a" "l" " " "o" "f" " " "a" "n" "e" "c" "d"
## [20] "o" "t" "e" " " "i" "s" " " "n" "o" "t" " " "d" "a" "t" "a" "." "z" " " "a"
## [39] "n" "f" "r" "a"
```

```r
num_to_letter <- rletters_plus %>%
  str_extract_all("\\d+") %>%
  unlist()

num_to_letter <- LETTERS[as.numeric(num_to_letter)]

num_to_letter
```

```
##  [1] "E" "X" "P" "E" "R" "T" "S" "O" "F" "T" "E" "N" "P" "O" "S" "S" "E" "S" "S"
## [20] "M" "O" "R" "E" "D" "A" "T" "A" "T" "H" "A" "N" "J" "U" "D" "G" "M" "E" "N"
## [39] "T"
```

```r
vowels <- rletters %>%
  str_remove_all("\ |\\.") %>%
  str_extract_all("[aeiou]+") %>%
  unlist() %>%
  .[which.max(str_length(.))]

vowels
```

```
## [1] "oaaoooo"
```

## Data Visualization


```r
# Use this R-Chunk to plot & visualize your data!
```

## Conclusions
