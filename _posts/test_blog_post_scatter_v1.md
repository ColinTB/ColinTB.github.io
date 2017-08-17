This notebook is to test placing images in markdown.

------------------------------------------------------------------------

1. Example data
---------------

Lets use the famous iris data set as an example. This is data on flowers and their measurements.

``` r
library(tidyverse)
```

    ## Warning: Installed Rcpp (0.12.12) different from Rcpp used to build dplyr (0.12.11).
    ## Please reinstall dplyr to avoid random crashes or undefined behavior.

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

2. Scatter Plot
---------------

This is a simple scatter plot.

``` r
ggplot(iris, aes(y = Sepal.Length, x = Sepal.Width, colour = Species)) +
  geom_point() 
```

![](/images/test_blog_post_scatter_v1_files/figure-markdown_github/unnamed-chunk-2-1.png)
