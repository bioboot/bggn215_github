# Class 6: R functions
Barry (PID: 911)

- [Our first (silly) function](#our-first-silly-function)
- [A second function](#a-second-function)
- [A protein generating function](#a-protein-generating-function)

All functions in R have at least 3 things:

- A **name**, we pick this and use it to call our function,
- Input **arguments** (there can be multiple)
- The **body** lines of R code that do the work

## Our first (silly) function

Write a function to add some numbers

``` r
add <- function(x, y=1) {
  x + y
}
```

Now we can call this function:

``` r
add(c(10, 10), 100)
```

    [1] 110 110

``` r
add(10, 100)
```

    [1] 110

## A second function

Write a function to generate random nucleotide sequences of a user
specified length:

The `sample()` function can be helpful here.

``` r
v <- sample(c("A","C","G","T"), size=50, replace = TRUE)
v
```

     [1] "G" "A" "C" "C" "A" "G" "C" "C" "A" "G" "A" "C" "T" "A" "G" "T" "T" "C" "T"
    [20] "C" "C" "A" "G" "T" "A" "C" "C" "G" "A" "C" "G" "C" "C" "A" "C" "C" "C" "C"
    [39] "C" "C" "T" "A" "C" "A" "G" "G" "G" "G" "T" "C"

I want the a 1 element long character vector that looks like this
“CACAGC” not “C” “A” “C” “A” “G” “C”

``` r
v <- sample(c("A","C","G","T"), size=50, replace = TRUE)
paste(v, collapse = "")
```

    [1] "GCAGGTGTCTGGGTTCTAGTCGAGGACCCGGGCAAATGGGTCTGTTCCAA"

Turn this into my first wee function

``` r
generate_dna <- function(size = 50) {
  v <- sample(c("A", "C", "G", "T"), size = size, replace = TRUE)
  return( paste(v, collapse = "") )

}
```

Test it:

``` r
generate_dna(60)
```

    [1] "TTTTGTGCCACGGGTGAGACATATGCTAGCGCCGCCTGCAGGGTACGGGAGAACCCACCT"

``` r
fasta <- TRUE
if(fasta) {
  cat("HELLO You!")
} else {
  cat("No you dont!")
}
```

    HELLO You!

Add the ability to retun a multi-elemnt vector or a single element fasta
like vector.

``` r
generate_fasta <- function(size = 50, fasta=TRUE) {
  v <- sample(c("A", "C", "G", "T"), size = size, replace = TRUE)
  s <- paste(v, collapse = "")
  
  if(fasta) {
    return(s)
  } else {
    return(v)
  }
}
```

``` r
generate_fasta(10)
```

    [1] "CTAAGGGCCC"

``` r
generate_fasta(10, fasta=FALSE)
```

     [1] "T" "T" "A" "G" "A" "C" "A" "T" "C" "G"

## A protein generating function

``` r
generate_protein <- function(size = 50, fasta = TRUE) {
  aa <- c("A", "R", "N", "D", "C", "Q", "E", "G", "H", "I", 
          "L", "K", "M", "F", "P", "S", "T", "W", "Y", "V")
  v <- sample(aa, size = size, replace = TRUE)
  s <- paste(v, collapse = "")
  
  if (fasta) {
    return(s)
  } else {
    return(v)
  }
}
```

``` r
generate_protein(6)
```

    [1] "SIRVTV"

Use our new `generate_protein()` function to make random prteon
sequences of length 6 to 12 (i.e. one length 6, one length 7, etc. up to
lenght 12).

One way to do this is “brute force”

``` r
generate_protein(6)
```

    [1] "HAYYKA"

``` r
generate_protein(7)
```

    [1] "QDRKQQT"

``` r
generate_protein(8)
```

    [1] "EHGDLSIA"

``` r
generate_protein(9)
```

    [1] "PDIMHAHDK"

A second way is to use a `for()` loop:

``` r
lengths <- 6:12
lengths
```

    [1]  6  7  8  9 10 11 12

``` r
for(i in lengths) {
  cat(">", i, "\n", sep="")
  aa <- generate_protein(i)
  cat(aa)
  cat("\n")
}
```

    >6
    IASLEL
    >7
    CYLVPLG
    >8
    RNMGACIA
    >9
    NPGWKWGVC
    >10
    YSFMCGFFAQ
    >11
    FEKQYIEVDKD
    >12
    LKKLMWNWGDGN

A third, and better, way to solve this is to use the `apply()` family of
functions, specifically the `sapply()` function in this case.

``` r
sapply(6:12, generate_protein)
```

    [1] "CYTQEL"       "HICNHGR"      "KYVVRCLV"     "IMNNEQWHS"    "YPRRWILFTV"  
    [6] "FMWFFKNRRED"  "YCNNPRDEQIFD"
