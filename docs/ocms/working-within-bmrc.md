---
title: Working within BMRC file system
description: SOP how OCMS members work within the BMRC file system
published: true
date: 2023-06-01T11:06:15.959Z
tags: sop
editor: markdown
dateCreated: 2023-04-26T11:19:30.681Z
---

# Working within BMRC File System
This page aims to outline how to operate within the BMRC file system. For more information on permissions and access for the different directories, please see the [File System page](/filesystem).

# Group vs Home Directory
The file system on BMRC is organized based on research group. Details on the file system can be found [here](https://rcwiki.kennedy.ox.ac.uk/en/filesystem). In short, there are two directories we need to familiarise ourselves with: the OCMS group directory and the home directory. The OCMS group directory is common to all members of `kir-ocms` group. The home directory is specific to the user, is is essentially a collection of symlinks to various directories in the group directory. This is illustrated in the diagram below, where the arrows represent symbolic links pointing to the source.

Each `kir-ocms` group member has a directory within `/gpfs3/well/kir-ocms/users/`. The `devel` and `work` directories under each user will be the main folders that we use, but more on this later. It's worth noting that `projects`, `archive`, and `shared` are originally located in the group directory, while `devel`, `work`, and `notebooks` are originally located in the home directory.

<img src=/ocms/group_vs_home_directories.png width=600/>

If a user is associated with more than one group, they will have multiple `$USER/devel` and `$USER/work` directories, one for every group they are affiliated with. For example, if `ysa365` is part of both OCMS and Powrie groups, then there will be a `/gpfs3/well/kir-ocms/users/ysa365` and `/gpfs3/well/powrie/users/ysa365`. However, each user only has one home directory, and it is associated with the user's primary group. So home directory of `ysa365` is `/gpfs3/users/kir-ocms/ysa365`.

# Archive
For legacy reasons, `archive` sits within `projects`. The purpose of `archive` is to house raw data, which should never be edited. This directory should contain only raw data, files generated from performing checksums, and identifier mapping files (maps OGC ids to our CMS ids). `archive` is organized according to OCMS project, then by data type, then by platform (if applicable). For example, if a CMS00X_XXXX had 16S, metagenomics, metabolomics, and transcriptomics data:

```
	/gpfs3/well/kir-ocms/projects/archive/
		|-- CMS00X_XXXX
				|-- 16S
				|-- metagenome
				|-- metabolome
				|-- transcriptome
				|-- metadata
```

Note there is a `metadata` subdirectory, this is to house any additional data on the samples. Usually, this is data collected in addition to -omic data, such as DNA concentrations, sample time points, patient data etc. For example, it is common to receive an excel file from a collaborator that gives participant or patient data associated with the study.

There is an  `archive/README` which should be updated every time a new project is created. The README should be updated with the following information and notation:

	CMS###_XXXX - [collaborator]; [data type]; [brief project description]; [who processed data]; [who analysed data]


# Projects
The purpose of `projects` is to house pipeline outputs. The idea behind this is that processed data may be used by multiple people, so keeping all pipeline outputs in a centralized location means pipelines only need to be executed once, and it is easy to see what pipelines have been run on a project. Just like `archive`, `projects` is organized by OCMS projects. Within each project, processed data is organized according to the pipelines, in subdirectories that are numbered according to the order in which they were run. Finally, outputs of pipelines are symlinked into a `data` directory. The purpose of the `data` directory is to be centralized location from which data at every stage of analysis are easily accessible. For example: 

```
/gpfs3/well/kir-ocms/
|-- projects
|	|--CMS00X
|		|-- 1_metagenome_pipeline_readqc
|		|-- 2_metagenome_pipeline_preprocess
|		|-- data
|			|--metagenome_renamed
|			|--metagenome_preprocessed
|		|-- README
|	|-- archive
|		|-- CMS00X
|			|-- metagenome
|			|-- metabolome
|		|-- CMS00Y
|		|-- CMS00Z
|		|-- README
|-- shared
|-- users
```

In the example above, CMS00X_XXXX has metagenomics and metabolomics data stored in `archive`. The metagenomics data has been renamed so fastq file names are changed from OGC IDs to CMS IDs, then `readqc` was run on the fastqs for quality control purposes, then finally, sequences were pre-processed using the `preprocess` pipeline. It's imperative that all progress for a given project is documented with a `projects/CMS00X_XXX/README`.

There is a `projects/README` that describes older projects that don't follow this format because they were transfered over from kgen (before BMRC).

# Linking Pipeline Inputs and Outputs
As mentioned earlier, each OCMS project within the `projects` directory has a `data` directory. The purpose of the `data` directory is to easily access the data at various points in the analysis. As such, `data` acts as an access point for all pipelines and analyses, where the outputs of pipelines are symlinked into the `data`, which can then by used (via symlink) as the input for other pipelines or analyses. Using the example above, we can illustrate how the inputs and outputs of pipelines are centralized around the `data` directory:

<img src=/ocms/projects_and_archive_expanded.png width=500/>

In our example, raw fastq files were renamed using `ocms combine_lanes`, which symlinks and renames the files at the same time. Therefore, renamed files will go in `data/metagenome_renamed`. The symlink between renamed files and raw files is shown by the blue arrow. `pipeline_preprocess` used renamed fastas as the input, so we symlink (purple arrow) the renamed fastas into `2_metagenome_pipeline_preprocess`, the directory where we are running the pipeline. The output of `pipeline_preprocess` are processed fastqs that will be used in downstream analyses. Therefore, the outputs of `pipeline_preprocess` are symlinked to `data/metagenome_preprocessed` (green arrow)


# Devel
The purpose of `devel` is to house code. This includes in-house OCMS pipelines and bespoke analysis for particular projects. OCMS projects within `devel` should be organized into their own directories, with a subdirectory called `code`. This `code` subdirectory houses any code developed to peform analysis on that particular project. Python virtual environments and local R libraries are also housed here. Since `devel` is not meant to be shared amongst users, how you organize your `devel` is up to you. If you have code that is meant to be shared, see section on [Collaborative Coding]([collaborative-coding](/ocms/collaborative-coding)).

# Work
The purpose of `work` is to house any analysis done outside of running a pipeline. Again, OCMS projects each get their own directory, and have the subdirectories `analysis`, `code`, and `data`.

`code` is symlinked to `devel/CMS00X_XXXX/code` of the corresponding project. This makes it more transparent to see how the analysis was done.
`analysis` houses the any analysis outputs
`data` houses any data that you may need as inputs for `code`. This can be symlinked to pipeline output files (in `projects`) or it can be an output from code. For example, usually you will need to do some bespoke data wrangling when reading in data from various pipelines. You may want to have a script that gathers and cleans up the various sets of data, write the cleaned up version to `data`, which can then be used in different analyses down the line.

An example of your `devel` and `work` directory for a given OCMS project is:

<img src=/ocms/devel_and_work.png width=300/>

# Rmarkdown and Python notebooks
These two types of documents are great ways to document your analysis. Even though there is a `notebooks` directory in the group and home directories, I find that in practice, `Rmd` (along with its rendered `html`) and `ipynb` files generally end up in `code`. 
