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

## Read CSV Options

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
