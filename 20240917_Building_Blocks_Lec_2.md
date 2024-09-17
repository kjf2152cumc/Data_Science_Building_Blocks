Data Wrangling Lecture
================
Kaleb J. Frierson
2024-09-17

- [Notes](#notes)
- [Data Import](#data-import)
  - [Import the FAS Litters CSV](#import-the-fas-litters-csv)
  - [Changing Column Names](#changing-column-names)
- [Learning Assessment](#learning-assessment)
- [Read CSV Options](#read-csv-options)
- [Excel Files](#excel-files)

# Notes

Today is data wrangling lecture.

Tibbles are data frames, slightly different. Much better. Intended to
solve problems that have emerged with data frames. Faster, more memory
efficient, force you to do best practices. By default, anything that you
import using tidyverse code will be a tibble.

So what is a tibble?

80/20 rule: 80% of import cases only take 20% of your time. 20% however
will take like 80% of your time.

Need to learn readr package, haven, readxl

Readr is great for csv files and is common way to import. Readxl is
great for excel spreadsheets. Haven is great for bringing data from
other packages.

Should be thoughtful about your data. Know what it should look like. See
things that might be wrong, and why are they wrong? Something should be
a number but it isn’t, why is that the case?

When you are doing data wrangling, you want the most raw data. It helps
you get to know the data and makes the entire process reproducible.

# Data Import

We will be importing data within this document. Using R projects makes
relative paths very easy. So as long as your data is in your project,
its easy and doesn’t require an absolute path.

## Import the FAS Litters CSV

``` r
litters_df = read_csv("data_import_examples/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): Group, Litter Number, GD0 weight, GD18 weight
    ## dbl (4): GD of Birth, Pups born alive, Pups dead @ birth, Pups survive
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
head(litters_df)
```

    ## # A tibble: 6 × 8
    ##   Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##   <chr> <chr>           <chr>        <chr>                 <dbl>
    ## 1 Con7  #85             19.7         34.7                     20
    ## 2 Con7  #1/2/95/2       27           42                       19
    ## 3 Con7  #5/5/3/83/3-3   26           41.4                     19
    ## 4 Con7  #5/4/2/95/2     28.5         44.1                     19
    ## 5 Con7  #4/2/95/3-3     <NA>         <NA>                     20
    ## 6 Con7  #2/2/95/3-2     <NA>         <NA>                     20
    ## # ℹ 3 more variables: `Pups born alive` <dbl>, `Pups dead @ birth` <dbl>,
    ## #   `Pups survive` <dbl>

``` r
tail(litters_df, 15)
```

    ## # A tibble: 15 × 8
    ##    Group `Litter Number` `GD0 weight` `GD18 weight` `GD of Birth`
    ##    <chr> <chr>           <chr>        <chr>                 <dbl>
    ##  1 Low7  #112            23.9         40.5                     19
    ##  2 Mod8  #97             24.5         42.8                     20
    ##  3 Mod8  #5/93           <NA>         41.1                     20
    ##  4 Mod8  #5/93/2         .            .                        19
    ##  5 Mod8  #7/82-3-2       26.9         43.2                     20
    ##  6 Mod8  #7/110/3-2      27.5         46                       19
    ##  7 Mod8  #2/95/2         28.5         44.5                     20
    ##  8 Mod8  #82/4           33.4         52.7                     20
    ##  9 Low8  #53             21.8         37.2                     20
    ## 10 Low8  #79             25.4         43.8                     19
    ## 11 Low8  #100            20           39.2                     20
    ## 12 Low8  #4/84           21.8         35.2                     20
    ## 13 Low8  #108            25.6         47.5                     20
    ## 14 Low8  #99             23.5         39                       20
    ## 15 Low8  #110            25.5         42.7                     20
    ## # ℹ 3 more variables: `Pups born alive` <dbl>, `Pups dead @ birth` <dbl>,
    ## #   `Pups survive` <dbl>

``` r
view(litters_df)
```

## Changing Column Names

``` r
litters_df = janitor::clean_names(litters_df)
```

By default, clean names puts it into lower snake case across variables.
The Janitor package is used to clean up a lot of data things. Since
clean names is the only function that I need, I can use one line of code
to say use this function from this package.

# Learning Assessment

``` r
pups_df = read_csv("data_import_examples/FAS_pups.csv")
```

    ## Rows: 313 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Litter Number, PD ears
    ## dbl (4): Sex, PD eyes, PD pivot, PD walk
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
head(pups_df, 15)
```

    ## # A tibble: 15 × 6
    ##    `Litter Number`   Sex `PD ears` `PD eyes` `PD pivot` `PD walk`
    ##    <chr>           <dbl> <chr>         <dbl>      <dbl>     <dbl>
    ##  1 #85                 1 4                13          7        11
    ##  2 #85                 1 4                13          7        12
    ##  3 #1/2/95/2           1 5                13          7         9
    ##  4 #1/2/95/2           1 5                13          8        10
    ##  5 #5/5/3/83/3-3       1 5                13          8        10
    ##  6 #5/5/3/83/3-3       1 5                14          6         9
    ##  7 #5/4/2/95/2         1 .                14          5         9
    ##  8 #4/2/95/3-3         1 4                13          6         8
    ##  9 #4/2/95/3-3         1 4                13          7         9
    ## 10 #2/2/95/3-2         1 4                NA          8        10
    ## 11 #1/5/3/83/3-3/2     1 4                NA         NA         9
    ## 12 #1/5/3/83/3-3/2     1 4                NA          7         9
    ## 13 #1/5/3/83/3-3/2     1 4                NA          7         9
    ## 14 #1/5/3/83/3-3/2     1 4                NA          7         9
    ## 15 #1/5/3/83/3-3/2     1 4                NA          7         9

``` r
tail(pups_df, 15)
```

    ## # A tibble: 15 × 6
    ##    `Litter Number`   Sex `PD ears` `PD eyes` `PD pivot` `PD walk`
    ##    <chr>           <dbl> <chr>         <dbl>      <dbl>     <dbl>
    ##  1 #7/82/3-2           2 3                13          6         8
    ##  2 #7/82/3-2           2 3                12          6         8
    ##  3 #7/82/3-2           2 3                12          6         8
    ##  4 #7/82/3-2           2 3                12          6         8
    ##  5 #7/110/3-2          2 4                14          8        10
    ##  6 #7/110/3-2          2 4                14          7         9
    ##  7 #2/95/2             2 4                12          7         9
    ##  8 #2/95/2             2 4                12          6         8
    ##  9 #2/95/2             2 4                13          7         9
    ## 10 #2/95/2             2 4                12          7         9
    ## 11 #2/95/2             2 3                13          6         8
    ## 12 #2/95/2             2 3                13          7         9
    ## 13 #82/4               2 4                13          7         9
    ## 14 #82/4               2 3                13          7         9
    ## 15 #82/4               2 3                13          7         9

``` r
pups_df = janitor::clean_names(pups_df)
```

# Read CSV Options

Skip some rows and turn off column names:

``` r
litters_df = 
  read_csv(file = "data_import_examples/FAS_litters.csv", 
    col_names = FALSE, 
    skip = 1) 
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): X1, X2, X3, X4
    ## dbl (4): X5, X6, X7, X8
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

What about missing data?

``` r
litters_df = 
  read_csv(
    file = "data_import_examples/FAS_litters.csv",
    na = c("NA", "", ".")
  )
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

The code below will pull a variable from the dataset and call it
something new if you want to do that (not necessary), then takes the
mean of that variable.

``` r
litters_df = janitor::clean_names(litters_df) 

oweight= pull(litters_df, gd0_weight)
oweight
```

    ##  [1] 19.7 27.0 26.0 28.5   NA   NA   NA   NA   NA 28.5 28.0   NA   NA   NA   NA
    ## [16] 17.0 21.4   NA   NA   NA 28.0 23.5 22.6   NA 21.7 24.4 19.5 24.3 22.6 22.2
    ## [31] 23.8 22.6 23.8 25.5 23.9 24.5   NA   NA 26.9 27.5 28.5 33.4 21.8 25.4 20.0
    ## [46] 21.8 25.6 23.5 25.5

``` r
mean(oweight, na.rm = TRUE)
```

    ## [1] 24.37941

What if we code group as a factor variable?

``` r
litters_df = 
  read_csv(
    file = "data_import_examples/FAS_litters.csv", 
    na = c("NA","","."),
    col_types= cols(
      Group= col_factor()
    )
  )
```

# Excel Files

Importing MLB 2011 summary data. Sheet and range are specific to
read_excel.

``` r
mlb_df = read_excel("data_import_examples/mlb11.xlsx", sheet = "mlb11")

mlb_df
```

    ## # A tibble: 30 × 12
    ##    team        runs at_bats  hits homeruns bat_avg strikeouts stolen_bases  wins
    ##    <chr>      <dbl>   <dbl> <dbl>    <dbl>   <dbl>      <dbl>        <dbl> <dbl>
    ##  1 Texas Ran…   855    5659  1599      210   0.283        930          143    96
    ##  2 Boston Re…   875    5710  1600      203   0.28        1108          102    90
    ##  3 Detroit T…   787    5563  1540      169   0.277       1143           49    95
    ##  4 Kansas Ci…   730    5672  1560      129   0.275       1006          153    71
    ##  5 St. Louis…   762    5532  1513      162   0.273        978           57    90
    ##  6 New York …   718    5600  1477      108   0.264       1085          130    77
    ##  7 New York …   867    5518  1452      222   0.263       1138          147    97
    ##  8 Milwaukee…   721    5447  1422      185   0.261       1083           94    96
    ##  9 Colorado …   735    5544  1429      163   0.258       1201          118    73
    ## 10 Houston A…   615    5598  1442       95   0.258       1164          118    56
    ## # ℹ 20 more rows
    ## # ℹ 3 more variables: new_onbase <dbl>, new_slug <dbl>, new_obs <dbl>

``` r
pulse_df = read_sas("data_import_examples/public_pulse_data.sas7bdat")

pulse_df
```

    ## # A tibble: 1,087 × 7
    ##       ID   age Sex    BDIScore_BL BDIScore_01m BDIScore_06m BDIScore_12m
    ##    <dbl> <dbl> <chr>        <dbl>        <dbl>        <dbl>        <dbl>
    ##  1 10003  48.0 male             7            1            2            0
    ##  2 10015  72.5 male             6           NA           NA           NA
    ##  3 10022  58.5 male            14            3            8           NA
    ##  4 10026  72.7 male            20            6           18           16
    ##  5 10035  60.4 male             4            0            1            2
    ##  6 10050  84.7 male             2           10           12            8
    ##  7 10078  31.3 male             4            0           NA           NA
    ##  8 10088  56.9 male             5           NA            0            2
    ##  9 10091  76.0 male             0            3            4            0
    ## 10 10092  74.2 female          10            2           11            6
    ## # ℹ 1,077 more rows

Note, never use read.csv(), its not good. Doesn’t help you like Tibble
does. Don’t use dollar signs either.
