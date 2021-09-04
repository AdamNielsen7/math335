---
title: "Exploratory Data Analysis"
author: "YOUR NAME"
date: "January 12, 2021"
output:
  html_document:  
    keep_md: true
    toc: true
    toc_float: true
    fig_height: 6
    fig_width: 12
    fig_align: 'center'
---



## Reading Notes

- EDA = Exploratory Data Analysis
- “Far better an approximate answer to the right question, which is often vague, than an exact answer to the wrong question, which can always be made precise.” — John Tukey

2 main questions  
- What type of variation occurs within my variables?  
- What type of covariation occurs between my variables?  

**Variation**  
categorical bar chart  
*ggplot(data = diamonds) +*  
  *geom_bar(mapping = aes(x = cut))*  
  
count the number in each category  
*diamonds %>%*  
  *count(cut)*  
  
continuous histogram  
*ggplot(data = diamonds) +*  
  *geom_histogram(mapping = aes(x = carat), binwidth = 0.5)*  
  
continuous count using "bins"  
*diamonds %>% *  
 *count(cut_width(carat, 0.5))*  
 
overlapping histograms use freqpoly for better visualization  
*ggplot(data = smaller, mapping = aes(x = carat, colour = cut)) +*  
  *geom_freqpoly(binwidth = 0.1)*  
  
- Which values are the most common? Why?  
- Which values are rare? Why? Does that match your expectations?  
- Can you see any unusual patterns? What might explain them?  

zoom into a plot with coord_cartesian  
*ggplot(diamonds) +*   
  *geom_histogram(mapping = aes(x = y), binwidth = 0.5) +*  
  *coord_cartesian(ylim = c(0, 50))*  

replace bad data using mutate and ifelse  
*diamonds2 <- diamonds %>% *  
  *mutate(y = ifelse(y < 3 | y > 20, NA, y))*  

-Why are these values missing?  
*mutate df to make seperate category?*  

**Covariation**  
use a density plot to standardize data between categories  
*ggplot(data = diamonds, mapping = aes(x = price, y = ..density..)) +   
  geom_freqpoly(mapping = aes(colour = cut), binwidth = 500)*  
  
boxplots are cool  
*ggplot(data = diamonds, mapping = aes(x = cut, y = price)) +  
  geom_boxplot()*
  



## EDA Example

The code below is an example of the EDA process using the `starwars` data from the `tidyverse` package. (Make sure you have the `tidyverse` package installed!)

Run the code line-by-line and look at the output. Add a comment to each line of code that explains what it does/what insights it provides.


```r
library(tidyverse)

dim(starwars) #returns the dimensions of starwars
```

```
## [1] 87 14
```

```r
colnames(starwars) # returns the column names of starwars
```

```
##  [1] "name"       "height"     "mass"       "hair_color" "skin_color"
##  [6] "eye_color"  "birth_year" "sex"        "gender"     "homeworld" 
## [11] "species"    "films"      "vehicles"   "starships"
```

```r
head(starwars) # a small preview of the df
```

```
## # A tibble: 6 x 14
##   name  height  mass hair_color skin_color eye_color birth_year sex   gender
##   <chr>  <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
## 1 Luke~    172    77 blond      fair       blue            19   male  mascu~
## 2 C-3PO    167    75 <NA>       gold       yellow         112   none  mascu~
## 3 R2-D2     96    32 <NA>       white, bl~ red             33   none  mascu~
## 4 Dart~    202   136 none       white      yellow          41.9 male  mascu~
## 5 Leia~    150    49 brown      light      brown           19   fema~ femin~
## 6 Owen~    178   120 brown, gr~ light      blue            52   male  mascu~
## # ... with 5 more variables: homeworld <chr>, species <chr>, films <list>,
## #   vehicles <list>, starships <list>
```

```r
glimpse(starwars) # the df by column
```

