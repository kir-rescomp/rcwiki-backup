---
title: Cheatsheet Rmarkdown
description: Tips on creating Rmarkdown for reports
published: true
date: 2024-05-22T15:03:41.622Z
tags: rmd, cheatsheet
editor: markdown
dateCreated: 2024-05-22T15:03:41.622Z
---

# Cheatsheet for Rmarkdown
This page contains helpful tips how to make reports from Rmarkdown files. Rmarkdown is a form of markdown that can run R code within your document. This is particularly helpful when generating a report on some R analysis. There are two ways in which you could set up your R analysis and Rmarkdown, and both ways have their advantages and disadvantages.

One option is to perform your analysis directly in the Rmarkdown.

Advantages:

* the code and the report are all in the same document so it's easy to see everything together. 

Disadvantages:

* you may not want to include all your analysis in the report, so your report may become bloated with code, which could reduce it's readability.

The other option is to have an R script for analysis, and an Rmarkdown for the report, and source the Rscript in your Rmarkdown so all the variables in your R script are accessible within the Rmarkdwon. 

Advantages:

* you can only report on the relevant parts of your analysis
* Rmarkdown can be easier to read, as all your code is in a separate file

Disadvantages:

* you have to run your entire analysis everytime you render your report (though there are some ways around this, discussed below)
* it is not immediately clear how variables are defined because code is in another file can

# Creating a Rmarkdown File
Rmarkdown (`.Rmd`) can be made in RStudio with `File > New > Rmd`, or use your favourite text editor. Rmarkdown is usually saved in the relevant `devel` directory, in the same location as the accompanying R script. 

## Elements of an Rmarkdown
This section breaks down the different elements of an Rmarkdown, but see the [Rmarkdown book](https://bookdown.org/yihui/rmarkdown/) for more details. For a quick view on how to write an Rmarkdown, please see the [example below](#example-rmarkdown).

### Preamble
Rmarkdown begins with a preamble that specifies the title of the report, author, date, and output parameters. The preamble is where you specify the the type of file rendered (usually `.html` or `.pdf`). You can also specify a table of contents.

### R Chunk Options
This section is where you set up the options for how the you want all R chunks in the document to behave using `knitr::opt_chunks$set()`. For example, if you want all code in R chunks to be printed, you can set `echo=TRUE`, if you want the R code to be run, set `eval=TRUE`. This is also where you load the R packages necessary to run the code in the R chunks, though no necessarily the packages needed by the R script (those packages are called within the R script itself). Lastly, you can source any R scripts or R functions in this section.

### Body of the text
You can populate the report with text much like you would any markdown, though there are some Rmarkdown-specific syntax. The example report showcases some commonly used syntaxes, such as sections and subsections, tabs, tables.

### R Chunks 
This is where you can include R code in your report, where code in the chunk are run (or not run, depending how the chunk is specified). You can set chunk options for individual chunks, which override the global chunk options set after the preamble. For example, if you have `echo=FALSE` (does not print code) in the global chunk options, but want to show the code for this specific R chunk, you can specify `echo=FALSE` in this chunk's options. You can also use chunk options to set figure sizes.

# Rendering Reports from Rmarkdown
Rmarkdown can generate reports in various formats, most common outputs are `.pdf` or `.html` files, depending on how you set up your Rmarkdown.

There are three ways you could render the report from Rmarkdown:

* In RStudio, clicking `knit` in RStudio
* In the R console, run `knitr::knit('example_report.Rmd')` 
* In the command line, load the relevant R module, and run 
`Rscript -e "knitr::knit('example_report.Rmd')"`
or
`Rscript -e "rmarkdown::render('example_report.Rmd', output_format='html_output')"`

# Example Rmarkdown 
Notice that the Rmarkdown source an R script, where the bulk of the analysis takes place.
````
---
title: "Report Title"
author: "Your Name"
date: "`r format(Sys.time(), '%Y-%m-%d')`"
output: 
  html_document:
    toc: true
    toc_float:
      collapsed: false
    toc_depth: 3
    number_sections: true
---

```{r setup, include=FALSE}
# set up r chunk parameters
knitr::opts_chunk$set(echo = FALSE, warning = FALSE, message = FALSE)

# load any r packages that are required in R chunks (not necessarily packages required in source R script)
require(knitr)

# run analysis script
source("example_script.R")
```

# Purpose
The purpose of the report, or the purpose of the analysis.

# Study overview
Simple description of the study, number of samples

# Data overview
Simple description of the read-outs from the study, or description of the data analysed in the current analysis.

# Analysis Header
## Analysis Subheader

# Tabbed section {.tabset}
The `{-}` in the header removes numbering.

## First tab {-}
tab1

## Second tab {-}
tab2

# Show analysis with R chunk.
You can give brief description of analysis, observations etc. You can optionally give the chunk a name. This can help you identify what chunk is being run while rendering the Rmarkdown (and where it's failing). Chunk names must be unique.

```{r chunkname}
plot1
```

You can set figure dimensions in inches the chunk options.

```{r longplot, fig.width=4, fig.height=8}
plot2
```

You can embed some r code within text. For example, The study has `r n_sample` samples. 

You can show tables in R chunks. `knitr::kable()` gives a relatively nice print-out.
```{r}
kable(table1)
```

You can show fancy tables using the `DT` package
```{r}
DT::datatable(table1, filter='top')
```

You can show R code in R chunks by setting `echo=TRUE` in the chunk option
```{r, echo=TRUE}
x <- c(rnorm(50, 10, 0.5), rnorm(50, 4, 0.01))
ddata <- data.frame(panel=rep(LETTERS[1:2], each=50), x, y = x*2.5)
summary(ddata)
```

You can also show R outputs
```{r}
summary(ddata_lm)
```

# Rendering R markdown into html
You can use the `knit` button in RStudio, or you can run from R console

`knitr::knit(example_report.Rmd)` 

````

## Example R Script
This is the R script that accompanies the example Rmarkdown above.
````
# Brief description of analysis performed in script
# This is some dummy code to run the example report

# load requried packages
require(ggplot2)

# read in data--------------------------------------------
set.seed(1)
x <- c(rnorm(50, 10, 0.5), rnorm(50, 4, 0.01))
ddata <- data.frame(panel=rep(LETTERS[1:2], each=50),
                    x, y = x*2.5)

ddata_lm <- lm(y~ x, ddata)

# plot 1
pdata <- ddata[ddata$panel == 'A',]
plot1 <- ggplot(pdata, aes(x=x, y=y)) +
    geom_point() +
    geom_smooth(method='lm') +
    theme_bw(14)

 # long plot
 plot2 <- ggplot(ddata, aes(x=x, y=y)) +
 	geom_point() +
 	geom_smooth(methdd='lm') +
 	facet_wrap(~panel, scales='free', ncol=1) +
 	theme_bw(14)

# some example table
 table1 <- data.frame(group=rep(LETTERS[1:3], each=4),
                      feature=rep(letters[24:26], 4),
                      value=rnorm(12, 40, 3))
n_sample <- nrow(table1)

````

# Example HTML Report
The output `html` report rendered from the example Rmarkdown can be found on the OCMS Bioinformatics Teams channel, under `Files > SOPs > example_report.html`