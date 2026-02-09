---
title: Frequently asked questions
description: 
published: true
date: 2025-07-31T15:37:52.037Z
tags: 
editor: markdown
dateCreated: 2025-07-31T14:41:35.209Z
---


## What can I do to schedule an interactive job more quickly? 

If you are experiencing excessive wait times for scheduling an interactive session with srun, please try submitting the request against the "kir.prj.high" account:

`srun -c2 --account=kir.prj.high -p short --pty /bin/bash`

> **Please note that the "kir.prj.high" account may only be used for this purpose**, and **you should only submit one job to this account at any one time**. Jobs submitted to this account will take priority over other KIR jobs: if you abuse this account your access to the cluster may be withdrawn. Use of this account is monitored. 
{.is-warning}


## What can I do to make my cluster jobs run faster?

First, please profile your jobs to understand their core, memory and walltime requirements. Then only ask for the resources that you need, as jobs with smaller resource requirements get scheduled more quickly.

The total time it takes a task to complete includes the time it waits in the queue to be scheduled for execution, and then the time it takes to execute when allocated to a node. It is therefore very important to balance the factors that affect the wait time in the queue with those that affect the run time. For example requesting 16 cores may lead to a very long wait for scheduling. You might find that your job completes more quickly if you request e.g. 4 cores, even though the execution phase was longer.

In particular, please note that:

1. Jobs with lower CPU requirements tend to be scheduled more quickly.
2. Jobs with shorter walltime limits can be scheduled more quickly. This is because the BMRC uses backfill scheduling and this fits short jobs in around existing jobs when possible.
3. It is possible to request CPU and memory requirements seperately. If you need 1 core + 32GB memory, your job will be scheduled faster if you ask for 1 core + 32GB memory than if you ask for 2 CPUs (by default each core is tied to 16GB RAM).


