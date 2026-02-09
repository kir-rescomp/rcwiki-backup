---
title: Job submission
description: How to submit a job to the cluster
published: true
date: 2024-11-05T15:44:03.073Z
tags: submit, job, srun, sbatch, efficiency
editor: markdown
dateCreated: 2022-09-29T12:58:28.352Z
---

# Submit a job to the cluster

# Tabs {.tabset}
## Queueing system

A shared computing cluster is used by many different users to run many different types of computing jobs. To do this a special software, called scheduler, distributes submitted jobs among many different types of cluster nodes in a way that is fair and makes efficient use of available compute resources. 

> The jobs on the cluster are managed by SLURM scheduler.
{.is-info}

To assist in this task, the scheduler runs a number of different queues knows as partitions. Each partition provides different sets of resources from other partitions and users are required, when submitting a job, to choose which partition is the most suitable. The two general partitions that are suitable for most purposes are `short` and `long`. These partitions submit jobs to any node that has the required resources and differ by the maximum time for which a job can run. If your computing job will complete in under 30 hours, then you should use the short partition. For longer jobs, we have long partition where the maximum running time is ten days. 

There are two different but complementary ways of getting your code running on the cluster - by submitting interactive and batch jobs.

## Interactive jobs

Using the `srun` command you can request an interactive cluster session in which you are given a live terminal (aka shell) on one of the cluster compute nodes with the amount of slots (CPU and RAM) you have requested. An interactive cluster session allows you to type commands and run code live from the terminal, which is the recommended way, as no jobs should be run on the login nodes.

> Since you are given an interactive Bash shell, your shell environment will automatically execute both your ~/.bash_profile and ~/.bashrc files to perform its setup. This is different to sbatch scripts where no startup files are processed (neither ~/.bashrc nor ~/.bash_profile).
{.is-info}


To request a simple interactive session with 1 CPU slot and default 15.2 GB of memory, run:

```
srun -p short --pty bash
```

To request an interactive session with several slots on a node (three in the example below with the deafult 15.2 x 3 = 45.6 GB of memory) use the following command:

```
srun -p short --cpus-per-task=3 --pty bash
```
or equivalent
```
srun -p short -c 3 --pty bash
```

> Always request an appropriate number of slots that you intend to use in your session. For example, if you are going to run software that requires 4 computing slots, request 4 slots in the interactive session. 
{.is-warning}

The output you see on screen will look as follows:

- srun: job 88440 queued and waiting for resources
srun: job 88440 has been allocated resources
\[username@compa002 ~\] $
{.grid-list}

In the above output, you can read that your srun session has been successfully scheduled and you have been given an interactive cluster session on compa002. Notice how the prompt changes to [username@compa002] to show that you are now working on one of the cluster compute nodes rather than on rescomp1/2.

When you have finished with your interactive session, logout as normal by typing e.g. `exit` and you will return to rescomp1/2. To avoid the risk of loosing your session in case the connection is lost accidentally or due to a long inactivity, we recommend starting your interactive job from within a `screen` or `tmux` session. 

The `srun` command accepts many of the same parameters and behaves similarly to the `sbatch` command described in **Batch jobs** section.

## Batch jobs

The most flexible method to submit a cluster job is to prepare and then submit a bash script file using an `sbatch` command. The bash script file can contain configuration settings for the scheduler, can load pre-installed software, can set any environment variables that your software needs, and then can launch your main software. A bash script is also useful when doing repetitive work such as running the same analysis several times with different input files (see **Array jobs** section).

We begin with a simple example. First, log on to `cluster1.bmrc.ox.ac.uk` following our access guide and ensure that you are in your home directory by running:

```
cd ~
```

Let's prepare our own simple bash script file. First of all, make a subdirectory in your home folder called sbatch_test and change directory into it:

```
mkdir sbatch_test
cd sbatch_test
```
Now, copy the contents below into a file named hello_world.sh in your sbatch_test folder. 

```bash
#!/bin/bash

echo "------------------------------------------------"
echo "Run on host: "`hostname`
echo "Operating system: "`uname -s`
echo "Username: "`whoami`
echo "Started at: "`date`
echo "------------------------------------------------"

sleep 60s
echo "Hello, World!"
```

> The first line in the script `#!/bin/bash` is a special command which says that this script should use the Bash shell. You will normally want to include this in every bash script file you write.
{.is-info}

