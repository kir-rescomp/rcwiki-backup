---
title: OCMS Modulefiles
description: How to access module files for OCMS pipeline configuration
published: true
date: 2023-09-25T15:26:48.621Z
tags: module, pipelines, sop
editor: markdown
dateCreated: 2023-09-25T15:26:48.621Z
---

# OCMS Modulefiles 

How to access modulefiles for OCMS pipeline configuration


# OCMS Modulefiles 

BMRC uses [Modules](https://modules.readthedocs.io/en/latest/module.html) and the `module` command to handle loading of software. As OCMS pipelines have a number of software dependencies, we provide pipeline-specific modulefiles for their convenient loading. 

# Setting Up Access to OCMS Modulefiles

To ensure `module` has access to modulefiles specifying OCMS pipeline dependencies, either run the following from the commandline, or add it to your ~/.bashrc: 

```
module use /well/kir-ocms/shared/apps/modulefiles/ocms
```

You should subsequently be able to see this path (and the modulefiles it contains) among the locations seen when running `module avail`. 


# Loading Software Dependencies for a Specific Pipeline


Once you have access to OCMS modulefiles, environments for specific pipelines are stored within an `pipelines` subdirectory in subdirectories that correspond to the pipeline name. For example, the environment for pipeline_preprocess.py will be located in `pipelines/preprocess/`. It can be loaded by running the following command: 

```
module load pipelines/preprocess
```

## Loading a Specific Pipeline Version

By convention, actual modulefiles are stored in a directory named after the software they load (e.g. Bowtie2). Within a software directory, there can therefore be modulefiles pertaining to multiple software versions, each named according to the version number (e.g. Bowtie2/1.2.3, Bowtie/2.4.1, etc).  If no version is specified when using module to load software, typically this will load the highest version number available in the specified directory (in this example `module load Bowtie` would load Bowtie v2.4.1).

Going forward, OCMS pipeline dependencies will also be versioned to a) accomodate changes to a pipeline, or b) conform to the latest toolchains/GCC versions used to compile software on BMRC. 

We recommend not specifying a pipeline version when loading pipeline software dependencies. However, if you need to run an earlier version of a pipeline, or use an earlier BMRC software build, then you can always specify the full file path to the required module path (e.g. `module load pipelines/preprocess/1.0`).

Details of the toolchain/GCC version loaded for a specific pipeline should be available via the `module help` command. For example:

```
module help pipelines/preprocess/1.0
```

# NOTE: 

OCMS pipeline modules make no assumption about the versions of R and Python you are running. It is your responsibility to ensure your R/Python versions are compatible with the compiled software versions required to run a pipeline. 