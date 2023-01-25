Lab 01 - Hello R
================
YG
1/23/2023

## Load packages and data

``` r
library(tidyverse) 
library(datasauRus)
```

## Exercises

### Exercise 1

``` r
dim(datasaurus_dozen)
```

    ## [1] 1846    3

``` r
datasaurus_dozen$dataset<-as.factor(datasaurus_dozen$dataset)
summary(datasaurus_dozen)
```

    ##      dataset          x               y           
    ##  away    :142   Min.   :15.56   Min.   : 0.01512  
    ##  bullseye:142   1st Qu.:41.07   1st Qu.:22.56107  
    ##  circle  :142   Median :52.59   Median :47.59445  
    ##  dino    :142   Mean   :54.27   Mean   :47.83510  
    ##  dots    :142   3rd Qu.:67.28   3rd Qu.:71.81078  
    ##  h_lines :142   Max.   :98.29   Max.   :99.69468  
    ##  (Other) :994

``` r
table(datasaurus_dozen$dataset)
```

    ## 
    ##       away   bullseye     circle       dino       dots    h_lines high_lines 
    ##        142        142        142        142        142        142        142 
    ## slant_down   slant_up       star    v_lines wide_lines    x_shape 
    ##        142        142        142        142        142        142

### Exercise 2

First let’s plot the data in the dino dataset:

``` r
dino_data <- datasaurus_dozen %>%
  filter(dataset == "dino")

ggplot(data = dino_data, mapping = aes(x = x, y = y)) +
  geom_point()
```

![](lab-01-hello-r_files/figure-gfm/plot-dino-1.png)<!-- -->

And next calculate the correlation between `x` and `y` in this dataset:

``` r
dino_data %>%
  summarize(r = cor(x,y))
```

    ## # A tibble: 1 × 1
    ##         r
    ##     <dbl>
    ## 1 -0.0645

### Exercise 3

Plot the star dataset.

``` r
star_data<-datasaurus_dozen %>%
  filter(dataset == "star")

ggplot(data = star_data, mapping = aes(x=x, y=y)) +
  geom_point()
```

![](lab-01-hello-r_files/figure-gfm/plot-star-1.png)<!-- -->

Calculate the correlation between x and y for the star dataset.

``` r
star_data %>%
  summarize(r = cor(x,y))
```

    ## # A tibble: 1 × 1
    ##         r
    ##     <dbl>
    ## 1 -0.0630

The dino data set has higher correlation than the star data set.

\### Exercise 4

Plot the circle dataset.

``` r
circle_data <- datasaurus_dozen %>%
  filter(dataset == "circle")

ggplot(data = circle_data, mapping = aes(x=x, y=y)) +
  geom_point()
```

![](lab-01-hello-r_files/figure-gfm/plot-circle-1.png)<!-- -->

``` r
circle_data %>%
  summarize(r = cor(x,y))
```

    ## # A tibble: 1 × 1
    ##         r
    ##     <dbl>
    ## 1 -0.0683

The circle data set has a higher correlation than the dino data set.

### Exercise 5

``` r
ggplot(datasaurus_dozen, aes(x=x, y=y, color = dataset)) + 
  geom_point() +
  facet_wrap(~dataset, ncol = 3) +
  theme(legend.position = "none")
```

![](lab-01-hello-r_files/figure-gfm/plot%20the%20entire%20data%20set-1.png)<!-- -->

``` r
datasaurus_dozen %>%
  group_by(dataset) %>%
  summarize(r = cor(x,y)) %>%
  print(13)
```

    ## # A tibble:
    ## #   13 × 2
    ##    dataset   
    ##    <fct>     
    ##  1 away      
    ##  2 bullseye  
    ##  3 circle    
    ##  4 dino      
    ##  5 dots      
    ##  6 h_lines   
    ##  7 high_lines
    ##  8 slant_down
    ##  9 slant_up  
    ## 10 star      
    ## 11 v_lines   
    ## 12 wide_lines
    ## 13 x_shape   
    ## # … with 1
    ## #   more
    ## #   variable:
    ## #   r <dbl>
