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
    into = c("breast_total", "female_breast_only"),
    sep = "-"
  ) %>% 
  select(-female_breast_only) %>%
  mutate(
    breast_male = if_else(breast_male == "n/a", "0", breast_male),
    cervix_male = if_else(cervix_male == "n/a", "0", cervix_male),
  ) %>%
  mutate_at(vars(-("state")), as.numeric) %>%
  filter(state != "Puerto Rico")
```

    ## Warning: Expected 2 pieces. Additional pieces discarded in 1 rows [41].

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

    ## Warning in mask$eval_all_mutate(quo): NAs introduced by coercion

# Death Rate Per Cancer Type

``` r
death_cancer =
  read_excel("data/DeathRate.xlsx", sheet = "All US", 
             skip = 6) %>%
  janitor::clean_names()  %>%
  mutate(
    male = if_else(male == "n/a", "0", male),
    female = if_else(female == "n/a", "0", female)
  ) %>%
  separate(both_sexes_combined, into = c("both_sexes_combined", "note"), sep = "\\-") %>%
  select(-note) %>%
  mutate_at(vars(-("cancer_type")), as.numeric)
```

    ## Warning: Expected 2 pieces. Missing pieces filled with `NA` in 23 rows [1, 2, 4,
    ## 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, ...].

# Incidence Rate State Level

``` r
inc_state =
  read_excel("data/IncRate.xlsx", sheet = "State", 
             skip = 6) %>%
  janitor::clean_names() %>% 
  separate(
    col = breast_both_sexes_combined,
    into = c("breast_total", "female_breast_only"),
    sep = "-"
  ) %>% 
  mutate(
    breast_male = if_else(breast_male == "n/a", "0", breast_male),
    cervix_male = if_else(cervix_male == "n/a", "0", cervix_male),
    colon_excluding_rectum_both_sexes_combined = if_else(colon_excluding_rectum_both_sexes_combined == "n/a", "0", colon_excluding_rectum_both_sexes_combined),
    colon_excluding_rectum_female = if_else(colon_excluding_rectum_female == "n/a", "0", colon_excluding_rectum_female),
    colon_excluding_rectum_male = if_else(colon_excluding_rectum_male == "n/a", "0", colon_excluding_rectum_male),
  ) %>%
  filter(state != "Puerto Rico") %>%
  select(-c("female_breast_only", starts_with("colon"), starts_with("rectum")))
```

    ## Warning: Expected 2 pieces. Missing pieces filled with `NA` in 2 rows [18, 25].

# Incidence Rate Per Cancer Type

``` r
inc_cancer =
  read_excel("data/IncRate.xlsx", sheet = "All US", 
             skip = 6) %>%
  janitor::clean_names() %>% 
  mutate(
    male = if_else(male == "n/a", "0", male),
    female = if_else(female == "n/a", "0", female)
  ) %>%
  separate(both_sexes_combined, into = c("both_sexes_combined", "note"), sep = "\\-") %>%
  select(-note) %>%
  mutate_at(vars(-("cancer_type")), as.numeric) %>%
  filter(cancer_type != "Colon (excluding rectum)",
         cancer_type != "Rectum")
```

    ## Warning: Expected 2 pieces. Missing pieces filled with `NA` in 25 rows [1, 2, 4,
    ## 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, ...].

# Death Trend Over Time

``` r
read_death_time =
  read_excel("data/DeathTrend.xlsx", 
             skip = 6) %>%
  janitor::clean_names()

x = c("colorectum_female", "colorectum_male", "liver_and_intrahepatic_bile_duct_female", "liver_and_intrahepatic_bile_duct_male", "lung_and_bronchus_female", "lung_and_bronchus_male", "ovary_female", "uterus_cervix_and_corpus_combined_female")

remove_note = function(column_name) {
  read_death_time = read_death_time %>% 
    separate(column_name, into = c(column_name, "note"), sep = "\\-") %>% 
    select(-note)}

for (i in x) {
  read_death_time = remove_note(i)} 

death_time =
  read_death_time %>%
  filter(year %in% 2000:2016) %>%
  select(-c("breast_male", "ovary_male", "prostate_female","uterus_cervix_and_corpus_combined_male")) %>%
  mutate_at(vars(-("year")), as.numeric) %>%
  mutate(year = as.factor(year))
```

# Pollution Data

``` r
pollution =
  read_csv("data/uspollution_us_2000_2016.csv") %>%
  janitor::clean_names() %>%
  select(state, date_local, no2_mean, o3_mean, 
         so2_mean, co_mean) %>%
  separate(date_local, into = c("year", "month", "day"), sep = "\\-") %>%
  select(-c(day)) %>%
  group_by(year, month, state) %>%
  summarize(across(everything(), mean)) %>%
  mutate_if(is.numeric, ~round(., 3)) %>%
  filter(state != "Country Of Mexico") %>%
  mutate(year = as.factor(year))
```

    ## New names:
    ## * `` -> ...1

    ## Rows: 1746661 Columns: 29

    ## -- Column specification --------------------------------------------------------
    ## Delimiter: ","
    ## chr   (8): Address, State, County, City, NO2 Units, O3 Units, SO2 Units, CO ...
    ## dbl  (20): ...1, State Code, County Code, Site Num, NO2 Mean, NO2 1st Max Va...
    ## date  (1): Date Local

    ## 
    ## i Use `spec()` to retrieve the full column specification for this data.
    ## i Specify the column types or set `show_col_types = FALSE` to quiet this message.

    ## `summarise()` has grouped output by 'year', 'month'. You can override using the `.groups` argument.

    ## `mutate_if()` ignored the following grouping variables:
    ## Columns `year`, `month`