In the next lines (all beginning `echo`...) we print some useful debugging information. This is included here just as an example.
The line `sleep 60s` causes our script to pause for 60 seconds.
The final line prints out the message ‘Hello, World!’

We submit the script to the scheduler to the short partition by running:

```
sbatch -p short hello_world.sh
```

- Submitted batch job 88480
{.grid-list}

### Job ID

When you submit the job, the scheduler will report back that it has received your job and assigned it an ID number. 

> The BMRC cluster handles so many jobs, it is not unusual to have a Job ID number in the millions. The ID number of your computing job is the most important piece of information about your job. When you ask for help with submitted jobs please remember to quote the Job ID.
{.is-info}

Now that your job has been submitted, if you are quick enough (within 60 seconds!) you can use the squeue command:

```
squeue -u your_username
```
to check the status of your job. The output will look something like the below.

```
							JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
							88480     short hello_wo username  R       0:14      1 compa008
```

You can see further details of the `squeue` command in the **Useful SLURM commands** section.  

> If no job name, partition or slots were specified, the job name is assumed to be the name of the script file, the job is assigned to short partition and is allocated 1 slot.  
{.is-info}


### Log files

When a cluster job is run, the scheduler automatically produces a file which it names in the format **slurm-jobid.out** in the current directory. 

> In Linux, running a command or a script in the terminal produces two output streams, called the Standard Output (stdout) and Standard Error (stderr). It can, of course, also send output directly to files on disk. Commands or scripts send their normal output to stdout while error messages go to stderr. When you run a command directly at the terminal, both streams are normally sent back to the terminal so you see them on screen. However, when running as a cluster job both streams are redirected to a file.
{.is-info}

If your job (`hello_world.sh`) has already finished, you will be able to see this file in your current working directory by running:

```
ls
```
This will list the output file in the sbatch_test folder:

- hello_world.sh slurm-88480.out
{.grid-list}

> If running the `ls` command does not show this file, wait a few more seconds and try again. It may be that the job is still queued. This can be revealed by `squeue -u <your_username>` command. 
{.is-info}

To see what is in the output file:

```
cat slurm-88480.out
```

This should give an output that looks something like this:

- Run on host: compa008.hpc.in.bmrc.ox.ac.uk
Operating system: Linux
Username: your-username
Started at: Wed Aug 08 12:54:28 GMT 2022
Hello, World!
{.grid-list}

The output shows that this script ran on the node compa008.hpc.in.bmrc.ox.ac.uk, however, you will likely see a different node. It also shows that the cluster node’s operating system was Linux, that the job was run as your username, and that the job started at the time shown - the outputs of the commands that we have included in the script. 

### Command line options and script parameters

The `sbatch` command accepts a wide range of configuration settings which can be used to modify the command. Here we review the most relevant ones.

As mentioned above, the option `-p` specifies which partition to submit to, and, for example, we could resubmit our example `hello_world.sh` script to a different queue as follows:

```
sbatch -p long hello_world.sh
```

Although we are resubmitting the same script `hello_world.sh` to the cluster, this still represents a new job so the scheduler will issue a new Job ID.

---

We can use `-J` option to specify a name for a job. By default, jobs are named after their script files, but using a name may be helpful.

```
sbatch -p short -J test hello_world.sh
```

The command above assigns name "test" to the submitted job.

---

To help with accounting we can specify the project that the job will belong to by using the `-A` option in the following command:

```
sbatch -p short -A project.prj hello_world.sh
```

You should replace project.prj with the name of your own project, if you have been allocated one.

> By default, the project is allocated to the Institute without using the -A option explicitly. 
{.is-info}

---

When a job is run by the scheduler, it will assume that your working directory is your current directory and it will write the standard output files there, unless you explicitly state what you want the working directory to be. 

To tell the scheduler to use a certain directory as working directory, you can specify it with the `-D` or `--chdr` option:

```
sbatch -p short -D $HOME hello_world.sh
```
The command above will write the script's output files into the user's home directory. 

---

The names of the standrd output and error files can be modified by specifying the options `-o` and `-e`, respectively:

```
sbatch -p short -J test -o output -e errors hello_world.sh
```

Now, the standard output will be written to file called "output" while the errors will be redirected to file called "errors" in your working directory.

> If only `-o` option is specified (or neither `-o` nor `-e` options), both error and output are written in the same file.
{.is-info}

---
`-c N` or equivalent `--cpus-per-task=N` requests N CPUs for the job. This can be used to run calculation on the same node with several slots.

