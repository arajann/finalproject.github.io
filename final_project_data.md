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

# Pollution Data Cleaned for Incidence State Data

``` r
pollution1 = 
  read_csv("data/uspollution_us_2000_2016.csv")  
  
pollution1 = read_csv("data/uspollution_us_2000_2016.csv") %>% 
  janitor::clean_names() %>%
  select(state, date_local, no2_mean, o3_mean, 
         so2_mean, co_mean) %>%
  separate(date_local, into = c("year", "month", "day"), sep = "\\-") %>%
  select(-c("month", "day")) %>%
  group_by(year, state) %>%
  summarize(across(everything(), mean)) %>%
  filter(state != "Country Of Mexico") %>% 
  filter(
    year %in% (2013:2017)
  ) %>% 
  ungroup() %>% 
  select(state:co_mean) %>% 
  group_by(state) %>% 
  summarize(
    no2 = mean(no2_mean),
    o3 = mean(o3_mean),
    so2 = mean(so2_mean),
    co = mean(co_mean)
  ) %>%
  mutate_if(is.numeric, ~round(., 3))
```

``` r
pollution = read_csv("data/uspollution_us_2000_2016.csv") %>% 
  janitor::clean_names() %>%
  select(state, date_local, no2_mean, o3_mean, 
         so2_mean, co_mean) %>%
  separate(date_local, into = c("year", "month", "day"), sep = "\\-") %>%
  select(-c("month", "day")) %>%
  group_by(year, state) %>%
  summarize(across(everything(), mean)) %>%
  mutate_if(is.numeric, ~round(., 3)) %>%
  filter(state != "Country Of Mexico") %>% 
  mutate(
    year = as.numeric(year)
  )

str(pollution)
```

    ## grouped_df [490 x 6] (S3: grouped_df/tbl_df/tbl/data.frame)
    ##  $ year    : num [1:490] 2000 2000 2000 2000 2000 2000 2000 2000 2000 2000 ...
    ##  $ state   : chr [1:490] "Arizona" "California" "Colorado" "District Of Columbia" ...
    ##  $ no2_mean: num [1:490] 26.5 17.6 14.9 22.7 12.5 ...
    ##  $ o3_mean : num [1:490] 0.024 0.024 0.017 0.018 0.026 0.017 0.03 0.03 0.029 0.024 ...
    ##  $ so2_mean: num [1:490] 2.3 1.72 2.14 8.14 1.97 ...
    ##  $ co_mean : num [1:490] 0.746 0.644 0.611 1.176 0.725 ...
    ##  - attr(*, "groups")= tibble [17 x 2] (S3: tbl_df/tbl/data.frame)
    ##   ..$ year : num [1:17] 2000 2001 2002 2003 2004 ...
    ##   ..$ .rows: list<int> [1:17] 
    ##   .. ..$ : int [1:19] 1 2 3 4 5 6 7 8 9 10 ...
    ##   .. ..$ : int [1:20] 20 21 22 23 24 25 26 27 28 29 ...
    ##   .. ..$ : int [1:22] 40 41 42 43 44 45 46 47 48 49 ...
    ##   .. ..$ : int [1:23] 62 63 64 65 66 67 68 69 70 71 ...
    ##   .. ..$ : int [1:19] 85 86 87 88 89 90 91 92 93 94 ...
    ##   .. ..$ : int [1:19] 104 105 106 107 108 109 110 111 112 113 ...
    ##   .. ..$ : int [1:26] 123 124 125 126 127 128 129 130 131 132 ...
    ##   .. ..$ : int [1:29] 149 150 151 152 153 154 155 156 157 158 ...
    ##   .. ..$ : int [1:29] 178 179 180 181 182 183 184 185 186 187 ...
    ##   .. ..$ : int [1:28] 207 208 209 210 211 212 213 214 215 216 ...
    ##   .. ..$ : int [1:30] 235 236 237 238 239 240 241 242 243 244 ...
    ##   .. ..$ : int [1:36] 265 266 267 268 269 270 271 272 273 274 ...
    ##   .. ..$ : int [1:35] 301 302 303 304 305 306 307 308 309 310 ...
    ##   .. ..$ : int [1:38] 336 337 338 339 340 341 342 343 344 345 ...
    ##   .. ..$ : int [1:41] 374 375 376 377 378 379 380 381 382 383 ...
    ##   .. ..$ : int [1:42] 415 416 417 418 419 420 421 422 423 424 ...
    ##   .. ..$ : int [1:34] 457 458 459 460 461 462 463 464 465 466 ...
    ##   .. ..@ ptype: int(0) 
    ##   ..- attr(*, ".drop")= logi TRUE

# Merging Pollution and Incidence Data Sets

``` r
merged_pollute_inc =
  merge(inc_state, pollution1, by = "state")
```

# Death\_time and Pollution Merged

``` r
modified_pollution =
  read_csv("data/uspollution_us_2000_2016.csv") %>% 
  janitor::clean_names() %>%
  select(state, date_local, no2_mean, o3_mean, 
         so2_mean, co_mean) %>%
  separate(date_local, into = c("year", "month", "day"), sep = "\\-") %>%
  select(-c("month", "day")) %>%
  group_by(year, state) %>%
  summarize(across(everything(), mean)) %>%
  mutate_if(is.numeric, ~round(., 3)) %>%
  filter(state != "Country Of Mexico") %>%
  group_by(year) %>%
  summarize(across(everything(), mean)) %>%
  select(-c(state)) %>% 
  mutate(
    year = as.numeric(year)
  )
```

# Plots by cancer type

``` r
inc_cancer_plot =
  inc_cancer %>%
  select(cancer_type, female, male) %>%
  pivot_longer(
    female:male,
    names_to = "sex",
    values_to = "incidence"
  ) %>%
  filter(cancer_type != "All cancer types combined",
         incidence != 0) %>%
  mutate(cancer_type = fct_reorder(cancer_type, incidence)) %>%
  ggplot(aes(x = cancer_type, y = incidence, color = sex)) +
  geom_point(aes(size = 2)) + guides(size = "none") +
  theme(axis.text.x = element_text(angle = 90, vjust = 0.5, hjust = 1)) +
  labs(title = "Cancer Incidence Rate for Different Cancer Types by Sex in 2013-2017", 
       x = "Cancer Type", y = "Incidence")

death_cancer_plot =
  death_cancer %>%
  select(cancer_type, female, male) %>%
  pivot_longer(
    female:male,
    names_to = "sex",
    values_to = "death"
  ) %>%
  filter(cancer_type != "All cancer types combined",
         death != 0) %>%
  mutate(cancer_type = fct_reorder(cancer_type, death)) %>%
  ggplot(aes(x = cancer_type, y = death, color = sex)) +
  geom_point(aes(size = 2)) + guides(size = "none") +
  theme(axis.text.x = element_text(angle = 90, vjust = 0.5, hjust = 1)) +
  labs(title = "Cancer Death Rate for Different Cancer Types by Sex in 2013-2017", 
       x = "Cancer Type", y = "Death")
```
