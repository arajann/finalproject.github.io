Data Cleaning
================

# Death Rate State Level

``` r
death_state =
  read_excel("data/DeathRate.xlsx", sheet = "State", 
             skip = 6) %>%
  janitor::clean_names() %>% 
  separate(
    col = breast_both_sexes_combined,
    into = c("breast_total", "female_only"),
    sep = "-"
  )
```

    ## Warning: Expected 2 pieces. Additional pieces discarded in 1 rows [41].

# Death Rate Per Cancer Type

``` r
death_cancer =
  read_excel("data/DeathRate.xlsx", sheet = "All US", 
             skip = 6) %>%
  janitor::clean_names()
```

# Incidence Rate State Level

``` r
inc_state =
  read_excel("data/IncRate.xlsx", sheet = "State", 
             skip = 6) %>%
  janitor::clean_names() %>% 
  separate(
    col = breast_both_sexes_combined,
    into = c("breast_total", "female_only"),
    sep = "-"
  )
```

    ## Warning: Expected 2 pieces. Missing pieces filled with `NA` in 2 rows [18, 25].

# Incidence Rate Per Cancer Type

``` r
inc_cancer =
  read_excel("data/IncRate.xlsx", sheet = "All US", 
             skip = 6) %>%
  janitor::clean_names()
```

# Death Trend Over Time

``` r
death_time =
  read_excel("data/DeathTrend.xlsx", 
             skip = 6) %>%
  janitor::clean_names()
```

# Pollution Data
