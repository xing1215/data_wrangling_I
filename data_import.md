data import
================
Xing Chen
2019-9-17

## load in the litters file

``` r
litters_data = read_csv(file = "./data/FAS_litters.csv",
  skip = 10, col_names = FALSE)
```

    ## Parsed with column specification:
    ## cols(
    ##   X1 = col_character(),
    ##   X2 = col_character(),
    ##   X3 = col_double(),
    ##   X4 = col_double(),
    ##   X5 = col_double(),
    ##   X6 = col_double(),
    ##   X7 = col_double(),
    ##   X8 = col_double()
    ## )

``` r
litters_data = janitor::clean_names(litters_data)
```

## load in the pups file

``` r
pups_file = read_csv(file = "./data/FAS_pups.csv")
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
pups_file = janitor::clean_names(pups_file)
```

## play with column parsing

``` r
litters_data = read_csv(file = "./data/FAS_litters.csv",
  col_types = cols(
    Group = col_character(),
    `Litter Number` = col_character(),
    `GD0 weight` = col_double(),
    `GD18 weight` = col_double(),
    `GD of Birth` = col_integer(),
    `Pups born alive` = col_integer(),
    `Pups dead @ birth` = col_integer(),
    `Pups survive` = col_integer()
  )
)
```

``` r
pups_data = read_csv("./data/FAS_pups.csv", col_types = "cciiii")
```

# import excel file

``` r
mlb11_data = 
  read_excel(path = "./data/mlb11.xlsx")
```

# read in sas file…

``` r
pulse_data = haven::read_sas("./data/public_pulse_data.sas7bdat")
```

# output data file…

``` r
mlb_data_subset = 
  read_excel(path = "./data/mlb11.xlsx",
             range = "A1:D7")

write_csv(mlb_data_subset, path = "./data/mlb_subset.csv")
```
