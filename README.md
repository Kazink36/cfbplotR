
<!-- README.md is generated from README.Rmd. Please edit that file -->

# cfbplotR <a href='https://cfbplotR.sportsdataverse.org/'><img src='https://raw.githubusercontent.com/sportsdataverse/cfbplotR/main/man/figures/logo.png' align="right" width="25%" min-width="120px" /></a>

<!-- badges: start -->
<!-- [![CRAN status](https://img.shields.io/cran/v/cfbplotR?style=flat-square&logo=R&label=CRAN)](https://CRAN.R-project.org/package=cfbplotR) -->

[![Version-Number](https://img.shields.io/github/r-package/v/sportsdataverse/cfbplotR?label=cfbplotR&logo=R&style=for-the-badge)](https://github.com/sportsdataverse/cfbplotR/)
[![R-CMD-check](https://img.shields.io/github/workflow/status/sportsdataverse/cfbplotR/R-CMD-check?label=R-CMD-Check&logo=R&logoColor=white&style=for-the-badge)](https://github.com/sportsdataverse/cfbplotR/actions/workflows/R-CMD-check.yaml)
[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg?style=for-the-badge&logo=github)](https://lifecycle.r-lib.org/articles/stages.html#experimental)[![Contributors](https://img.shields.io/github/contributors/sportsdataverse/cfbplotR?style=for-the-badge)](https://github.com/sportsdataverse/cfbplotR/graphs/contributors)
[![Twitter
Follow](https://img.shields.io/twitter/follow/JaredDLee.svg?color=blue&label=%40JaredDLee&logo=twitter&style=for-the-badge)](https://twitter.com/JaredDLee)
<!-- [![R build status](https://img.shields.io/github/workflow/status/Kazink36/cfbplotR/R-CMD-check?label=R%20check&style=flat-square&logo=github)](https://github.com/Kazink36/cfbplotR/actions) -->
<!-- [![R-CMD-check](https://github.com/Kazink36/cfbplotR/workflows/R-CMD-check/badge.svg)](https://github.com/Kazink36/cfbplotR/actions)-->
<!-- badges: end -->

The code for this package was copied heavily from
[nflplotR](https://nflplotr.nflverse.com/index.html) with minor changes
to support college football team logos.

The goal of cfbplotR is to provide functions and geoms that help
visualization of CFB related analysis. It provides a ggplot2 geom that
does the heavy lifting of plotting CFB logos in high quality, with
correct aspect ratio and possible transparency.

## Installation

<!-- You can install the released version of cfbplotR from [CRAN](https://CRAN.R-project.org) with: -->
<!-- ``` r -->
<!-- install.packages("cfbplotR") -->
<!-- ``` -->
<!-- And the development version from [GitHub](https://github.com/) with: -->
<!-- ``` r -->
<!-- # install.packages("devtools") -->
<!-- devtools::install_github("Kazink36/cfbplotR") -->
<!-- ``` -->

You can install the development version from
[GitHub](https://github.com/) with:

``` r
if (!require("remotes")) install.packages("remotes")
remotes::install_github("sportsdataverse/cfbplotR")
```

## Using cfbplotR

[You can follow this tutorial to see several different uses for
`cfbplotR`.](https://cfbplotR.sportsdataverse.org/articles/tutorial.html)
The key function in the package is `geom_cfb_logo()` which will add
college football team logos to a ggplot.

``` r
library(cfbplotR)
library(ggplot2)
team <- valid_team_names()
team <- team[1:32]
df <- data.frame(
  a = rep(1:8, 4),
  b = sort(rep(1:4, 8), decreasing = TRUE),
  teams = team
)

# keep alpha == 1 for all teams including an "A"
matches <- grepl("A", team)
df$alpha <- ifelse(matches, 1, 0.9)
# change color of all teams including an "o" to black and white
matches <- grepl("o", team)
df$color <- ifelse(matches, "b/w",NA)

 ggplot(df, aes(x = a, y = b)) +
   geom_cfb_logos(aes(team = teams, color = color, alpha = alpha), width = 0.075) +
   geom_label(aes(label = teams), nudge_y = -0.35, alpha = 0.5) +
   scale_color_identity() +
   scale_alpha_identity() +
   theme_void() 
```

<img src="man/figures/README-example-1.png" width="100%" />

## Getting help

The best places to get help on this package are:

-   messaging [Jared Lee on twitter](https://twitter.com/JaredDLee)
-   opening [an
    issue](https://github.com/sportsdataverse/cfbplotR/issues/new/choose)

## Contributing

Many hands make light work! Here are some ways you can contribute to
this project:

-   You can [open an
    issue](https://github.com/sportsdataverse/cfbplotR/issues/new/choose)
    if you’d like to request specific data or report a bug/error.

## Terms of Use

The R code for this package is released as open source under the [MIT
License](https://cfbplotR.sportsdataverse.org/LICENSE.html). CFB data
accessed by this package belong to their respective owners, and are
governed by their terms of use.
