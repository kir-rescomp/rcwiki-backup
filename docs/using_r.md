---
title: R
description: Working with R
published: true
date: 2024-10-09T10:07:32.939Z
tags: r
editor: markdown
dateCreated: 2021-10-19T11:20:22.547Z
---

# R on the BMRC cluster

# Tabs {.tabset}
## gompi/foss-2022b/GCC/GCCcore-12.2.0
### Available R versions

The up-to-date versions of the main R software are installed centrally and can be listed by running:

```
module avail R
```

To maintain compatibility with various other software used at the Kennedy Instutite, please load the software built with a toolset compatible across many other packages, such as `foss-2022b`. The version of R that is compatible across the RStudio Workbench server and free RStudio that can be run on the cluster is `R/4.3.1-foss-2022b-bare`.

> At the Kennedy Institute we encourage use of minimal versions of R modules (so-called "bare" versions). This allows users more control over what packages they install into their own R environment.    
{.is-info}

So, you can load the R module by running:

```
module load R/4.3.1-foss-2022b-bare
```

### Installing local packages

To install local packages please follow the steps below.

> To maintain continuity with previous set up of the cluster, we will keep installing the local packages for Skylake CPU architectures into a separate directory called `skylake`. 
{.is-info}

#### Skylake

1. Log on to any of login nodes.

2. First, create a folder to be the main repository directory. This should be a new folder. Please do not re-use an existing folder of R packages, for example, the one transferred from elsewhere. If you have an existing R folder that has been copied from another cluster, it is important to rename it or delete all its content:

```
mkdir -p ~/devel/R
rm -r ~/devel/R/*
```

3. Using your favourite text editor, create the R profile file in your home directory `~/.Rprofile` and add the following code in the beginning of the file, replacing `group` and `username` with your corresponding values.  

- R_LIBS_BASE="/well/`group`/users/`username`/devel/R"
BMRC_RPROFILE="/apps/misc/R/bmrc-r-user-tools/Rprofile"
if (Sys.getenv("SINGULARITY_CONTAINER") == "") {
source(BMRC_RPROFILE)
options(bitmapType='cairo-png')
} else {
print("[BMRC] Warning: The BMRC Rprofile has been de-activated because R is running inside a singularity container.")
}

{.grid-list}

> Before saving the `~/.Rprofile` file, please add one blank line at the end of the code or the file will not load.
{.is-warning}

> For BMRC-provided Singularity container users (such as, for example, SAIGE container users), the code above ensures that the BMRC-provided Rprofile is loaded when running R directly on the cluster and de-activated when running inside a Singularity container.
{.is-info}

4. Your R setup is ready for testing. Load an R module and then start R by the R command:

```
module load R/4.3.1-foss-2022b-bare
R
```
You should see an output like the following:

- [1] "[BMRC] You have sourced the BMRC Rprofile provided at /apps/misc/R/bmrc-r-user-tools/Rprofile"
[1] "[BMRC] Messages coming from this file (like this one) will be prefixed with [BMRC]"
[1] "[BMRC] You are running R on host `<XXX>` with CPU `<YYY>`
[1] "[BMRC] While running on this host, local R packages will be sourced from and installed to /well/`group`/users/`username`/devel/R/`R version`/`architecture`"
{.grid-list}
  
The path in the final line will be an extension of your `R_LIBS_BASE` variable, with sub-directories added for the R version and the CPU architecture.

As a final check, from within R run the `.libPaths()` command and check that the first entry shows the same directory as specified in the last line of the output above.

5. Once you have tested your setup using the instructions in step 4, install your own packages by using the usual commands within R, for example: 
  
```
  install.packages("zip") 
```  
to install the zip package.

  Exit R by typing `q()`

> Some packages may require access to cmake for installation. The compatible module of cmake can be loaded by `module load CMake/3.24.3-GCCcore-12.2.0` command before or just after loading the R module.
{.is-info}

> To install `hdf5r` package, please run the following command:
{.is-warning}