> The higher the number of slots requested the longer it will normally take for your job to be scheduled. The maximum is 48 slots on A nodes, 24 slots on D and E nodes, 40 slots on F nodes, 46 slots on H nodes, and 96 slots on Epyc nodes, but you are advised to request less than the maximum available in order for your jobs to be scheduled within a reasonable time.
{.is-info}

---
  
`--wrap=<executable>` option wraps a binary automatically in a simple shell script so that it can be submitted with sbatch directly 

---

`--array <options>` declares an **Array job**. 

---

`--mem-per-cpu` option requests the specified allocation of memory per slot rather than default 15.2 GB. For example, `--mem-per-cpu=20G` will allocate 20 GB memory per requested core. If you know your job needs less than the default memory allocation, it will be beneficial to request an appropriate smaller amount as doing so will make it easier for the scheduler to find space to execute your job, so it will spend less time in the queue.

---

> By default, the SLURM scheduler makes a copy of the user's shell environment, including all environment variables, at the time of submission and adds these to the environment when your scheduled job is run on a cluster node. We strongly advise though using the `--export=NONE` parameter (which will not propagate any environment variable except those beginning with SLURM_ or SBATCH_) and putting all the code needed to setup your desired environment into your bash submission script.
{.is-warning}

### Submitting to specific host groups or nodes

Sometimes, you may wish to target which cluster nodes your job will run on more finely than by specifying just a queue. In this case, it is possible to add further information to your queue specification. 

For example, adding option `--constraint=hga` to `sbatch` command will submit only to A nodes, while `--constraint=skl-compat` will submit to only the nodes with Skylake or later CPU microarchitecture. The wider list of node groups that you can use for these purposes are:

- `intel` – an Intel CPU node
`skylake` (or `skl`) – a Skylake node
`skl-compat` – a node capable of running code compiled for Skylake
`cascadelake` (or `csl`) – a Cascadelake node
`csl-compat` – a node capable of running code compiled for Cascadelake
`hostgroupe` (or `hge`) – an E node
`hostgroupf` (or `hgf`) – an F node
`hostgroupa` (or `hga`) – an A node
`hostgrouph` (or `hgh`) – an H node
{.grid-list}

It is rarely desirable to limit submitting your job to a particular node, but in cases where this is needed, you can use the `-w` or `--nodelist` specification similarly to specifying a particular target node or list of nodes. 

For example, using option `–w compa020` you will submit your job to node **compa020**. 

### Defining parameters in the submit script

Typing all the desired options for job at the command line is certainly possible, but it also has disadvantages: not only does it require more typing, it makes it more difficult to record which options were used at a particular time. So, instead of having to type these options in every time, it is also possible to include them directly in our script file.

Let’s modify our hello_world.sh bash script file specifying the submit parameters in the script as below. Make sure to change the second line #BATCH -D /users/group/user/sbatch_test to reflect the path to your sbatch_test folder.:

```bash
#!/bin/bash
#SBATCH -D /users/group/user/sbatch_test
#SBATCH -A project.prj
#SBATCH -c 2
#SBATCH -J my-python-job
#SBATCH -p short
#SBATCH -o my-python-job-%j.out
#SBATCH -e my-python-job-%j.err

echo "------------------------------------------------"
echo "Run on host: "`hostname`
echo "Operating system: "`uname -s`
echo "Username: "`whoami`
echo "Started at: "`date`
echo "------------------------------------------------"

source /well/kir/config/modules.sh
module load Python/3.8.2-GCCcore-9.3.0

sleep 60s
python -c 'print("Hello, World!")'
```

The lines that use the special `#SBATCH` comment syntax are the options that we want to pass to our sbatch command. In particular:
- We specify `-D /path/to/qsub-test` so that the script will be run with the qsub-test folder as its current directory.
- We can specify our project name using `-A` (make sure to substitute your own project name if you have one or remove this line to use the default project).
- We request two slots by the `-c 2` option. This automatically allocates 2x15.2=30.4 GB of memory by default.
- We use `-J` to specify a name for this job. You can specify any name that would be helpful to you.
- We use `-p short` to request that the job should run on that particular queue.
- Finally, we use `-o my-python-job-%j.out` and `-e my-python-job-%j.err` to tell the sheduer to write the output and error messages in the corresponding specified files, where %j represents the Job ID.