```
## Rows: 87
## Columns: 14
## $ name       <chr> "Luke Skywalker", "C-3PO", "R2-D2", "Darth Vader", "Leia...
## $ height     <int> 172, 167, 96, 202, 150, 178, 165, 97, 183, 182, 188, 180...
## $ mass       <dbl> 77.0, 75.0, 32.0, 136.0, 49.0, 120.0, 75.0, 32.0, 84.0, ...
## $ hair_color <chr> "blond", NA, NA, "none", "brown", "brown, grey", "brown"...
## $ skin_color <chr> "fair", "gold", "white, blue", "white", "light", "light"...
## $ eye_color  <chr> "blue", "yellow", "red", "yellow", "brown", "blue", "blu...
## $ birth_year <dbl> 19.0, 112.0, 33.0, 41.9, 19.0, 52.0, 47.0, NA, 24.0, 57....
## $ sex        <chr> "male", "none", "none", "male", "female", "male", "femal...
## $ gender     <chr> "masculine", "masculine", "masculine", "masculine", "fem...
## $ homeworld  <chr> "Tatooine", "Tatooine", "Naboo", "Tatooine", "Alderaan",...
## $ species    <chr> "Human", "Droid", "Droid", "Human", "Human", "Human", "H...
## $ films      <list> [<"The Empire Strikes Back", "Revenge of the Sith", "Re...
## $ vehicles   <list> [<"Snowspeeder", "Imperial Speeder Bike">, <>, <>, <>, ...
## $ starships  <list> [<"X-wing", "Imperial shuttle">, <>, <>, "TIE Advanced ...
```

```r
?starwars # help and info about df, opens up a html page

starwars %>% count(species) # a count of each species in df
```

```
## # A tibble: 38 x 2
##    species       n
##    <chr>     <int>
##  1 Aleena        1
##  2 Besalisk      1
##  3 Cerean        1
##  4 Chagrian      1
##  5 Clawdite      1
##  6 Droid         6
##  7 Dug           1
##  8 Ewok          1
##  9 Geonosian     1
## 10 Gungan        3
## # ... with 28 more rows
```

```r
mean(starwars$height) #the mean of all heights
```

```
## [1] NA
```

```r
mean(starwars$height, na.rm = TRUE) # the mean of all heights not counting NA values
```

```
## [1] 174.358
```

```r
summary(starwars$height) #basic info for df (min mean max NA count etc)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
##    66.0   167.0   180.0   174.4   191.0   264.0       6
```

```r
# a function that takes in cm and returns the equivelent length in feet
cm_to_ft <- function(cm){ 
  ft = cm / 30.48
  return(ft)
}

#uses cm_to_feet to create a new variable height_ft in df
starwars_2 <- starwars %>% mutate(height_ft = cm_to_ft(height)) 

dim(starwars_2)
```

```
## [1] 87 15
```

```r
colnames(starwars_2)
```

```
##  [1] "name"       "height"     "mass"       "hair_color" "skin_color"
##  [6] "eye_color"  "birth_year" "sex"        "gender"     "homeworld" 
## [11] "species"    "films"      "vehicles"   "starships"  "height_ft"
```

```r
summary(starwars_2$height_ft)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
##   2.165   5.479   5.906   5.720   6.266   8.661       6
```

```r
#a histogram of height_ft
ggplot(starwars_2, aes(height_ft)) + 
  geom_histogram()
```

```
## Warning: Removed 6 rows containing non-finite values (stat_bin).
```

![](task3_template_files/figure-html/unnamed-chunk-2-1.png)<!-- -->

```r
#filter to find the tallest row, na.rm is needed
starwars_2 %>% filter(height_ft == max(height_ft))
```

```
## # A tibble: 0 x 15
## # ... with 15 variables: name <chr>, height <int>, mass <dbl>,
## #   hair_color <chr>, skin_color <chr>, eye_color <chr>, birth_year <dbl>,
## #   sex <chr>, gender <chr>, homeworld <chr>, species <chr>, films <list>,
## #   vehicles <list>, starships <list>, height_ft <dbl>
```

```r
starwars_2 %>% filter(height_ft == max(height_ft, na.rm = TRUE))
```

```
## # A tibble: 1 x 15
##   name  height  mass hair_color skin_color eye_color birth_year sex   gender
##   <chr>  <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
## 1 Yara~    264    NA none       white      yellow            NA male  mascu~
## # ... with 6 more variables: homeworld <chr>, species <chr>, films <list>,
## #   vehicles <list>, starships <list>, height_ft <dbl>
```

```r
# https://starwars.fandom.com/wiki/Yarael_Poof
```

## EDA Practice

Continue exploring the `starwars` data to gain additional insights, using [R4DS: Chapter 7](https://r4ds.had.co.nz/exploratory-data-analysis.html) as a guide.

It is ok if you don't understand the all code in Chapter 7. (That is what we'll be learning the next two weeks!) If writing your own code is a struggle, try the "copy, paste, and tweak" method.


```r
# your code goes here
```
