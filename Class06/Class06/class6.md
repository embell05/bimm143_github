# Class06: R Functions
Emma Bell

- [Background](#background)
- [A first function](#a-first-function)
- [A Second Function](#a-second-function)
- [A new cool function](#a-new-cool-function)

## Background

Functions are at the heart of using R. Everything we do involves calling
and using functions (from data input, analysis to results output).

All functions in R have at least three things:

1.  a **name** the thing we use to call the function.
2.  one or more input **arguments** that are comma separated
3.  the **body**, lines of code between curly brackets {} that does the
    work of the function.

## A first function

Let’s write a silly wee fucntion to add some numbers.

``` r
add <- function(x) {
  x + 1
}
```

Let’s try it out

``` r
add(100)
```

    [1] 101

Will this work?

``` r
add( c(100, 200, 300))
```

    [1] 101 201 301

Modify to be more useful and add more than just 1

``` r
add <- function(x, y) {
  x + y
}
```

``` r
add(100, 10)
```

    [1] 110

``` r
plot(1:10, col="blue", typ= "b")
```

![](class6_files/figure-commonmark/unnamed-chunk-6-1.png)

``` r
log(10, base=10)
```

    [1] 1

Given y a default, so if we don’t give a value for y, it will
automatically think 1.

``` r
add <- function(x, y=1) {
  x + y
}
```

``` r
add(100)
```

    [1] 101

> **N.B** Input arguments can either be **required** or *optional*. The
> latter have a fall-back default that is specified in the function code
> with an equal sign.

``` r
#add(x=100, y=200, z=300)
```

## A Second Function

All funcitons in R look like this

    name <- function(arg) {
    body
    }

The `sample()` function in R

``` r
sample(1:10, size=4)
```

    [1] 7 9 3 8

> Q. Return 12 numbers picked randomly from the input 1:10

``` r
sample(1:10, size=10, replace=TRUE)
```

     [1] 6 7 9 9 8 7 3 7 8 8

you have to replace to TRUE, when wanting to generate more numbers than
the size you have.

> Q. Write the code to generate a random 12 nucleotide long DNA sequence

``` r
DNA <- c("A", "C", "T", "G")
sample(DNA, size=12, replace=TRUE)
```

     [1] "C" "G" "C" "G" "C" "G" "A" "G" "G" "T" "A" "A"

> Q. Write a first version function called `generate_dna()` that
> generates a user specified length `n` random DNA sequence?

``` r
generate_dna <- function(n=6){
  DNA <- c("A", "C", "T", "G")
sample(DNA, size=n, replace=TRUE)
}
```

``` r
generate_dna()
```

    [1] "G" "T" "C" "C" "A" "T"

``` r
generate_dna(100)
```

      [1] "G" "C" "G" "T" "T" "T" "T" "C" "G" "T" "C" "T" "T" "G" "G" "T" "C" "A"
     [19] "A" "C" "C" "G" "C" "G" "T" "C" "C" "T" "C" "T" "G" "T" "G" "A" "C" "A"
     [37] "T" "C" "A" "A" "A" "G" "G" "T" "C" "G" "G" "G" "A" "A" "C" "C" "C" "A"
     [55] "G" "A" "G" "C" "A" "G" "A" "A" "A" "G" "C" "C" "C" "A" "A" "A" "T" "A"
     [73] "G" "T" "A" "G" "C" "A" "G" "A" "A" "C" "T" "C" "T" "A" "T" "G" "A" "C"
     [91] "C" "G" "T" "G" "T" "G" "T" "T" "A" "G"

> Q. Modify your function to retunr a FASTA like sequence so rather than
> \[1\] “G” “C” etc we want GCAAT.

``` r
generate_dna <- function(n=6){
  DNA <- c("A", "C", "T", "G")
sample(DNA, size=n, replace=TRUE)
}
```

``` r
hello <- c("H", "E", "L", "L", "O")
paste(hello, collapse="")
```

    [1] "HELLO"

THIS is how you get the quotations marks out of the way.

``` r
paste(generate_dna(20), collapse="")
```

    [1] "TGTGCTAAGAGCTTTCATGT"

or

``` r
generate_dna <- function(n=6){
  DNA <- c("A", "C", "T", "G")
ans <- sample(DNA, size=n, replace=TRUE)
ans <- paste(ans, collapse="")
return(ans)
}
```

``` r
generate_dna(10)
```

    [1] "CTGGGCACTT"

> Q. Give the user an option to return FASTA format output sequence or
> standard multi-element vector format.

``` r
generate_dna <- function(n=6, fasta=TRUE){
  DNA <- c("A", "C", "T", "G")
ans <- sample(DNA, size=n, replace=TRUE)

if(fasta) {
  ans <- paste(ans, collapse="")
}
return(ans)
}
```

``` r
generate_dna(10)
```

    [1] "AATACTTCTA"

``` r
generate_dna(10, fasta=FALSE)
```

     [1] "C" "G" "T" "T" "T" "T" "G" "T" "C" "A"

just to show how it works:

``` r
generate_dna <- function(n=6, fasta=TRUE){
  DNA <- c("A", "C", "T", "G")
ans <- sample(DNA, size=n, replace=TRUE)

if(fasta) {
  ans <- paste(ans, collapse="")
  cat("Hello...")
}
return(ans)
}
```

``` r
generate_dna(10)
```

    Hello...

    [1] "GAGGTAGAAT"

``` r
generate_dna(10, fasta=FALSE)
```

     [1] "C" "C" "G" "C" "A" "G" "A" "C" "T" "A"

``` r
generate_dna <- function(n=6, fasta=TRUE){
  DNA <- c("A", "C", "T", "G")
ans <- sample(DNA, size=n, replace=TRUE)

if(fasta) {
  ans <- paste(ans, collapse="")
  cat("Hello...")
} else {
  cat("...is it me you are looking for")
}
return(ans)
}
```

``` r
generate_dna(10)
```

    Hello...

    [1] "GTAGACTTAA"

``` r
generate_dna(10, fasta=FALSE)
```

    ...is it me you are looking for

     [1] "A" "T" "A" "C" "C" "A" "T" "G" "G" "G"

## A new cool function

> Q. Write a function called `generate_protein()` that generates a use
> specified length protein sequence in FASTA like format

``` r
generate_protein <- function(n=6){
  aa <- c("A", "R", "N", "D", "C", "Q", "E", "G", "H", "I", "L", "K", "M", "F", "P", "S", "T", "W", "Y", "V")
ans <- sample(aa, size=n, replace=TRUE)
ans <- paste(ans, collapse="")
return(ans)
}
```

``` r
generate_protein(10)
```

    [1] "PMFDAIATHS"

> Q. Use your new `generate_protein()` function to generate all
> sequences between length 6 and 12 amino acids in length and check that
> any of these are unique in nature (ie found in the NR database at NBI)

``` r
generate_protein(6)
```

    [1] "VTMWVM"

this is found in NBI

``` r
generate_protein(12)
```

    [1] "SINNVIKDSFQI"

there is no 100% cover and identity

``` r
generate_protein(10)
```

    [1] "MWLRHDDDNG"

to not keep repeating yourself, using the for() loop

``` r
for(i in 6:12) {
  cat(i, "\n")
  cat(generate_protein(i), "\n")
}
```

    6 
    KTAPMQ 
    7 
    CYRYGSK 
    8 
    GYKPDKFV 
    9 
    SVQPGYFMN 
    10 
    VIQNYTRTRA 
    11 
    MLLWSQVVAWN 
    12 
    RYKWCYMTGSNT 

what a FASTA format looks like: \>id AGKRTST \>next GKSTR

sep is for getting rid of the space between the \> and the numbers

``` r
for(i in 6:12) {
  cat(">", i, sep="", "\n")
  cat(generate_protein(i), "\n")
}
```

    >6
    AAKPKT 
    >7
    YTNGVEP 
    >8
    WKTNDFAK 
    >9
    GTTSNGQFG 
    >10
    NDPGRDQKHF 
    >11
    MWGVKYLCTRW 
    >12
    RCNLCGGTHEDN 

number 9, 10, 11, 12 does not have a match