As before, the next lines (all beginning `echo`...) will print some useful debugging information. The line `source /well/kir/config/modules.sh` makes the modules specific for KIR users available for subsequent loading. 
The line `module load Python/3.8.2-GCCcore-9.3.0` uses the module system to load a version of Python.
The line `sleep 60s` causes our script to pause for 60 seconds.
The final line uses Python to print the message ‘Hello, World!’

Now, for the sake of this example, we will move back to our home directory and submit the script file from there:

```
cd $HOME
sbatch sbatch_test/hello_world.sh
```

Because we told the scheduler to use the folder $HOME/sbatch_test as the working directory for this script, that is where it will put its log files (even though we submitted the script from our $HOME directory). Now let’s look at the log files:

```
cd sbatch_test
ls
```

We will now see that there are two separate files for output (.out) and error (.err) in the sbatch_test folder:

- hello_world.sh my-python-job-89346.out my-python-job-89346.err
{.grid-list}

Since this job ran successfully, the .err file will be empty, which is a reassuring sign! You can check that it’s empty, if you like, using the `cat` command. The output file will contain similar information to the one we saw in previous trials with hello_world.sh script.

### Organising complex job dependencies
 
When organising complex cluster workflows, it may become necessary to order jobs into stages and to require that later jobs commence only after earlier jobs have completed. 

To ensure that **jobB** will commence only after **jobA** has finished, you first submit **jobA** and make a note of its job ID number. Then you can submit **jobB** and specify that it should be held until **jobA** finishes and returns an exit code of 0 (that is, successful execution): 

```
sbatch -p short -d afterok:<jobA_id> jobB.sh 
```

If wishing to make such hold requests in a shell script, it may help to submit **jobA** using the `--parsable` option so that only its job id number is returned. You can then collect this id number in a shell variable and use it when submitting **jobB** like so:

```
JOBA_ID=$(sbatch --parsable -p short jobA.sh) 
sbatch -p short -d afterok:$JOBA_ID jobB.sh 
```

> Note that there are other possible state requirements than `afterok` and they can be put together with either separating commas for all the requirements to be met or question marks for any of them to be met. Only one separator type (comma or question mark) can be used. Please see the sbatch man page for more details by running `man sbatch`. 
{.is-info}

It is also possible to use an advanced form of job holding when you have sequential array jobs and you wish the tasks in the second job to start as soon as the corresponding task in the first job has completed. For example, if **jobA** is an array job with tasks numbered 1-100 and **jobB** is another array job also with tasks number 1-100 then one can arrange for **jobB**'s subtasks to run as soon as the corresponding task in **jobA** has completed by running:

```
JOBA_ID=$(sbatch --parsable -p short --array 1-100 jobA.sh) 
sbatch -p short --array 1-100 -d aftercorr:$JOBA_ID jobB.sh 
```

Using this method, **jobB**'s tasks will be allowed to run (subject to availability of resources on the cluster) as soon as the corresponding task in **jobA** has completed. 

> Since **jobA**'s tasks may have different run-time durations and so may complete in any order, **jobB**'s tasks may commence in any order.
{.is-info}

### Using a template script

Instead of writing your own job submission script from scratch, you can use a copy of our job submission template file located at `/apps/scripts/slurm.template.sh` which contains hints on a number of commonly used parameters. To use this file, begin by making a copy into your own working directory by running:

```
cp /apps/scripts/slurm.template.sh ~/work/myjobscript.sh
```

Then you can edit the file for your own purposes.

## Array jobs

If you have a set of jobs that perform the same action on many different inputs then you may be better submitting an array job. An array job:

- is made up of a number of tasks, with each task having a specific task id 
- has a single submission script that gets executed for each task in the array 
- has a single job id. 

The tasks get scheduled separately such that many tasks can be executing at the same time. This means tasks should not depend upon each other as there is no guarantee any one task will have completed before another starts.

The task id, along with other relevant information, is passed to the job through some environment variables. The task id is a number. It may be possible to use this number directly in your script or it may be necessary to use the task id to identify the specific inputs for the task.

There are a number of benefits to choosing to use array jobs rather than submitting lots of nearly identical jobs. As the entire array is just a single job, it is easier to keep track of and manage. Also, array jobs put much less load on the job scheduling system than the equivalent number of single jobs.

> Task id in array job is different to job id. Task id is a number assigned to jobs initiated by declaring an array job. Job id is a number assigned by the scheduler to the submitted job.   
{.is-warning}

<a href="#Example-decompressing-files">Example decompressing files</a>

