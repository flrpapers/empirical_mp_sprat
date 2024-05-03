# Developing management plans for sprat (Sprattus sprattus) in the Celtic Sea to advance the Ecosystem Approach to Fisheries

## Introduction

The code in this repository conducts Management Strategy Evaluation (MSE) to evaluate an empirical harvest control rule. The Operating Model is conditioned on Strategic Ecosystem Information and Life History Theory.

The FLR library is used to conduct the MSE, and a variety of additional R packages are required for data manipulation and plotting, obtaining life history parameters.

### FLR (Fisheries Library in R)

The [Fisheries Library in R](https://flr-project.org/), a collection of tools for quantitative fisheries science, developed in the R language, that facilitates the construction of bio-economic simulation models of fisheries systems. FLR provides a variety of tools for stock assesment and conducting MSE.

The packages used in this study are

```{r, pkgs-flr}
library(FLCore)
library(FLBRP)
library(FLasher)
library(FLife)
library(ggplotFL)
```

-   **FLCore**: Provides the core classes and methods to represent typical fisheries science data types and operations on them [Vignette](https://flr-project.org/FLCore/).

-   **FLBRP**: is a package for estimating biological reference points [Documentation](https://flr-project.org/packages/).

-   **FLasher**: allows projection to be conducted under a variety of assumptions [Vignette](https://flr-project.org/FLasher/).

-   **FLife**: Provides life history models for simulating population dynamics. [Documentation](https://flr-project.org/packages/).

-   **ggplotFL**: Extends ggplot2 for plotting FLR objects, and allows for the creation of publication-quality plots for data represented using FLR classes. [Vignette](https://flr-project.org/ggplotFL/).

### Life Histories

Life history parameters can be obtained from FishBase and used to infer mising values and to develop prior for population parameters.

```{r, pkgs-lh}
library(rfishbase)
library(SPMpriors)
library(FishLife)
```

-   **rfishbase**: A programmatic interface to 'FishBase', the world's largest database of fish species. It allows for easy access to a wide range of fish species data in R. [Vignette](https://cran.r-project.org/web/packages/rfishbase/vignettes/intro.html).

-   **SPMpriors**: Provides a way to generate prior distributions for stock productivity parameters, useful in stock assessment models and fisheries management. [Documentation](https://cran.r-project.org/web/packages/SPMpriors/index.html)

-   **FishLife**: Offers predictions of life history, morphological, ecological, and phylogenetic traits of fish based on the 'FishLife' database. It's useful for ecological and evolutionary research. [Vignette](https://cran.r-project.org/web/packages/FishLife/vignettes/FishLife.html).

### Data Manipulation and Plotting

We use a variety of packages, primarily authored or co-authored by Hadley Wickham, for data manipulation and visualisation.

```{r, pkgs-ggplot}
library(plyr)
library(dplyr)
library(reshape)

library(ggplot2)
library(GGally)
library(ggpubr)
library(ggcorrplot)
```

-   **plyr**: A set of tools for splitting, applying, and combining data, designed to work with data frames, lists, and arrays, making it easier to manipulate data structures in R. [Vignette](https://www.rdocumentation.org/packages/plyr/versions/-%208.9)[10][13][15][17][19].

-   **dplyr**: A grammar of data manipulation, providing a consistent set of verbs that helps in the most common data manipulation challenges. Primarily focused on tools for working with data frames. [Vignette](https://dplyr.tidyverse.org/articles/dplyr.html)[2][5][11][14][16][18][20].

-   **reshape**: Allows for flexibly restructuring and aggregating data using just two functions: melt and cast. It simplifies the process of transforming data between wide and long formats. [Documentation](https://cran.r-project.org/web/packages/reshape/index.html)[3][9].

-   **ggplot2**: A system for declaratively creating graphics, based on The Grammar of Graphics. It allows for the creation of complex plots from data in a data frame. [Vignette](https://ggplot-%20tidyverse.org)[4].

-   **ggpubr**: Provides easy-to-use functions for creating and customizing 'ggplot2'-based publication-ready plots. Simplifies the process of creating common types of plots and adjusting their appearance. [Vignette](https://rpkgs.datanovia.com/ggpubr/)[7].

-   **ggcorrplot**: A visualisation tool for displaying a correlation matrix using ggplot.\
    Simplifies the process of creating visually appealing correlation matrices. [Vignette](https://cran.r-project.org/web/packages/ggcorrplot/vignettes/ggcorrplot-intro.html)[7].

-   **GGally**: Extends ggplot2 by adding several functions to reduce the complexity of combining geometric objects with transformed data. It's useful for creating pairs plots, correlations, and other complex relationships. [Vignette](https://ggobi.github.io/ggally/)[7].

### Parallel Computing

Packages that allow the MSE to be conducted in parallel

```{r, pkgs-paral}
library(doParallel)
library(foreach)
```

-   **doParallel**: Provides a parallel backend for the 'foreach' looping construct. It allows for easy parallelization of R code on platforms supporting the 'parallel' package. [Vignette](https://cran.r-project.org/web/packages/doParallel/vignettes/gettingstartedParallel.pdf).

-   **foreach**: Provides a looping construct for executing R code repeatedly. 'foreach' can be used with parallel backends provided by other packages like 'doParallel' for parallel execution. [Vignette](https://cran.r-project.org/web/packages/foreach/vignettes/foreach.pdf).

### Statistics

```{r, pkgs-stat}
library(statcomp)
#library(RTseries)
```

### statcomp

Facilitates statistical complexity and entropy-based analysis of time series data. It includes various methods for chaos, fractal, and complexity analysis. [Vignette](https://cran.r-project.org/web/packages/statcomp/index.html).

### RTseries

Provides tools for analyzing and manipulating time series data, including functions for smoothing, decomposition, and forecasting. [Documentation](https://cran.r-project.org/web/packages/RTseries/index.html).

## Installation

The required Libraries (i.e. packages) can be installed from cran, or from [FLR-Project](https://flr-project.org)

Set mirror if needed using `chooseCRANmirror()`

```{r, install-util, eval=FALSE}
install.packages(c("plyr", 
                   "dplyr", 
                   "reshape"))
```

```{r, install-gg, eval=FALSE}
install.packages(c("ggplot2",
                   "ggpubr",
                   "ggcorrplot",
                   "GGally"))
```

### FLR

Via <https://flr-project.org/>

To install the latest released versions of the FLR packages, and their dependencies enter

```{r, eval=FALSE}
source("http://flr-project.org/R/instFLR.R")
```

then select 'FLCore', 'ggplotFL', 'FLBRP', 'FLasher', 'FLife', 'mydas'

Or install from source

```{r, eval=FALSE}
install.packages("remotes")

library(remotes)

remotes:::install_github("flr/FLCore")
remotes:::install_github("flr/FLBRP")
remotes:::install_github("flr/ggplotFL")
remotes:::install_github("flr/FLfishery")
remotes:::install_github("flr/FLasher", dependencies=TRUE)
remotes:::install_github("flr/FLife")
remotes:::install_github("flr/mydas")
```

#### FishBase

There are compatability problems with `FishBase`, so install an earlier version.

These have been fixed now. see <https://james-thorson-noaa.github.io/FishLife/>

```{r, eval=FALSE}
remotes::install_github("ropensci/rfishbase",ref="d150f2e0f5")
remotes::install_github("james-thorson/FishLife")
remotes::install_github("Henning-Winker/SPMpriors")
```

[Back to Top](#top)

## Examples {#example}

The examples here use `FLR`, tutorials on the various methods and packages can be found at <https://flr-project.org/doc/>

The Fisheries Library in R (FLR) is a collection of tools for quantitative fisheries science, developed in the R language, that facilitates the construction of bio-economic simulation models of fisheries systems. FLR builds on the powerful R environment and syntax to create a domain-specific language for the quantitative analysis of the expected risks and effects of fisheries management decision. The classes and methods in FLR consider uncertainty an integral part of our knowledge of fisheries system.

Life history traits include growth rate; age and size at sexual maturity; the temporal pattern or schedule of reproduction; the number, size, and sex ratio of offspring; the distribution of intrinsic or extrinsic mortality rates (e.g., patterns of senescence); and patterns of dormancy and dispersal. These traits contribute directly to age-specific survival and reproductive functions. The [`FLife`](https://flr-project.org/doc/Using_information_on_life_history_relationships.html) package has a variety of methods for modelling life history traits and functional forms for processes for use in fish stock assessment and for conducting Management Strategy Evaluation.

These relationships have many uses, for example in age-structured population models, functional relationships for these processes allow the calculation of the population growth rate and have been used to to develop priors in stock assesments and to parameterise ecological models. The `FLife` package has methods for modelling functional forms, for simulating equilibrium `FLBRP` and dynamic stock objects `FLStock`.

Create an `FLPar` object For a fish of length 45 cm.

```{r}
par=FLPar(linf=45)
```

```{r}
par
```

`FLPar()` creates an FLR object of [class](https://flr-project.org/doc/An_overview_of_the_FLCore_classes.html) `FLPar`

```{r}
is(par)
```

```{r}
?FLPar
```

Life history theory means that traits like length at maturity ($l_{50}$) can be derived from the expected size of a species, the `lhPar` method therefore uses life history theory to derive missing parameters.

```{r}
par=lhPar(par)
par
```

```{r}
?lhPar
```

An `FLBRP` object can then be created using `lhEql`

```{r}
eql=lhEql(par)
```

```{r}
?lhEql
```

This creates an object of class `FLBRP`

```{r}
is(eql)
```

[`FLBRP`](https://flr-project.org/doc/Reference_points_for_fisheries_management_with_FLBRP.html) is used to estimate reference points, and model equilibrium dynamics

```{r}
refpts(eql)
```

[ggplotFL](https://flr-project.org/doc/ggplotFL_plotting_FLR_objects_with_ggplot-%20html) is used for plotting FLR objects with ggplot2

```{r}
plot(eql)
```

```{r}
plot(eql,refpts="msy")
```

## More Information {#more}

-   For more information on the FLR Project for Quantitative Fisheries Science in R, visit the FLR webpage [^readme-1].

[^readme-1]: <http://flr-project.org>

## Author information

**Laurence Kell**. [laurie\@seaplusplus.co.uk](mailto:laurie@seaplusplus.co.uk){.email}

## Acknowledgements
