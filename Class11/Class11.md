# Class 11
Emma Bell (A19247017)

- [Background](#background)
- [EBI AlphaFold Database](#ebi-alphafold-database)
- [Running Alphafold](#running-alphafold)

## Background

In this handson session we will utilise AlphaFold to predict protein
structure from sequence (Jumper et al., 2021).

Without the aid of such approaches, it can take years of expensive lab
work to determine the strutcure of just one protein. With AlphaFold, we
can now accuratelu compute a typical protein structure in as little as
ten minutes.

The PDB database (the main repository of experimental structures) only
has **~250 thousand structures** (last lab). The main protein sequencee
database has over **200 million** sequences!

``` r
(250000 / 200000000) * 100
```

    [1] 0.125

Only 0.125 of known sequences have a known structure! This is called the
‘structure knowledge gap’.

- Stuctures are much harder to determine than sequences.
- They are expensive, on average ~\$1000000, and take on average 3-5yrs.

## EBI AlphaFold Database

The EBI has a database of pre-computed AlphaFold (AF) models called
AFDB. This is growing all the time and can be useful to check before
running AF ourselves.

## Running Alphafold

We can download and run locally (on our own computers) but we need a
GPU. Or we can use the “cloud” computing to run this on someone elses
computer

We will use Colabfold \< https://github.com/sokrypton/ColabFold \>

We previously found there was no AFDB entry for our HIV sequence:

    >HIV-Pr-Dimer
    PQITLWQRPLVTIKIGGQLKEALLDTGADDTVLEEMSLPGRWKPKMIGGIGGFIKVRQYDQILIEICGHKAIGTVLVGPTPVNIIGRNLLTQIGCTLNF:PQITLWQRPLVTIKIGGQLKEALLDTGADDTVLEEMSLPGRWKPKMIGGIGGFIKVRQYDQILIEICGHKAIGTVLVGPTPVNIIGRNLLTQIGCTLNF

Here we will use AlphaFold2_mmseqs2