### Declaring an array job

Array jobs are declared using the `--array` argument to sbatch in the form `--array n[-m[:s]]`, where:
- **n** is the first task id;
- **m** is the last task id;
- **s** is the task id step size (default is 1);

If only **n** is specified in `--array n`, only a single task with id **n** is launched. This may be useful for re-running a single step in an array job.

The task ids can be represented by a comma separated list, for example, `--array 0,6,16-32`

The task id range specified by, for example, 2-10:2 would result in the task id indexes 2, 4, 6, 8, and 10, for a total of 5 otherwise identical tasks. Using the example hello_world.sh script described in the **Batch jobs** section:

```bash
#!/bin/bash

echo "------------------------------------------------"
echo "Run on host: "`hostname`
echo "Operating system: "`uname -s`
echo "Username: "`whoami`
echo "Started at: "`date`
echo "------------------------------------------------"

sleep 60s
echo "Hello, World!"
```

We can run:

```
cd ~/sbatch_test
sbatch -p short --array 2-10:2 hello_world.sh
```

The output files written by the above command will conform to format **slurm-jobid_taskid.out**, somethihg like:

- slurm-1249270_2.out
slurm-1249270_4.out
slurm-1249270_6.out
slurm-1249270_8.out
slurm-1249270_10.out
{.grid-list}

> The following restrictions apply to the values **n** and **m**:
> 
> 1 <= **n** <= MIN(4000001, MaxArraySize)
> 1 <= **m** <= MIN(4000001, MaxArraySize)
> **n** <= **m**
> 
> where MaxArraySize is defined in the cluster configuration (4000001 at the time of writing). The total number of tasks in the array must be less than or equal to MIN(MaxArraySize, max_array_tasks). Where max_array_tasks is the number of simultaneously running tasks. Currently, max_array_tasks is set to 75001. If max_array_tasks is insufficient then please contact [KIR Research Computing Administrator](mailto:konstantin.borisenko@kennedy.ox.ac.uk) to ask for it to be raised.
{.is-info}

The maximum number of simultaneously running tasks from the job array can be specified with the `%` separator. For example, specifying `--array=1-100%2` would submit a 100-task array job where only 2 tasks can be executing at the same time. 

> The maximum two tasks allowed to run at the same time in the example above does not mean that tasks will necessarily run in pairs. They may still run one by one, depending on how busy is the cluster. 
{.is-info}

### Environment variables

To make the tasks dynamic, the scheduler will ensure that each task in the array job runs in an environment with different environment variables. Using these variables allows control of what is exactly done in each task, for example, which file is procesed. 

The scheduler sets the following task-related environment variables:

- SLURM_ARRAY_JOB_ID – job array's master job id number 
- SLURM_ARRAY_TASK_COUNT – total number of tasks in a job array 
- SLURM_ARRAY_TASK_ID – the task id of this task 
- SLURM_ARRAY_TASK_MIN – the task id of the first task in the array (parameter ‘n’ given to the ‘--array’ argument) 
- SLURM_ARRAY_TASK_MAX – the task id of the last task in the array (parameter ‘m’ given to the ‘--array’ argument) 
- SLURM_ARRAY_TASK_STEP – the size of the step in task id from one task to the next (parameter ‘s’ given to the ‘--array’ argument) 

### Simple example

```bash
#!/bin/bash

# This script sets up a task array with a step size of one.

#SBATCH -J TestSimpleArrayJob
#SBATCH -p short
#SBATCH --array 1-527:1
#SBATCH --requeue

echo `date`: Executing task ${SLURM_ARRAY_TASK_ID} of job ${SLURM_ARRAY_JOB_ID} on `hostname` as user ${USER} 
echo SLURM_ARRAY_TASK_MIN=${SLURM_ARRAY_TASK_MIN}, SLURM_ARRAY_TASK_MAX=${SLURM_ARRAY_TASK_MAX}, SLURM_ARRAY_TASK_STEP=${SLURM_ARRAY_TASK_STEP} 

##########################################################################################
#
# Do any one-off set up here
#
## For example, set up the environment for R/3.1.3-openblas-0.2.14-omp-gcc4.7.2:
## . /etc/profile.d/modules.sh
## module load R/3.1.3-openblas-0.2.14-omp-gcc4.7.2
## which Rscript
#
##########################################################################################

##########################################################################################
#
# Do your per-task processing here
#
## For example, run an R script that uses the task id directly:
## Rscript /path/to/my/rscript.R ${SLURM_ARRAY_TASK_ID}
## rv=$?
#
##########################################################################################

echo `date`: task complete
exit $rv
```

