
<!-- README.md is generated from README.Rmd. Please edit that file -->
[![Travis-CI Build Status](https://travis-ci.org/fmichonneau/foghorn.svg?branch=master)](https://travis-ci.org/fmichonneau/foghorn) [![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/fmichonneau/foghorn?branch=master&svg=true)](https://ci.appveyor.com/project/fmichonneau/foghorn) ![Work in Progress](https://img.shields.io/badge/status-work%20in%20progress-yellow.svg) [![](http://www.r-pkg.org/badges/version/foghorn)](http://www.r-pkg.org/pkg/foghorn)

foghorn
=======

> **foghorn** *noun* <br> 1. Device used to facilitate navigation in foggy conditions by warning of potential hazards ahead.

`foghorn` makes accessible to the R terminal the results of the CRAN check results for the packages maintained by individuals, or for other package of interests. It provides a graphical summary of the results designed to added to your `.Rprofile` (to check regularly on the status of the published packages), or as a tibble.

As new features are introduced in development versions of R, or new policies are put in place, packages that are not updated frequently may start generating warnings or errors when built by CRAN. `foghorn` brings this information to your terminal automatically so you don't have to check the CRAN check results page regularly.

The package uses [whoami](https://cran.r-project.org/package=whoami) to guess your email address, but it can be specified manually.

Installation
------------

You can install foghorn from github with:

``` r
# install.packages("ghit")
ghit::install_github("fmichonneau/foghorn")
```

Example
-------

``` r
## load the package
library(foghorn)

## Graphical interface
summary_cran_checks(email = "francois.michonneau@gmail.com")
#> ◉ Package(s) with warnings on CRAN: rotl
#> ★ Package(s) with notes on CRAN: rncl

## Summary as a tibble
cran_check_results(email = "francois.michonneau@gmail.com")
#>     Package ERROR WARN NOTE OK
#> 1 phylobase    NA   NA   NA 13
#> 2  riceware    NA   NA   NA 13
#> 3      rncl    NA   NA    7  6
#> 4      rotl    NA    1   NA 12

## You can also have information just for some packages
summary_cran_checks(email = NULL,  package = c("mregions", "ridigbio"))
#> ✖ Package(s) with errors on CRAN: mregions
#> ★ Package(s) with notes on CRAN: mregions
cran_check_results(email = NULL,  package = c("mregions", "ridigbio"))
#> # A tibble: 2 × 5
#>    Package ERROR  WARN  NOTE    OK
#>      <chr> <int> <int> <int> <int>
#> 1 mregions     1    NA     1    11
#> 2 ridigbio    NA    NA    NA    13

## Or both
summary_cran_checks(email = "francois.michonneau@gmail.com",  package = c("mregions", "ridigbio"))
#> ✖ Package(s) with errors on CRAN: mregions
#> ◉ Package(s) with warnings on CRAN: rotl
#> ★ Package(s) with notes on CRAN: mregions, rncl
cran_check_results(email = "francois.michonneau@gmail.com",  package = c("mregions", "ridigbio"))
#> # A tibble: 6 × 5
#>     Package ERROR  WARN  NOTE    OK
#>       <chr> <int> <int> <int> <int>
#> 1  mregions     1    NA     1    11
#> 2  ridigbio    NA    NA    NA    13
#> 3 phylobase    NA    NA    NA    13
#> 4  riceware    NA    NA    NA    13
#> 5      rncl    NA    NA     7     6
#> 6      rotl    NA     1    NA    12
```
