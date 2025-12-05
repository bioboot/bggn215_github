# HW Class 6
Barry (PID: 911)

Function writting homework

Here is the code from the hw:

``` r
# Can you improve this analysis code?
library(bio3d)
s1 <- read.pdb("4AKE") # kinase with drug
```

      Note: Accessing on-line PDB file

``` r
s2 <- read.pdb("1AKE") # kinase no drug
```

      Note: Accessing on-line PDB file
       PDB has ALT records, taking A only, rm.alt=TRUE

``` r
s3 <- read.pdb("1E4Y") # kinase with drug
```

      Note: Accessing on-line PDB file

``` r
s1.chainA <- trim.pdb(s1, chain="A", elety="CA")
s2.chainA <- trim.pdb(s2, chain="A", elety="CA")
s3.chainA <- trim.pdb(s1, chain="A", elety="CA")
s1.b <- s1.chainA$atom$b
s2.b <- s2.chainA$atom$b
s3.b <- s3.chainA$atom$b
plotb3(s1.b, sse=s1.chainA, typ="l", ylab="Bfactor")
```

![](hw_class6_files/figure-commonmark/unnamed-chunk-1-1.png)

``` r
plotb3(s2.b, sse=s2.chainA, typ="l", ylab="Bfactor")
```

![](hw_class6_files/figure-commonmark/unnamed-chunk-1-2.png)

``` r
plotb3(s3.b, sse=s3.chainA, typ="l", ylab="Bfactor")
```

![](hw_class6_files/figure-commonmark/unnamed-chunk-1-3.png)

## Test

``` r
library(readr)

url <- "https://tinyurl.com/UK-foods"
x <- read_csv(url)
```

    New names:
    Rows: 17 Columns: 5
    ── Column specification
    ──────────────────────────────────────────────────────── Delimiter: "," chr
    (1): ...1 dbl (4): England, Wales, Scotland, N.Ireland
    ℹ Use `spec()` to retrieve the full column specification for this data. ℹ
    Specify the column types or set `show_col_types = FALSE` to quiet this message.
    • `` -> `...1`

``` r
x
```

    # A tibble: 17 × 5
       ...1               England Wales Scotland N.Ireland
       <chr>                <dbl> <dbl>    <dbl>     <dbl>
     1 Cheese                 105   103      103        66
     2 Carcass_meat           245   227      242       267
     3 Other_meat             685   803      750       586
     4 Fish                   147   160      122        93
     5 Fats_and_oils          193   235      184       209
     6 Sugars                 156   175      147       139
     7 Fresh_potatoes         720   874      566      1033
     8 Fresh_Veg              253   265      171       143
     9 Other_Veg              488   570      418       355
    10 Processed_potatoes     198   203      220       187
    11 Processed_Veg          360   365      337       334
    12 Fresh_fruit           1102  1137      957       674
    13 Cereals               1472  1582     1462      1494
    14 Beverages               57    73       53        47
    15 Soft_drinks           1374  1256     1572      1506
    16 Alcoholic_drinks       375   475      458       135
    17 Confectionery           54    64       62        41
