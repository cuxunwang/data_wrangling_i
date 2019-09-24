Tidy Data
================
Xun Wang
9/24/2019

## Wide to long

``` r
pulse_data = 
  haven::read_sas("./data/public_pulse_data.sas7bdat") %>% 
  janitor::clean_names() %>% 
  pivot_longer(
    bdi_score_bl:bdi_score_12m,
    names_to = "visit", # create a new column
    names_prefix = "bdi_score_", # remove the unrelavent words
    values_to = "bdi"
  ) %>% 
  mutate(
    visit = recode(visit, "bl" = "00m") # change the variable name
  )
```

## separate in litters

``` r
litters_data = 
  read_csv("./data/FAS_litters.csv") %>% 
  janitor::clean_names() %>% 
  separate(col = group, into = c("dose", "day_of_tx"), 3)
```

    ## Parsed with column specification:
    ## cols(
    ##   Group = col_character(),
    ##   `Litter Number` = col_character(),
    ##   `GD0 weight` = col_double(),
    ##   `GD18 weight` = col_double(),
    ##   `GD of Birth` = col_double(),
    ##   `Pups born alive` = col_double(),
    ##   `Pups dead @ birth` = col_double(),
    ##   `Pups survive` = col_double()
    ## )
