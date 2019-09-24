data manipulation
================
Xing Chen
2019-9-19

## import data files

``` r
litters_data = read_csv("./data/FAS_litters.csv")
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

``` r
litters_data = janitor::clean_names(litters_data)

pups_data = read_csv("./data/FAS_pups.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   `Litter Number` = col_character(),
    ##   Sex = col_double(),
    ##   `PD ears` = col_double(),
    ##   `PD eyes` = col_double(),
    ##   `PD pivot` = col_double(),
    ##   `PD walk` = col_double()
    ## )

``` r
pups_data = janitor::clean_names(pups_data)
```

## selecting…

``` r
select(litters_data, group, litter_number, starts_with("pups"))
```

    ## # A tibble: 49 x 5
    ##    group litter_number   pups_born_alive pups_dead_birth pups_survive
    ##    <chr> <chr>                     <dbl>           <dbl>        <dbl>
    ##  1 Con7  #85                           3               4            3
    ##  2 Con7  #1/2/95/2                     8               0            7
    ##  3 Con7  #5/5/3/83/3-3                 6               0            5
    ##  4 Con7  #5/4/2/95/2                   5               1            4
    ##  5 Con7  #4/2/95/3-3                   6               0            6
    ##  6 Con7  #2/2/95/3-2                   6               0            4
    ##  7 Con7  #1/5/3/83/3-3/2               9               0            9
    ##  8 Con8  #3/83/3-3                     9               1            8
    ##  9 Con8  #2/95/3                       8               0            8
    ## 10 Con8  #3/5/2/2/95                   8               0            8
    ## # … with 39 more rows

``` r
select(litters_data, litter_number, group)
```

    ## # A tibble: 49 x 2
    ##    litter_number   group
    ##    <chr>           <chr>
    ##  1 #85             Con7 
    ##  2 #1/2/95/2       Con7 
    ##  3 #5/5/3/83/3-3   Con7 
    ##  4 #5/4/2/95/2     Con7 
    ##  5 #4/2/95/3-3     Con7 
    ##  6 #2/2/95/3-2     Con7 
    ##  7 #1/5/3/83/3-3/2 Con7 
    ##  8 #3/83/3-3       Con8 
    ##  9 #2/95/3         Con8 
    ## 10 #3/5/2/2/95     Con8 
    ## # … with 39 more rows

``` r
select(litters_data, litter_number, group, everything())
```

    ## # A tibble: 49 x 8
    ##    litter_number group gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>         <chr>      <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85           Con7        19.7        34.7          20               3
    ##  2 #1/2/95/2     Con7        27          42            19               8
    ##  3 #5/5/3/83/3-3 Con7        26          41.4          19               6
    ##  4 #5/4/2/95/2   Con7        28.5        44.1          19               5
    ##  5 #4/2/95/3-3   Con7        NA          NA            20               6
    ##  6 #2/2/95/3-2   Con7        NA          NA            20               6
    ##  7 #1/5/3/83/3-… Con7        NA          NA            20               9
    ##  8 #3/83/3-3     Con8        NA          NA            20               9
    ##  9 #2/95/3       Con8        NA          NA            20               8
    ## 10 #3/5/2/2/95   Con8        28.5        NA            20               8
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
select(litters_data, -group)
```

    ## # A tibble: 49 x 7
    ##    litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 #85                 19.7        34.7          20               3
    ##  2 #1/2/95/2           27          42            19               8
    ##  3 #5/5/3/83/3-3       26          41.4          19               6
    ##  4 #5/4/2/95/2         28.5        44.1          19               5
    ##  5 #4/2/95/3-3         NA          NA            20               6
    ##  6 #2/2/95/3-2         NA          NA            20               6
    ##  7 #1/5/3/83/3-…       NA          NA            20               9
    ##  8 #3/83/3-3           NA          NA            20               9
    ##  9 #2/95/3             NA          NA            20               8
    ## 10 #3/5/2/2/95         28.5        NA            20               8
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
select(litters_data, litter_number, gd0_weight:pups_born_alive)
```

    ## # A tibble: 49 x 5
    ##    litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>                <dbl>       <dbl>       <dbl>           <dbl>
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
    ## # … with 39 more rows

``` r
litters_select = select(litters_data, litter_number, gd0_weight:pups_born_alive)

select(litters_data, litter_number, GROUP = group)
```

    ## # A tibble: 49 x 2
    ##    litter_number   GROUP
    ##    <chr>           <chr>
    ##  1 #85             Con7 
    ##  2 #1/2/95/2       Con7 
    ##  3 #5/5/3/83/3-3   Con7 
    ##  4 #5/4/2/95/2     Con7 
    ##  5 #4/2/95/3-3     Con7 
    ##  6 #2/2/95/3-2     Con7 
    ##  7 #1/5/3/83/3-3/2 Con7 
    ##  8 #3/83/3-3       Con8 
    ##  9 #2/95/3         Con8 
    ## 10 #3/5/2/2/95     Con8 
    ## # … with 39 more rows

``` r
rename(litters_data, Group = group)
```

    ## # A tibble: 49 x 8
    ##    Group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  8 Con8  #3/83/3-3           NA          NA            20               9
    ##  9 Con8  #2/95/3             NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95         28.5        NA            20               8
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
litters_data
```

    ## # A tibble: 49 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  8 Con8  #3/83/3-3           NA          NA            20               9
    ##  9 Con8  #2/95/3             NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95         28.5        NA            20               8
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

In larger datasets, I also use `starts_with()`, `ends_with()`, and
`contains()` often.

## filtering…..

``` r
filter(litters_data, group == "Con7")

filter(litters_data, gd_of_birth == 20)

filter(litters_data, group %in% c("Con7", "Con8"))

filter(litters_data, gd0_weight + gd18_weight < 70)

# dont do this!
# filter(litters_data, !is.na(gd0_weight))

drop_na(litters_data)
drop_na(litters_data, gd0_weight)
```

## mutate…

``` r
mutate(litters_data,
  wt_gain = gd18_weight - gd0_weight,
  group = str_to_lower(group),
  group = str_to_upper(group)
)
```

    ## # A tibble: 49 x 9
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 CON7  #85                 19.7        34.7          20               3
    ##  2 CON7  #1/2/95/2           27          42            19               8
    ##  3 CON7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 CON7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 CON7  #4/2/95/3-3         NA          NA            20               6
    ##  6 CON7  #2/2/95/3-2         NA          NA            20               6
    ##  7 CON7  #1/5/3/83/3-…       NA          NA            20               9
    ##  8 CON8  #3/83/3-3           NA          NA            20               9
    ##  9 CON8  #2/95/3             NA          NA            20               8
    ## 10 CON8  #3/5/2/2/95         28.5        NA            20               8
    ## # … with 39 more rows, and 3 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>, wt_gain <dbl>

## Arrange…

``` r
arrange(litters_data, pups_born_alive)
```

    ## # A tibble: 49 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Low7  #111                25.5        44.6          20               3
    ##  3 Low8  #4/84               21.8        35.2          20               4
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con8  #2/2/95/2           NA          NA            19               5
    ##  6 Mod7  #3/82/3-2           28          45.9          20               5
    ##  7 Mod7  #5/3/83/5-2         22.6        37            19               5
    ##  8 Mod7  #106                21.7        37.8          20               5
    ##  9 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## 10 Con7  #4/2/95/3-3         NA          NA            20               6
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
arrange(litters_data, desc(pups_born_alive))
```

    ## # A tibble: 49 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Low7  #102                22.6        43.3          20              11
    ##  2 Mod8  #5/93               NA          41.1          20              11
    ##  3 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  4 Con8  #3/83/3-3           NA          NA            20               9
    ##  5 Con8  #5/4/3/83/3         28          NA            19               9
    ##  6 Mod7  #103                21.4        42.1          19               9
    ##  7 Mod7  #4/2/95/2           23.5        NA            19               9
    ##  8 Mod7  #8/110/3-2          NA          NA            20               9
    ##  9 Low7  #107                22.6        42.4          20               9
    ## 10 Low7  #98                 23.8        43.8          20               9
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>

``` r
arrange(litters_data, pups_born_alive, gd0_weight)
```

    ## # A tibble: 49 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Low7  #111                25.5        44.6          20               3
    ##  3 Low8  #4/84               21.8        35.2          20               4
    ##  4 Mod7  #106                21.7        37.8          20               5
    ##  5 Mod7  #5/3/83/5-2         22.6        37            19               5
    ##  6 Mod7  #3/82/3-2           28          45.9          20               5
    ##  7 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  8 Con8  #2/2/95/2           NA          NA            19               5
    ##  9 Low8  #99                 23.5        39            20               6
    ## 10 Low7  #112                23.9        40.5          19               6
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <dbl>,
    ## #   pups_survive <dbl>
