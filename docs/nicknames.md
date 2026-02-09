---
title: Nicknames
description: Display customisable nicknames instead of BMRC user names in commands output
published: true
date: 2023-03-16T10:35:43.565Z
tags: nicknames
editor: markdown
dateCreated: 2022-02-24T16:06:35.208Z
---

# Nicknames

There is a possibility to set up and display customisable nicknames insted of BMRC user names in outputs of various commands, such as, for example `ls`

## Set up

1. To be able to use the nicknames load the corresponding module: 

```
module load nicknames/1.0 
```

2. In your home directory create a `.nick` file with two columns. The first column lists the BMRC user name, and the second column defines the nickname assigned to that user name and which will be displayed in the output. For example,

```
ccx298 Konstantin
apq902 Brian

```

The nickname can be an alphanumeric string without spaces.

3. Set up an alias for a command that will decode the BMRC user names into corresponding nicknames in the `.bashrc` file. For example, the following commands will be equivalent of the `ls` and `qstat` commands but use nicknames instead of user names in displaying file/directory/process ownership:  

```
lsnick() { nick2bmrc /usr/bin/ls $@ | bmrc2nick -left -field 2 ; }
qstatnick() { nick2bmrc -lists ',' /gpfs3/mgmt/uge/8.6.8/bin/lx-amd64/qstat $@ | bmrc2nick -left ; }
```

4. To activate modified .bashrc file use `source ~/.bashrc` command. The nickname-substituted `ls` command can then be invoked by entering:

```
lsnick
```

Other commands that display ownership can be similarly modified.
