---
title: RStudio server
description: Graphical RStudio server
published: true
date: 2024-04-22T15:03:34.168Z
tags: rstudio
editor: markdown
dateCreated: 2021-10-19T15:01:45.249Z
---

# Professional RStudio Workbench

The Kennedy Institute has a dedicated RStudio Workbench server, which supports R and Jupyter Lab/Notebook sessions. 

Before starting using the RStudio server, please follow instruction on setting up the [R environment](/using_r), which includes instruction on setting up ~/.Rprofile.

To be able to use Jupyter Lab/Notebook sessions, please install a suitable [Python virtual environment](/python_venv) and corresponding [Jupyter libraries](/jupyter) before attempting to run them. 

The server is accessible at: https://rstudio-kir.bmrc.ox.ac.uk through Chrome or Firefox browser. Do not use Safari browser to access the server, as it has been identified to have problems with connection.

> To log in to the server, enter your BMRC user name and then your BMRC password immediately followed by 6-digit second authentication factor in the same password field.  
{.is-info}

> Please remember that RStudio server has a limited capacity (CPUs and memory). It should be used primarily for lightweight calculations, visualising results and code development. All heavy calculations should be run on the cluster.  
{.is-warning}

# Jupyter Lab in RStudio Workbench

Once you have installed your [Python virtual environment](/python_venv), any required Python libraries and [Jupyter libraries](/jupyter), you will need to set up a Jupyter kernel, which will tell the RStudio which Python virtual environment and any other additional software modules to use within the Jupyter Lab session. 

# Tabs {.tabset}
## gompi/foss-2022b/GCC/GCCcore-12.2.0

### Set up Jupyter Kernel

To set up a Jupyter kernel:

1. Log into the RStudio server at https://rstudio-kir.bmrc.ox.ac.uk and start an R session.

2. In the session, open terminal window by clicking on Terminal tab. 

3. Create a Jupyter kernel to load your Python virtual environment and any other additional software modules by running a command in the terminal in the form `/apps/local/bin/create-jupyter-kernel.sh -m module -e location -n name`. Here, `module` is the Python software module to use in the kernel which corresponds to the software module used to set up your Pyhton virtual environment. 

> Repeat `-m module` for each additional software module you wish to load for your Jupyter Lab session 
{.is-info}

`location` is the path to your Python virtual environment, including the CPU architecture directory, as used in [Python virtual environment](/python_venv) and `name` is a name you wish to give to the kernel (do not use too long names, as they will appear cut in the Jupyter Lab).

For example, with the modules and locations used for setting up [Python virtual environment](/python_venv) as described on the corresponding pages, the command will be:

```
/apps/local/bin/create-jupyter-kernel.sh -m Python/3.10.8-GCCcore-12.2.0 -e ~/devel/venv/Python-3.10.8-GCCcore-12.2.0/skylake -n Python-3.10.8
```

When loading an additional module for your Jupyter Lab session, for example, a Biopython module, the command would be:

```
/apps/local/bin/create-jupyter-kernel.sh -m Python/3.10.8-GCCcore-12.2.0 -m Biopython/1.81-foss-2022b -e ~/devel/venv/Python-3.10.8-GCCcore-12.2.0/skylake -n Biopython-3.10.8
```

> Kernels only need to be set up once. New Jupyter Lab sessions can be launched using existing (previously created) kernels. 
{.is-info}

Now you are ready to start a Jupyter Lab/Notebook session in RStudio. 

### Start a Jupyter Lab session

Once the required kernel is set up as described above, the Jupyter Lab/Notebook session can be started as follows. 

1. In the RStudio, create a new session, change the session Editor option to JupyterLab and click Open session. Once Jupyter Lab session starts, the list of installed kernels will be shown on the welcome page and new sessions can be created by double clicking your desired kernel. 

> Once your Jupyter Notebook page appears, the icon in the top right will initially display a lighting bolt (to indicate that it is trying to connect) and after a few moments it will change into a circle. Hovering over the icon will show that the kernel is running. 
{.is-info}

2. If required, you can switch kernels by selecting `Kernel->Change Kernel` from the menus from within a running Jupyter Notebook in the top right corner.

> It is important not to select the `Python 3 (ipykernel)` that comes with RStudio. This kernel is local to RStudio server and it will not have access to neither any packages installed in your Python virtual environment on the cluster nor additional software modules.  
{.is-warning}

## gompi/foss-2020a/GCC/GCCcore-9.3.0
### Set up Jupyter Kernel

To set up a Jupyter kernel:

1. Log into the RStudio server at https://rstudio-kir.bmrc.ox.ac.uk and start an R session.

2. In the session, open terminal window by clicking on Terminal tab. 

3. Create a Jupyter kernel to load your Python virtual environment and any other additional software modules by running a command in the terminal in the form `/apps/local/bin/create-jupyter-kernel.sh -m module -e location -n name`. Here, `module` is the Python software module to use in the kernel which corresponds to the software module used to set up your Pyhton virtual environment. 

