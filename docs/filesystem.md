---
title: File system
description: The file organisation on the BMRC cluster
published: true
date: 2025-11-11T12:57:05.144Z
tags: file system, storage quota
editor: markdown
dateCreated: 2021-06-25T15:16:14.633Z
---

# File organisation
## Home folder

On the BMRC cluster, there are two folders for each user - home folder and file folder.

Your home folder is located at `/users/"group"/"user"` - with `"group"` and `"user"` being your group name and username, which is a random combination of three letters and three numbers. To easily recognise users behind these user names it is possible to set up customisable [nicknames](/nicknames). 

> The size of the home folder is limited to **10 GB** - you should use it only for storing essential configuration files which software often expects to find there, like the Bash configuration file `.bashrc`.
{.is-warning}


## Automatic backups

The BMRC does not provide any backup for data on its systems. It uses a redudant array for data storage that is resilent to individual disks failing.

For KIR groups, the Kennedy automatically backs up two designated locations, these are:

1. ~/devel (/well/"group"/users/"user"/devel) - this folder is where project code should be kept.
2. ~/notebooks (/well/"group"/users/"user"/notebooks) - this folder is where code notebooks should be kept.
3. ~/archive (/well/"group"/projects/archive) - this is the folder where raw data should be kept.

In the highly unlikely event of a failure of the BMRC filesystem, the KIRs philosopy is that recovery of the code and the raw data should be sufficient to reproduce any analyses.

> It is also strongly recommended that users version control their code on github.
{.is-info}

## Purpose of `projects` and `shared` folders

1. `projects`is for **intra-group** sharing
2. `shared`	 is for **inter-group** sharing

## File locations

Your folder for general files is located at `/well/"group"/users/"user"`. Please use this folder to store your code, results of data analysis and other files.

> For convenience, symbolic links are set up in your home folder to point to the location in the file folder to organise the files according to their functionality or use, such as code development (devel), Jupyter notebooks (notebooks), individual and collaborative work at the group and Institute levels (work, projects and shared) and data storage (archive, mirror).
{.is-info}

These are:

<table>
	<tr>
    <td><b>Folder</b></td>
    <td><b>Linked location</b></td>
    <td><b>User permissions</b></td>
    <td><b>Group permission</b></td>
    <td><b>Backed up?</b></td>
  </tr>
  <tr>
		<td>~/devel</td>
		<td>/well/"group"/users/"user"/devel</td>
		<td>Read/Write</td>
		<td>Read</td>
    <td>Yes</td>
  </tr>
	<tr>
		<td>~/work</td>
		<td>/well/"group"/users/"user"/work</td>
		<td>Read/Write</td>
		<td>Read</td>
    <td>No</td>
  </tr>
	<tr>
		<td>~/notebooks</td>
		<td>/well/"group"/users/"user"/notebooks</td>
		<td>Read/Write</td>
		<td>Read</td>
    <td>Yes</td>
	</tr>
	<tr>
		<td>~/projects</td>
		<td>/well/"group"/projects</td>
    <td>Read/Write</td>
		<td>Read/Write</td>
    <td>No</td>
	</tr>
	<tr>
		<td>~/shared</td>
		<td>/well/"group"/shared</td>
    <td>Read/Write</td>
		<td>Read/Write</td>
    <td>No</td>
	</tr>
	<tr>
		<td>~/archive</td>
		<td>/well/"group"/projects/archive</td>
    <td>Read/Write</td>
		<td>Read/Write</td>
    <td>Yes</td>
	</tr>
	<tr>
		<td>~/mirror</td>
		<td>/well/kir/mirror</td>
    <td>Read</td>
		<td>Read</td>
    <td>No</td>
	</tr>
</table>

## **Storage quota**

The storage folder at `/well/"group"/users/"user"` shares in your group's allocation for disk space, so please use the space responsibly. Compress the files when not in use or for longer term storage.

To obtain current space use and allocated quota run:

```
df -BG /well/group
```
replacing `group` with your group name. 