```
install.packages("hdf5r", configure.args="--with-hdf5=/apps/eb/2022b/skylake/software/HDF5/1.14.0-gompi-2022b/bin/h5pcc")
```
  
### Troubleshooting

If something goes wrong in this setup, an informative error message should be printed with the "[BMRC] ..." prefix and R will automatically quit. The messages will indicate the possible source of error.  

## gompi/foss-2020a/GCC/GCCcore-9.3.0
### Available R versions

The up-to-date versions of the main R software are installed centrally and can be listed by running:

```
module avail R
```

To maintain compatibility with various other software used at the Kennedy Instutite, please load the software built with a toolset compatible across many other packages, such as `foss-2020a`. The version of R that is compatible across the RStudio Workbench server and free RStudio that can be run on the cluster is `R/4.1.2-foss-2020a-bare`.

> At the Kennedy Institute we encourage use of minimal versions of R modules (so-called "bare" versions). This allows users more control over what packages they install into their own R environment.    
{.is-info}

So, you can load the R module by running:

```
module load R/4.1.2-foss-2020a-bare
```

### Installing local packages

To install local packages please follow the steps below.

> To maintain continuity with previous set up of the cluster, we will keep installing the local packages for Skylake CPU architectures into a separate directory called `skylake`.  
{.is-info}

#### Skylake

1. Log on to any of login nodes.

2. First, create a folder to be the main repository directory. This should be a new folder. Please do not re-use an existing folder of R packages, for example, the one transferred from elsewhere. If you have an existing R folder that has been copied from another cluster, it is important to rename it or delete all its content:

```
mkdir -p ~/devel/R
rm -r ~/devel/R/*
```

3. Using your favourite text editor, create the R profile file in your home directory `~/.Rprofile` and add the following code in the beginning of the file, replacing `group` and `username` with your corresponding values.  

- R_LIBS_BASE="/well/`group`/users/`username`/devel/R"
BMRC_RPROFILE="/apps/misc/R/bmrc-r-user-tools/Rprofile"
if (Sys.getenv("SINGULARITY_CONTAINER") == "") {
source(BMRC_RPROFILE)
options(bitmapType='cairo-png')
} else {
print("[BMRC] Warning: The BMRC Rprofile has been de-activated because R is running inside a singularity container.")
}

{.grid-list}

> Before saving the `~/.Rprofile` file, please add one blank line at the end of the code or the file will not load.
{.is-warning}

> For BMRC-provided Singularity container users (such as, for example, SAIGE container users), the code above ensures that the BMRC-provided Rprofile is loaded when running R directly on the cluster and de-activated when running inside a Singularity container.
{.is-info}

4. Your R setup is ready for testing. Load an R module and then start R by the R command:

```
module load R/4.1.2-foss-2020a-bare
R
```
You should see an output like the following:

- [1] "[BMRC] You have sourced the BMRC Rprofile provided at /apps/misc/R/bmrc-r-user-tools/Rprofile"
[1] "[BMRC] Messages coming from this file (like this one) will be prefixed with [BMRC]"
[1] "[BMRC] You are running R on host `<XXX>` with CPU `<YYY>`
[1] "[BMRC] While running on this host, local R packages will be sourced from and installed to /well/`group`/users/`username`/devel/R/`R version`/`architecture`"
{.grid-list}
  
The path in the final line will be an extension of your `R_LIBS_BASE` variable, with sub-directories added for the R version and the CPU architecture.

As a final check, from within R run the `.libPaths()` command and check that the first entry shows the same directory as specified in the last line of the output above.

5. Once you have tested your setup using the instructions in step 4, install your own packages by using the usual commands within R, for example: 
  
```
  install.packages("zip") 
```  
to install the zip package.

  Exit R by typing `q()`

> Some packages may require access to cmake for installation. The compatible module of cmake can be loaded by `module load CMake/3.16.4-GCCcore-9.3.0` command before or just after loading the R module.
{.is-info}

### Troubleshooting

If something goes wrong in this setup, an informative error message should be printed with the "[BMRC] ..." prefix and R will automatically quit. The messages will indicate the possible source of error.  

