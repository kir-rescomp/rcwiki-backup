---
title: Initiating a new project
description: Starting a new project
published: true
date: 2023-05-05T11:57:08.201Z
tags: sop
editor: markdown
dateCreated: 2023-04-26T11:24:57.447Z
---

# Initiating new projects

New OCMS projects should take the notation `CMS###_XXXX` where the numbers correspond to the OCMS project number and the 4-letter suffix are the first two letters of the collaborator's first name and last name. In some cases, the letters correspond to the first 4 letters of the study name

# Set up project directories
You can run the following code to set up all necessary project directories for a new project:
```
mkdir ~/projects/NEW_PROJECT
mkdir ~/projects/archive/NEW_PROJECT
mkdir -p ~/devel/NEW_PROJECT/code
mkdir -p ~/work/NEW_PROJECT/analysis
ln -s ~/devel/NEW_PROJECT/code ~/work/NEW_PROJECT/code
```

Or you can install the OCMS_Sandbox command line interface and run:
```
ocms new_project --project_name=NEW_PROJECT --level=both
```

`-p` or `--project_name` is the new project name
`-l` or `--level` is the level at which new projects should be made. Takes `group`, `user`, or `both`. `--level=group` creates the directories in `projects` and `archive`. `l-level=user` creates directories in `devel` and `work`. `--level=both` makes all directories. You may want to set `--level=user` if the project has already been created in `project` and `archive` and you just need the directories in your own user space.

# Download data and cheksums
Download data from a link. If the data is coming from OGC, they will include the link in an email. Make sure you are on the head node (not an interactive session -- internet connection only available on head node). Enter the the relevant `archive` directory.

```
wget -r LINK
```

Create mapping file by:
* copy sample IDs from email body into a text file
* save as `.txt` E.g. WT2CMS001.txt
* save/copy mapping to relevant `archive` directory on BMRC
* format the mapping file by replacing spaces with tabs and getting rid of "Sample:" prefix:

```
cat WT2CMS001.txt | sed 's/ /\t/g' | cut -f1,2 | sed 's/Sample://g' > WT2CMS001.tsv
```

Go into the downloaded directory and perform md5 checksuns on downloaded files to make sure files to make sure files downloaded properly. Change to OGC project number accordingly
```
md5sum * > CMS001_md5sum.txt
md5sum -c CMS001_md5sum.txt P14256-md5sum.txt > CMS001_check.txt
```

Check that no files have failed
```
cat CMS001_check.txt | grep -v OK
```

Remove `.bam` and `.bam.bai` files
```
rm -rf *bam
rm -rf *bam.bai
```