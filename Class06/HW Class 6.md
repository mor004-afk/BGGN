# HW Class 6
Montserrat(PID:A16536527)

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

![](HW-Class-6_files/figure-commonmark/unnamed-chunk-1-1.png)

``` r
plotb3(s2.b, sse=s2.chainA, typ="l", ylab="Bfactor")
```

![](HW-Class-6_files/figure-commonmark/unnamed-chunk-1-2.png)

``` r
plotb3(s3.b, sse=s3.chainA, typ="l", ylab="Bfactor")
```

![](HW-Class-6_files/figure-commonmark/unnamed-chunk-1-3.png)

> Q6. How would you generalize the original code above to work with any
> set of input protein structures?

``` r
plot_kinase_bfactor <- function(pdb_id) {
  pdb <- read.pdb(pdb_id)
  chainA <- trim.pdb(pdb, chain="A", elety="CA")
  b <- chainA$atom$b
  plotb3(b, sse=chainA, typ="l", ylab="Bfactor")
}

plot_kinase_bfactor("1AKE")
```

      Note: Accessing on-line PDB file

    Warning in get.pdb(file, path = tempdir(), verbose = FALSE):
    /var/folders/x9/n4kqcfvn2dqgldcbtkjd702h0000gn/T//Rtmp7c1Z7t/1AKE.pdb exists.
    Skipping download

       PDB has ALT records, taking A only, rm.alt=TRUE

![](HW-Class-6_files/figure-commonmark/unnamed-chunk-2-1.png)

The input to this function are the pdb ID such as “4AKE” or “1AKE”.

This function takes a PDB ID, reads the corresponding protein structure,
extracts Calpha atoms from chain A, retrieves their B-factors, and plots
those B-factors with secondary structure annotation

The output of the function is a plot showing the B-factor values for
Calpha atoms in chain A of the specified PDB structure, with secondary
structure annotation
