---
title: Contributing to OCMSutility
description: How to contribute to OCMSutility R package
published: true
date: 2024-05-03T10:27:05.962Z
tags: r, sop, collab-coding
editor: markdown
dateCreated: 2024-05-03T10:26:41.115Z
---

# Contributing to OCMSutility R package
This page describes how to contribute to the [OCMSutlity R package](https://github.com/OxfordCMS/OCMSutility). OCMSutility is an R package for R functions that we think may be useful for ourselves and others doing similar work. The functions range from plotting to data manipulation. Functions are documented in the vignette (in the form of a Rmarkdown) and in the readme of the repository (in the form of a markdown). This page documents what to include in the documentation and how steps on how to render the documentation so both the vignette and readme are updated. OCMSutility uses `devtools` to build the package.

# Increment version number
When making changes to the package, please increment the version number in the `DESCRIPTION` file. Please increment the version number according to the type of change being made:
X.0.0 - major update to package
0.X.0 - new features, updates to features
0.0.X - minor changes and bug fixes

# Adding a function
Here, I'm describing what details should be included in every function added to OCMSutility. For more information on writing functions and R packages, see Hadley Wickham and Jennifer Bryan's [book](https://r-pkgs.org). **Remember to work in a new git branch**.

## Function name
Function naming convention should be all lower case with underscores. R file defining the function should be same as function name with `.R` extension. Legacy functions that don't follow this convention have wrapper functions that do follow the convention.

## Function pre-amble
This is the information to be included in the function pre-amble. All functions are exported so they are accessible with `OCMSutility::function_name`. 


```
#' function_name
#' 
#' Short description of function
#' 
#' @param argument type (dataframe, character, logical etc.). Short description of parameter. Perameter default if applicable.
#' 
#' @details (optional) Additional information on what the function needs or how to set the parameters.
#'
#' @import package dependency (remember to check package is in DESCRIPTION file)
#' 
#' @returns brief description of output
#' 
#' @export
#' 
#' @examples
#' reproducible R code to show how to use function

```

## Example Data
OCMSutility comes with DSS 16S data and metadata in case you want to use some microbiome data to showcase your function. You can load the data with `data(dss_example)` which is a list consisting of : a dataframe of ASV counts (`dss_example$merged_abundance_id`), a dataframe of taxonomy (`dss_example$merged_taxonomy`), and a dataframe of sample metadata (`dss_example$metadata`). Details on example data are found in the OCMSutility documentation.

## Testing Your Function
To test your function while you're writing it, save your R script and enter the following in the R console. This will load all the functions defined in the R package.

```
devtools::load_all()
```

# Documenting Function in Vignette
To add a function to the vignette, please edit the file `OCMSutility/vignettes/OCMSutilty.Rmd`. Vignette is functions based on the type of task they perform: plotting, data manipulation, and analysis. Add your function to the bottom of the relevant section. Please include the following in your addition:

```
## function_name {#function_name}

Brief description of function and when it would be useful. Any helpful information on how to use the function

Usage:

# Example on how to use the function shown in an R chunk (can be copied from the function preamble)
```

**Important**: please give the R chunk a unique name with `{r chunkname}` Chunck names can't have underscores.

Additionally, please add a hyperlink to the function in the table of contents at the top of the `Rmd` file.

```
# Table of Contents
...
[function_name](#function_name)
```

# Rendering the Vignette
Do not use `knit` to render the Rmarkdown. Instead, enter the following in the R console. This will build the help documents and render the vignette from the Rmarkdown.


```
devtools::document()
```

# Building the README.md
As a way to avoid updating OCMSutility documentation in two places, we build a `.md` file from the `Rmd` file. We do this using a `Makefile`. You have to first install the OCMSutility package that has been updated with the new function.

```
module load R/4.1.2-foss-2020a-bare
module load Pandoc/2.5
R
devtools::install_local(".")
quit(save='no')

cd OCMSutility
make clean
make all
```

## Push New Function to Github Repo
Once are finished writing and testing the new function, stage and commit your changes, and push your changes to a new branch on the github repository.

```
git add function_name.R
git add vignettes/OCMSutility.Rmd vignettes/OCMSutility.md vignettes/OCMSutility_files/*
git commit -m "added function_name"
git push origin branch_name
```

Next merge the new remote branch into main branch by going to the [OCMSutility github repo](https://github.com/OxfordCMS/OCMSutility) and click the green button to create a pull request and merge the branch.

## Install the latest version of OCMSutility

Pull the latest version of OCMSutility from remote main and re-install the updated OCMSutility package

```
git pull origin
R
devtools::install_github("https://github.com/OxfordCMS/OCMSutility")
quit(save='no')
```
