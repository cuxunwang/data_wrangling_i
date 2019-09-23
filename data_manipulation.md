Data Manipulation
================
Xun Wang
9/19/2019

## Import datasets

``` r
litters_data = read_csv("./data/FAS_litters.csv",
  col_types = "ccddiiii")
litters_data = janitor::clean_names(litters_data)

pups_data = read_csv("./data/FAS_pups.csv",
  col_types = "ciiiii")
pups_data = janitor::clean_names(pups_data)
```

## Selecting\!\!\!

``` r
select(litters_data, group, litter_number)
```

    ## # A tibble: 49 x 2
    ##    group litter_number  
    ##    <chr> <chr>          
    ##  1 Con7  #85            
    ##  2 Con7  #1/2/95/2      
    ##  3 Con7  #5/5/3/83/3-3  
    ##  4 Con7  #5/4/2/95/2    
    ##  5 Con7  #4/2/95/3-3    
    ##  6 Con7  #2/2/95/3-2    
    ##  7 Con7  #1/5/3/83/3-3/2
    ##  8 Con8  #3/83/3-3      
    ##  9 Con8  #2/95/3        
    ## 10 Con8  #3/5/2/2/95    
    ## # ... with 39 more rows

``` r
select(litters_data, group, litter_number, gd0_weight)
```

    ## # A tibble: 49 x 3
    ##    group litter_number   gd0_weight
    ##    <chr> <chr>                <dbl>
    ##  1 Con7  #85                   19.7
    ##  2 Con7  #1/2/95/2             27  
    ##  3 Con7  #5/5/3/83/3-3         26  
    ##  4 Con7  #5/4/2/95/2           28.5
    ##  5 Con7  #4/2/95/3-3           NA  
    ##  6 Con7  #2/2/95/3-2           NA  
    ##  7 Con7  #1/5/3/83/3-3/2       NA  
    ##  8 Con8  #3/83/3-3             NA  
    ##  9 Con8  #2/95/3               NA  
    ## 10 Con8  #3/5/2/2/95           28.5
    ## # ... with 39 more rows

``` r
select(litters_data, litter_number, gd0_weight, starts_with("pups"))
```

    ## # A tibble: 49 x 5
    ##    litter_number   gd0_weight pups_born_alive pups_dead_birth pups_survive
    ##    <chr>                <dbl>           <int>           <int>        <int>
    ##  1 #85                   19.7               3               4            3
    ##  2 #1/2/95/2             27                 8               0            7
    ##  3 #5/5/3/83/3-3         26                 6               0            5
    ##  4 #5/4/2/95/2           28.5               5               1            4
    ##  5 #4/2/95/3-3           NA                 6               0            6
    ##  6 #2/2/95/3-2           NA                 6               0            4
    ##  7 #1/5/3/83/3-3/2       NA                 9               0            9
    ##  8 #3/83/3-3             NA                 9               1            8
    ##  9 #2/95/3               NA                 8               0            8
    ## 10 #3/5/2/2/95           28.5               8               0            8
    ## # ... with 39 more rows

``` r
select(litters_data, litter_number, group, gd0_weight)
```

    ## # A tibble: 49 x 3
    ##    litter_number   group gd0_weight
    ##    <chr>           <chr>      <dbl>
    ##  1 #85             Con7        19.7
    ##  2 #1/2/95/2       Con7        27  
    ##  3 #5/5/3/83/3-3   Con7        26  
    ##  4 #5/4/2/95/2     Con7        28.5
    ##  5 #4/2/95/3-3     Con7        NA  
    ##  6 #2/2/95/3-2     Con7        NA  
    ##  7 #1/5/3/83/3-3/2 Con7        NA  
    ##  8 #3/83/3-3       Con8        NA  
    ##  9 #2/95/3         Con8        NA  
    ## 10 #3/5/2/2/95     Con8        28.5
    ## # ... with 39 more rows

``` r
select(litters_data, litter_number, group, everything()) #reorganizing columns
```

    ## # A tibble: 49 x 8
    ##    litter_number group gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>         <chr>      <dbl>       <dbl>       <int>           <int>
    ##  1 #85           Con7        19.7        34.7          20               3
    ##  2 #1/2/95/2     Con7        27          42            19               8
    ##  3 #5/5/3/83/3-3 Con7        26          41.4          19               6
    ##  4 #5/4/2/95/2   Con7        28.5        44.1          19               5
    ##  5 #4/2/95/3-3   Con7        NA          NA            20               6
    ##  6 #2/2/95/3-2   Con7        NA          NA            20               6
    ##  7 #1/5/3/83/3-~ Con7        NA          NA            20               9
    ##  8 #3/83/3-3     Con8        NA          NA            20               9
    ##  9 #2/95/3       Con8        NA          NA            20               8
    ## 10 #3/5/2/2/95   Con8        28.5        NA            20               8
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
select(litters_data, -group)
```

    ## # A tibble: 49 x 7
    ##    litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 #85                 19.7        34.7          20               3
    ##  2 #1/2/95/2           27          42            19               8
    ##  3 #5/5/3/83/3-3       26          41.4          19               6
    ##  4 #5/4/2/95/2         28.5        44.1          19               5
    ##  5 #4/2/95/3-3         NA          NA            20               6
    ##  6 #2/2/95/3-2         NA          NA            20               6
    ##  7 #1/5/3/83/3-~       NA          NA            20               9
    ##  8 #3/83/3-3           NA          NA            20               9
    ##  9 #2/95/3             NA          NA            20               8
    ## 10 #3/5/2/2/95         28.5        NA            20               8
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
select(litters_data, litter_number, gd0_weight:pups_born_alive)
```

    ## # A tibble: 49 x 5
    ##    litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>                <dbl>       <dbl>       <int>           <int>
    ##  1 #85                   19.7        34.7          20               3
    ##  2 #1/2/95/2             27          42            19               8
    ##  3 #5/5/3/83/3-3         26          41.4          19               6
    ##  4 #5/4/2/95/2           28.5        44.1          19               5
    ##  5 #4/2/95/3-3           NA          NA            20               6
    ##  6 #2/2/95/3-2           NA          NA            20               6
    ##  7 #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 #3/83/3-3             NA          NA            20               9
    ##  9 #2/95/3               NA          NA            20               8
    ## 10 #3/5/2/2/95           28.5        NA            20               8
    ## # ... with 39 more rows

``` r
litters_selected = select(litters_data, group, litter_number, gd0_weight, pups_born_alive) # a new data frame is created

select(litters_data, GROUP = group, litter_number) #rename varibles while selecting
```

    ## # A tibble: 49 x 2
    ##    GROUP litter_number  
    ##    <chr> <chr>          
    ##  1 Con7  #85            
    ##  2 Con7  #1/2/95/2      
    ##  3 Con7  #5/5/3/83/3-3  
    ##  4 Con7  #5/4/2/95/2    
    ##  5 Con7  #4/2/95/3-3    
    ##  6 Con7  #2/2/95/3-2    
    ##  7 Con7  #1/5/3/83/3-3/2
    ##  8 Con8  #3/83/3-3      
    ##  9 Con8  #2/95/3        
    ## 10 Con8  #3/5/2/2/95    
    ## # ... with 39 more rows

``` r
rename(litters_data, GROUP = group) #rename varibles without selecting
```

    ## # A tibble: 49 x 8
    ##    GROUP litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-~       NA          NA            20               9
    ##  8 Con8  #3/83/3-3           NA          NA            20               9
    ##  9 Con8  #2/95/3             NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95         28.5        NA            20               8
    ## # ... with 39 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

## Filtering\!\!\!