### Step size and batching

There is an appreciable dead time between one job or task finishing and the next starting - sometimes as much as 15s. This time is spent reporting the job/task’s exit status and resource usage, tidying up after the job/task, waiting for the next run of the scheduler to select the next job/task and preparing for that job/task to run. If the action performed by the script takes considerably more time than this, say, a couple of hours to run, this dead time is fairly unnoticable. 

> If the command that we want to execute takes very short time, say, one second to run, then running it once per job/task means that the dead time may be up to 15 times longer than the run time. In case of many tasks to run, it may take very much longer than expected to finish the job! 
{.is-warning}

The best approach for such short job/task run times is to batch multiple runs together.

This can be done by using an array job with a step size > 1 and a loop within the script that loops over all the task ids in the step. The step size should be chosen such that the combined run time for all the tasks in the step is long enough to make the dead time insignificant without putting the task at risk of being killed for exceeding the queue’s run time limit. It is also polite to not hog the execution slot, so 2-4 hours is a good target. With a little bit of arithmetic it is possible to write the script in such a way that all that needs adjusting is the step size and the script takes care of the rest. See **Example using step size** below for an example script.

### Example using step size

```bash
#!/bin/bash

# This script sets up a task array with one task per operation and uses the step size
# to control how many operations are performed per script run, e.g. to manage the
# turnover time of the tasks. This also makes it a bit easier to re-run a specific
# task than using a step size of one and an unrelated loop counter inside the script

#SBATCH -J TestArrayJobWithStep
#SBATCH -p short
#SBATCH --array 1-527:60
#SBATCH --requeue

echo `date`: Executing task ${SLURM_ARRAY_TASK_ID} of job ${SLURM_ARRAY_JOB_ID} on `hostname` as user ${USER} 
echo SLURM_ARRAY_TASK_MIN=${SLURM_ARRAY_TASK_MIN}, SLURM_ARRAY_TASK_MAX=${SLURM_ARRAY_TASK_MAX}, SLURM_ARRAY_TASK_STEP=${SLURM_ARRAY_TASK_STEP} 

##########################################################################################
#
# Do any one-off set up here
#
## For example, set up the environment for R/3.1.3-openblas-0.2.14-omp-gcc4.7.2:
## . /etc/profile.d/modules.sh
## module load R/3.1.3-openblas-0.2.14-omp-gcc4.7.2
## which Rscript
#
##########################################################################################

# Calculate the last task id for this step 
this_step_last=$(( SLURM_ARRAY_TASK_ID + SLURM_ARRAY_TASK_STEP - 1 )) 
if [ "${SLURM_ARRAY_TASK_MAX}" -lt "${this_step_last}" ] 
then 
    this_step_last="${SLURM_ARRAY_TASK_MAX}" 
fi 
 
# Loop over task ids in this step 
while [ "${SLURM_ARRAY_TASK_ID}" -le "${this_step_last}" ] 
do 
    echo `date`: starting work on SLURM_ARRAY_TASK_ID=`printenv SLURM_ARRAY_TASK_ID` 
 
##########################################################################################
#
#   Do your per-task processing here
#
##  For example, run an R script that uses the task id directly:
##  Rscript /path/to/my/rscript.R ${SLURM_ARRAY_TASK_ID}
##  rv=$?
#
##########################################################################################

    # Increment SLURM_ARRAY_TASK_ID 
    export SLURM_ARRAY_TASK_ID=$(( SLURM_ARRAY_TASK_ID + 1 )) 
done

echo `date`: task complete
exit $rv
```
### Mapping task-specific arguments from task ids 

The examples above just use the task id directly but this isn’t always possible. There are a number of ways that one might be able to map the task id to the task-specific arguments but if your requirements are complicated then you may have to write some code to do it. However, there are some simple options.

If you have a file that lists the task-specific arguments, with the arguments for each task (for example, a file name to process) on each line:

```
cat /path/to/my/argument/list | tail -${SLURM_ARRAY_TASK_ID} | head -1 | xargs /path/to/my/command
```

The individual arguments/lines from the list can also be accessed using bash array notation: 

```
ARG_LIST=($(</path/to/my/argument/list))
ARG=${ARG_LIST[${SLURM_ARRAY_TASK_ID}]}
```

