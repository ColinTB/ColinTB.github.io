This notebook shows some simple code to create and work with overlapping groups in a tidyverse framework.

This is based on a questions I originally asked [here](https://stackoverflow.com/questions/42933058/summarizing-with-overlapping-groups-using-dplyr).

------------------------------------------------------------------------

1. Example data
---------------

Lets use the famous iris data set as an example. This is data on flowers and their measurements.

``` r
library(tidyverse)
```

    ## Loading tidyverse: ggplot2
    ## Loading tidyverse: tibble
    ## Loading tidyverse: tidyr
    ## Loading tidyverse: readr
    ## Loading tidyverse: purrr
    ## Loading tidyverse: dplyr

    ## Conflicts with tidy packages ----------------------------------------------

    ## filter(): dplyr, stats
    ## lag():    dplyr, stats

``` r
glimpse(iris)
```

    ## Observations: 150
    ## Variables: 5
    ## $ Sepal.Length <dbl> 5.1, 4.9, 4.7, 4.6, 5.0, 5.4, 4.6, 5.0, 4.4, 4.9,...
    ## $ Sepal.Width  <dbl> 3.5, 3.0, 3.2, 3.1, 3.6, 3.9, 3.4, 3.4, 2.9, 3.1,...
    ## $ Petal.Length <dbl> 1.4, 1.4, 1.3, 1.5, 1.4, 1.7, 1.4, 1.5, 1.4, 1.5,...
    ## $ Petal.Width  <dbl> 0.2, 0.2, 0.2, 0.2, 0.2, 0.4, 0.3, 0.2, 0.2, 0.1,...
    ## $ Species      <fctr> setosa, setosa, setosa, setosa, setosa, setosa, ...

2. Simple Summary
-----------------

It is easy to summarize across Species. For example the average sepal and petal length by species.

``` r
iris %>% 
  group_by(Species) %>% 
  summarize_at(vars(Sepal.Length, Petal.Length), mean)
```

    ## # A tibble: 3 x 3
    ##      Species Sepal.Length Petal.Length
    ##       <fctr>        <dbl>        <dbl>
    ## 1     setosa        5.006        1.462
    ## 2 versicolor        5.936        4.260
    ## 3  virginica        6.588        5.552

2. Overlapping group summaries
------------------------------

Now lets suppose we want to summarize with overlapping groups. We now want summary figures across all groups, and just Setosa and Versicolor.

``` r
iris %>% 
  mutate(`All Species` = T,
         `Setosa & Versicolour` = Species %in% c("setosa", "versicolor")) %>% 
  gather(group, keep, `All Species`, `Setosa & Versicolour`) %>% 
  filter(keep) %>% 
  group_by(group) %>% 
  summarize_at(vars(Sepal.Length, Petal.Length), mean)
```

    ## # A tibble: 2 x 3
    ##                  group Sepal.Length Petal.Length
    ##                  <chr>        <dbl>        <dbl>
    ## 1          All Species     5.843333        3.758
    ## 2 Setosa & Versicolour     5.471000        2.861

And that's it. Done!