> Repeat `-m module` for each additional software module you wish to load for your Jupyter Lab session 
{.is-info}

`location` is the path to your Python virtual environment, including the CPU architecture directory, as used in [Python virtual environment](/python_venv) and `name` is a name you wish to give to the kernel (do not use too long names, as they will appear cut in the Jupyter Lab).

For example, with the modules and locations used for setting up [Python virtual environment](/python_venv) as described on the corresponding pages, the command will be:

```
/apps/local/bin/create-jupyter-kernel.sh -m Python/3.8.2-GCCcore-9.3.0 -e ~/devel/venv/Python-3.8.2-GCCcore-9.3.0/skylake -n Python-3.8.2
```

When loading an additional module for your Jupyter Lab session, for example, a Biopython module, the command would be:

```
/apps/local/bin/create-jupyter-kernel.sh -m Python/3.8.2-GCCcore-9.3.0 -m Biopython/1.76-foss-2020a-Python-3.8.2 -e ~/devel/venv/Python-3.8.2-GCCcore-9.3.0/skylake -n Biopython-3.8.2
```

> Kernels only need to be set up once. New Jupyter Lab sessions can be launched using existing (previously created) kernels. 
{.is-info}

Now you are ready to start a Jupyter Lab/Notebook session in RStudio. 

### Start a Jupyter Lab session

Once the required kernel is set up as described above, the Jupyter Lab/Notebook session can be started as follows. 

1. In the RStudio, create a new session, change the session Editor option to JupyterLab and click Open session. Once Jupyter Lab session starts, the list of installed kernels will be shown on the welcome page and new sessions can be created by double clicking your desired kernel. 

> Once your Jupyter Notebook page appears, the icon in the top right will initially display a lighting bolt (to indicate that it is trying to connect) and after a few moments it will change into a circle. Hovering over the icon will show that the kernel is running. 
{.is-info}

2. If required, you can switch kernels by selecting `Kernel->Change Kernel` from the menus from within a running Jupyter Notebook in the top right corner.

> It is important not to select the `Python 3 (ipykernel)` that comes with RStudio. This kernel is local to RStudio server and it will not have access to neither any packages installed in your Python virtual environment on the cluster nor additional software modules.  
{.is-warning}

# Free RStudio version

Also, you can use a free RStudio version available on BMRC cluster. 

> An advantage of running RStudio in this way is that you can request required resources from the cluster and not be limited by the capacity of the RStudio Workbench server - you can run as heavy calculation as you want within RStudio. The disadvantage is that it has limited functionality, such as it does not support Jupyter sessions. 
{.is-info}

As for the RStudio Workbench, it is important to first set up the [R environment](/using_r) and ~/.Rprofile. 

# Tabs {.tabset}

## gompi/foss-2022b/GCC/GCCcore-12.2.0

After setting up your ~/.Rprofile, follow the process below to setup an RStudio session:

1. First, login to either cluster1 or cluster2 and then begin an interactive session on the cluster, requesting an appropriate amount of resources for your intended calculations. For example, 3 CPU slots with a total of 45 GB of memory:

```
srun -p short -c 3 --pty bash
```

2. From within your interactive session, load a suitable version of RStudio, for example:

```
module load RStudio-Server/2023.09.0+463-foss-2022b-Java-11-R-4.3.1-bare
```

3. Start your RStudio service by running:

```
/apps/misc/R/bmrc-r-user-tools/rstudio/rserver.sh
```

The script above will start RStudio on a suitable free port and provide instructions for how to connect to and log into the RStudio from your own computer.

4. On your own computer, open a new terminal window and create an ssh tunnel to the RStudio server by running the `ssh` command suggested in the instructions.

5. In your browser, navigate to the address shown in the instructions and you should see the RStudio login screen.

> Login is required to access RStudio sessions. Please use your BMRC credentials and follow the instructions on how to log in into the session. 
{.is-info}

## gompi/foss-2020a/GCC/GCCcore-9.3.0

After setting up your ~/.Rprofile, follow the process below to setup an RStudio session:

1. First, login to either cluster1 or cluster2 and then begin an interactive session on the cluster, requesting an appropriate amount of resources for your intended calculations. For example, 3 CPU slots with a total of 45 GB of memory:

```
srun -p short -c 3 --pty bash
```

2. From within your interactive session, load a suitable version of RStudio, for example:

```
module load RStudio-Server/1.4.1717-foss-2020a-Java-11-R-4.1.2-bare
```

3. Start your RStudio service by running:

```
/apps/misc/R/bmrc-r-user-tools/rstudio/rserver.sh
```

The script above will start RStudio on a suitable free port and provide instructions for how to connect to and log into the RStudio from your own computer.

4. On your own computer, open a new terminal window and create an ssh tunnel to the RStudio server by running the `ssh` command suggested in the instructions.

5. In your browser, navigate to the address shown in the instructions and you should see the RStudio login screen.

> Login is required to access RStudio sessions. Please use your BMRC credentials and follow the instructions on how to log in into the session. 
{.is-info}