An example where this might be useful includes processing a list of genes or compressing/decompressing a list of files.

<a id="Example-decompressing-files"></a>
#### Example decompressing files

Suppose we have a large number of compressed data files `*.gz`, which also may be symbolic links, in a ~/work/data directory. We want to quickly decompress them into a directory ~/work/data/decompressed utilising the power of parallel processing on the cluster. First, we create the destination directory:

```
cd ~/work/data
mkdir decompressed
```
We create a list of the `*.gz` files to process in a file in the current directory:

```
ls *.gz > files_to_process
```

The output of the following command gives the number of lines/files to process:

```
wc -l files_to_process
```

Say, we got `265` files. We use this number to set up an array job that decompresses all files in parallel in a submit.sh script:

```bash
#!/bin/bash

#SBATCH -J decompress_array
#SBATCH -p short
#SBATCH --array 1-265

inp=$(cat files_to_process | tail -${SLURM_ARRAY_TASK_ID} | head -1 )
out=${inp/".gz"/""}
gunzip -c ${inp} > decompressed/${out}

```
To submit the job we run:

```
sbatch submit.sh
```

## Useful SLURM commands

### Checking or deleting running jobs
A busy computing cluster handles many thousands of computing jobs every day. For this reason, when you submit a computing job to the cluster your job may not run immediately. Instead, it will be held in its queue until the scheduler decides to send it to a cluster node for execution. This is one important difference to what happens when you run a job on your own computer.

You can check the status of your job in the queue at any time using the 

```
squeue -u <your_username>
```
command, which will report the status of every job of yours which remains in the queue. 

The output of the command will look like this:
```
							JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
							83456     short 	script   <user>  R       1:12      1 compa002
```
The command reports some useful information such as job id, the time the job has been running for and the nodes the job is running on or the reason it is still pending. The ST (state) column shows the current state of the job. For example, **PD** means that the job is currently being held in the queue and waiting to start. A state of **R** means that the job is currently running.

Use 

```
squeue -j <jobid>
```

command to report the status of an individual job. 

To show detailed information about a job in the queue use:

```
scontrol show job <jobid>
```

If `jobid` is not specified then the command will show statistics for all jobs.
  
One important thing to note is that the `squeue` and `scontrol` commands report only jobs which are either waiting to run or currently running. Once a job has finished, squeue/scontrol will no longer report it. Instead, once a job has finished you can see a report on the job, including how many CPUs were allocated and its exit code by running:
```
sacct -j <jobid>
```
Occasionally, you may wish to delete a job before it starts or before it completes. For this you can use the command:
```
scancel <jobid>
```
### Getting information about partitions

Information about the SLURM partitions can be shown with the sinfo command:

```
sinfo
```
### Getting information about execution time, memory and CPU use

To get execution time of a job run

```
sacct -j <jobid> -o Elapsed 
```

The following command:

```
sacct -j <jobid> -o ReqMem,MaxRSS 
```

will print out the requested amount of memory (ReqMem) and the maximum amount of memory the job actually used (MaxRSS). 

To get information about CPU utilisation, you can run (if the job has completed in less than 24 hours):

```
sacct -j <jobid> -o ReqCPUS,ElapsedRaw,TRESUsageInMax%80 | tr ',=:' '  ' | awk 'NR>2 {print $1,(($4*3600)+($5*60)+$6)/$2 }'
```
This command will print out two numbers - first the number of requested CPUs and second the effective number of CPUs utilised during runtime. The effective number of utilised CPUs may be much lower than the number of requested CPUs (and requested parallel threads in the software) because of how the software is written and running. There may be stages in the software when it is not running in parallel or some of the processes are inactive, therefore resulting in lower effective CPU number. This may provide useful insight on how many CPUs (and threads) to request to run the software more effectively.     

Requesting too many CPUs (and software parallel threads) may slow down the progress of the job through the queues, especially when the cluster is busy. Reducing the number of requested CPUs (and correspondingly, number of threads) to closer reflect the effective CPU utilisation may slow down the job runtime, but it will definitely help in getting it much quicker through the queues, resulting in possibly faster and effective execution overall.

> For more general report on how effectively the job used the requested resorces please see the `Test resource utilisation` tab on the top of the page.
{.is-info}

## Test resource utilisation

### Checking how effectively the job used allocated resources

There are several scripts available on the cluster to test how a completed job has utilised its requested resources - memory and CPUs. To get access to the scripts, please run:

