---
title: Research Computing at the Kennedy Institute of Rheumatology
description: Computational resources at the Kennedy Institute
published: true
date: 2026-02-10T09:38:24.727Z
tags: 
editor: markdown
dateCreated: 2021-06-25T09:54:12.658Z
---

# Tabs {.tabset}

## General

### High-performance computing

High-performance computing (HPC) at the Kennedy Institute of Rheumatology is provided in collaboration with Biomedical Research Computing (BMRC). This facility is called the "KIR BMRC Shared Reserarch Facility (SRF)".

The services include:

- High-performance batch (cluster) computing, as well as specialised hardware and software to run GPU-enabled and AI/Machine Learning codes
- Large, fast storage systems supported by ultra-fast networking
- Low-cost data storage
- On-premise cloud computing (OpenStack)
- Training and workshops on using these facilities

<br>

### Rules and regulations

Access to the HPC systems and services are provided for authorised work purposes only. 

In using them you are bound by the terms and conditions of the [University of Oxford's IT Regulations](https://governance.admin.ox.ac.uk/legislation/it-regulations-1-of-2002), the [NDORMS Information Security Policy](https://www.ndorms.ox.ac.uk/information-security-policy) and you must follow the [KIR Information Governance Policy](information_governance).

 Where necessary, and within the relevant laws and regulations, the Kennedy Institute and the University of Oxford reserve the right to exercise control over all activities employing its computer facilities, including examining the content of users' data.

<br>

### Cluster overview

The BMRC cluster is a shared computational resource to allow a large number of users to do useful computing work in a way that is typically easily scalable, better organised, more reliable and more cost-effective than running it on personal desktops or laptops. In basic terms, it comprises some computers, called *nodes*, shared disk storage, and a special software, called *scheduler* to coordinate all the different computing work that different users wish to run. There is a wide range of pre-installed scientific software plus the means to add additional custom software.

> A typical workflow when using the cluster is as follows. First, you use your own computer to login to a login node. Then you prepare and submit one or more computing jobs to the scheduler, specifying the queue, software and resources needed to execute your job. The scheduler then takes care of choosing which cluster node will run it. You can use data stored on disk as inputs to your computing job. Finally, the output files produced by your jobs, together with some log files containing information about where and how your job ran, are also stored in your disk space. Later, you re-login to a login node and view the outputs of your computing jobs on disk.
{.is-info}

> It is important to remember that the login nodes are reserved solely for the purpose of preparing and submitting computing jobs to the scheduler, which will then send them to a cluster compute node for execution. For this reason, the computing jobs **MUST NOT** be run directly on the login nodes themselves. Any jobs running on login nodes (i.e. without submitting them to the scheduler) are liable to be stopped by the BMRC team. This policy helps to ensure that the login nodes are always available to everyone for their intended use.
{.is-warning}

An overview of the cluster organisation, types and specifications of compute nodes and queues are summarised in the diagram below. 

```plantuml
'left to right direction
'skinparam BackgroundColor transparent
skinparam rectangle {
	fontSize 25
  roundCorner 25
}
skinparam arrow {
	Color Blue
  fontName Arial
  fontSize 15
  Thickness 3
}
skinparam node { 
  backgroundColor Yellow
}
skinparam queue {
  backgroundColor LightGreen
  borderColor Black
}
skinparam actorStyle awesome
skinparam actor {
  borderColor Blue
  backgroundColor Blue
}
actor "User 1" as u1
actor "User 2" as u2
actor "User 3" as u3
actor "User ..." as u4

rectangle "BMRC cluster" {
	storage "GPFS shared file system" as f
  node "Login nodes:\n cluster1.bmrc.ox.ac.uk\n cluster2.bmrc.ox.ac.uk\n cluster3.bmrc.ox.ac.uk\n cluster4.bmrc.ox.ac.uk\n" as nl
  queue "SLURM scheduler" as q
	node "48 A nodes\nSkylake\n48 cores/node\n15.2 GB/core" as nc #SkyBlue  
  node "102 E nodes\nSkylake\n24 cores/node\n15.2 GB/core" as ne #LawnGreen
  node "16 F nodes\nSkylake\n40 cores/node\n4.2 GB/core" as nf #Pink
  node "High-memory nodes\nare being configured" as nh #LightBlue
  node "21 GPU (G) nodes\nSkylake\n12 to 48 cores/node\n4.2 to 124 GB/core" as ng #Red
  node "4 Epyc nodes\nAMD Epyc\n32 to 128 cores/node\n4.2 to 15.2 GB/core" as nep #White 
}
u1 --> nl : ssh
u2 --> nl : ssh
u3 --> nl : ssh
u4 --> nl : ssh
nl -> q : srun\n sbatch
q --> nc : short\n long
q --> ne : short\n long
q --> nf : short\n long
q --> nh : himem
q --> ng : gpu_short\n gpu_long
q --> nep : epyc
nl -- f
nc -- f
ne -- f
nf -- f
nh -- f
ng -- f
nep -- f
```

## Getting started

- [Opening an account *How to get an account on the cluster*](/account)
- [Information Governance *Information Governance*](/information_governance)
- [Accessing the cluster *How to connect to the cluster*](/access)
- [File system *Files organisation on the cluster*](/filesystem)
- [Software *How to work with software and software modules*](/software)
- [Submit a job to the cluster *How to use the computing power*](/job_submission) 
- [Setting up Python virtual environment *Working with Python*](/python_venv)
- [Running Jupyter Notebook or Lab *How to run and access a Jupyter Notebook or Lab*](/jupyter)
- [Working with Conda *How to work with Conda*](/conda)
- [Using R *How to work with R*](/using_r)
- [RStudio server *How to work with R interactively*](/rstudio)
- [GPU Resources *How to request GPUs](/gpu_resources)
{.links-list}

## Group pages

- [Johnson group](/johnson)
- [Jostins group](/jostins)
- [Sansom group](/sansom)
- [OCMS group](/ocms)
- [Powrie group](/powrie) 
{.links-list}

## Getting Help

- [Getting Help](/getting_help) 
{.links-list}

## FAQ

- [FAQ](/faq) 
{.links-list}