```
module load seff/2.1
```

To get information about memory and CPU utilisation for a job with job ID <job_id>, you can then run:

```
test_efficiency <job_id>
```

The output will look like this:

```
Requested CPUs: 16, utilised CPUS: 7.8467, CPU use efficiency: 49.00 %
Requested memory: 16  GB, utilised memory: 1.7 GB, memory use efficiency: 10.62 %
Billed for: 16 CPUs
```

This script is tailored to the billing system implemented on the BMRC cluster.

Alternatively, you can run: 

```
seff <job_id>
```

The information about resource utilisation can be used to optimise similar jobs. The aim is to increase memory and CPU use efficiency by requesting only resources that were effectively utilised in the job.

> The example above represents not very effective resource use. According to the information in the example, the requested CPUs for such a job can be reduced to 8 (with corresponding reduction in the parallel threads in the command) and the amount of requested memory can be reduced to 4 GB. This will speed up the job's progress through the queues - especially noticeable when the cluster is busy - and halve the amount of billed CPUs with a large chance of not affecting total execution time considerably.     
{.is-info}


The code of the test_efficiency script is shown below: 

```bash

#!/bin/bash
read -r BILL RCPUS RMEM ELAPSED CPUT1 UMEM1 CPUT2 UMEM2 <<< "$(sacct -j $1 -r short,long -n -o ReqTRES%60,ElapsedRaw,TRESUsageInMax%80 | tr '\n,=' ' ' | awk '{print $2,$4,$6,$9,$12,$18,$25,$31}')"
CPUT=$( echo "$CPUT1 $CPUT2" | tr ' ' '\n' | sort -r | head -1 )
UMEM=$( echo "$UMEM1 $UMEM2" | tr ' ' '\n' | sort -hr | head -1 )
# CPU utilisation and efficiency
if [[ $ELAPSED == 0 ]]
then
    ELAPSED=1
fi                                                                                           
if [[ $CPUT == *"-"* ]]
then
    T1=$(echo "$CPUT" | cut -d "-" -f 1 | awk '{ print $1 * 86400}')
    T2=$(echo "$CPUT" | cut -d "-" -f 2 | awk -F: '{ print ($1 * 3600) + ($2 * 60) + $3 }')
    UCPUS=$(echo "scale=4; ($T1+$T2)/$ELAPSED" | bc)
    CPUE=$(echo "scale=2; 100*$UCPUS/$RCPUS" | bc)
    echo "Requested CPUs: $RCPUS, utilised CPUS: $UCPUS, CPU use efficiency: $CPUE %"
else
    T1=$(echo "$CPUT" | awk -F: '{ print ($1 * 3600) + ($2 * 60) + $3 }')
    UCPUS=$(echo "scale=4; $T1/$ELAPSED" | bc)
    CPUE=$(echo "scale=2; 100*$UCPUS/$RCPUS" | bc)
    echo "Requested CPUs: $RCPUS, utilised CPUS: $UCPUS, CPU use efficiency: $CPUE %"
fi
# Memory utilisation and efficiency                                                                                                                                                             
if [[ $RMEM == *"K"* ]]
then
    RMEM=$(echo "$RMEM" | tr 'K' ' ')
    RMEM=$(echo "scale=1; $RMEM/1024/1024" | bc)
fi
if [[ $RMEM == *"M"* ]]
then
    RMEM=$(echo "$RMEM" | tr 'M' ' ')
    RMEM=$(echo "scale=1; $RMEM/1024" | bc)
fi
if [[ $RMEM == *"G"* ]]
then
    RMEM=$(echo "$RMEM" | tr 'G' ' ')
fi
if [[ $UMEM == *"K"* ]]
then
    UMEM=$(echo "$UMEM" | tr 'K' ' ')
    UMEM=$(echo "scale=1; $UMEM/1024/1024" | bc)
fi
if [[ $UMEM == *"M"* ]]
then
    UMEM=$(echo "$UMEM" | tr 'M' ' ')
    UMEM=$(echo "scale=1; $UMEM/1024" | bc)
fi
if [[ $UMEM == *"G"* ]]
then
    UMEM=$(echo "$UMEM" | tr 'G' ' ')
fi
MEME=$(echo "scale=2; 100*$UMEM/$RMEM" | bc)
echo "Requested memory: $RMEM GB, utilised memory: $UMEM GB, memory use efficiency: $MEME %"
echo "Billed for: $BILL CPUs"
```




