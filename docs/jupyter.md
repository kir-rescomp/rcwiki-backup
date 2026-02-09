---
title: Jupyter Notebook and Lab
description: Running interactive Jupyter Notebook and Jupyter Lab sessions
published: true
date: 2025-10-20T11:29:44.323Z
tags: jupyter
editor: markdown
dateCreated: 2021-08-20T11:53:17.331Z
---

# Jupyter Notebook and Jupyter Lab

# Tabs {.tabset}
## gompi/foss-2022b/GCC/GCCcore-12.2.0

Jupyter is a popular Python-based software that allows you to edit and run Python code interactively over a web-browser. 

> Before attempting to run Jupyter Notebook or Jupyter Lab, please install your Python virtual environment. Also, you will need to have Jupyter Notebook and Lab software installed in the two Python virtual environments, one for Skylake and one for Ivybridge (as described in [Python virtual environment](/python_venv) section). Inside each virtual environment, install Jupyter Notebook using `pip install --force notebook`. If you intend to run Jupyter Lab, also install corresponding Python libaries with `pip install jupyterlab` command.
{.is-info}

### Starting up Jupyter Notebook server

1. While logged into cluster1 or cluster2, start an interactive cluster session with the required number of CPUs or amount of memory. For example, the command below requests 2 CPUs and up to 30 GB of memory:  
```
srun -p short -c 2 --pty bash 
```

2. Make a note of which node is running your interactive session by using the `hostname` command or checking your prompt. For example, it is `compe023`

3. Start Python virtual environment on the node:

```
module load Python/3.10.8-GCCcore-12.2.0
source ~/devel/venv/Python-3.10.8-GCCcore-12.2.0/${MODULE_CPU_TYPE}/bin/activate
``` 
4. Change into the folder where you store your notebooks (`~/notebooks`) and start Jupyter Notebook: 

```
cd ~/notebooks
jupyter notebook --no-browser --ip=*
```
After running this command, you will see several lines of text appear on screen. Note the port number the Jupyter is running on, for example, `8888`. Also you will need one of the last lines which begins with `http://127.0.0.1:` and includes a long token string.

### Starting up Jupyter Lab server

1. Follow the steps 1, 2 and 3 in the `Starting up Jupyter Notebook server` instructions above. 

2. Change into the folder where you store your notebooks (`~/notebooks`), load an appropriate nodejs module and start Jupyter Lab: 

```
cd ~/notebooks
module load nodejs/18.12.1-GCCcore-12.2.0
jupyter lab --no-browser --ip=*
```
After running the last command, you will see several lines of text appear on screen. Note the port number the Jupyter is running on, for example, `8888`. Also you will need one of the last lines which begins with `http://127.0.0.1:` and includes a long token string.

### Setting up tunneling to the Jupyter server

1. On your own computer (not cluster1 or cluster2), open a new terminal window and create an SSH tunnel following the pattern: 

```
ssh -L 8888:compe023:8888 username@cluster1.bmrc.ox.ac.uk
```

> Remember to use the correct port number in place of `8888` if Jupyter runs on a different port in Step 4 above - the second port number (after compe023), an appropriate hostname instead of `compe023` and `cluster1` (if you are connecting to cluster2) and your own username instead of `username`.
{.is-info}

After running the tunnel command your terminal will appear to be logged into cluster1 and (invisibly to you) an additional connection will now exists between your computer and your interactive session host. 

> It may happen that port 8888 on your own computer is already in use. If so, change the first port number (before `compe023`) to e.g. 9999. Make sure that the second port number (after `compe023`) matches what you saw in Step 4 when starting the Jupyter server.
{.is-warning}

2. Copy the line from your Jupyter Notebook or Jupyter Lab server that begins with `http://127.0.0.1:` including the long token string. 
3. Open a web browser on your own computer and paste the copied line into your web browser. Jupyter Notebook or Jupyter Lab will appear.

> If you have changed your local port number when creating the SSH tunnel, you will also need to change the port number in the url before connecting to it in the web browser.
{.is-warning}

> When running Jupyter Lab session on the cluster, it is important not to select any kernel that you have prepared for Jupyter Lab session in RStudio server, like, for example, a kernel called Python-3.8.2. For Jupyter Lab sessions on the cluster, always choose the `Python 3 (ipykernel)` kernel.
{.is-warning}


## gompi/foss-2020a/GCC/GCCcore-9.3.0

Jupyter is a popular Python-based software that allows you to edit and run Python code interactively over a web-browser. 

> Before attempting to run Jupyter Notebook or Jupyter Lab, please install your Python virtual environment. Also, you will need to have Jupyter Notebook and Lab software installed in the two Python virtual environments, one for Skylake and one for Ivybridge (as described in [Python virtual environment](/python_venv) section). Inside each virtual environment, install Jupyter Notebook using `pip install --force notebook`. If you intend to run Jupyter Lab, also install corresponding Python libaries with `pip install jupyterlab` command.
{.is-info}

### Starting up Jupyter Notebook server

1. While logged into cluster1 or cluster2, start an interactive cluster session with the required number of CPUs or amount of memory. For example, the command below requests 2 CPUs and up to 30 GB of memory:  
```
srun -p short -c 2 --pty bash 
```

2. Make a note of which node is running your interactive session by using the `hostname` command or checking your prompt. For example, it is `compe023`

3. Start Python virtual environment on the node:

```
module load Python/3.8.2-GCCcore-9.3.0
source ~/devel/venv/Python-3.8.2-GCCcore-9.3.0/${MODULE_CPU_TYPE}/bin/activate
``` 
4. Change into the folder where you store your notebooks (`~/notebooks`) and start Jupyter Notebook: 

```
cd ~/notebooks
jupyter notebook --no-browser --ip=*
```
After running this command, you will see several lines of text appear on screen. Note the port number the Jupyter is running on, for example, `8888`. Also you will need one of the last lines which begins with `http://127.0.0.1:` and includes a long token string.

### Starting up Jupyter Lab server

1. Follow the steps 1, 2 and 3 in the `Starting up Jupyter Notebook server` instructions above. 

2. Change into the folder where you store your notebooks (`~/notebooks`), load an appropriate nodejs module and start Jupyter Lab: 

```
cd ~/notebooks
module load nodejs/12.16.1-GCCcore-9.3.0
jupyter lab --no-browser --ip=*
```
After running the last command, you will see several lines of text appear on screen. Note the port number the Jupyter is running on, for example, `8888`. Also you will need one of the last lines which begins with `http://127.0.0.1:` and includes a long token string.

### Setting up tunneling to the Jupyter server

1. On your own computer (not cluster1 or cluster2), open a new terminal window and create an SSH tunnel following the pattern: 

```
ssh -L 8888:compe023:8888 username@cluster1.bmrc.ox.ac.uk
```

> Remember to use the correct port number in place of `8888` if Jupyter runs on a different port in Step 4 above - the second port number (after compe023), an appropriate hostname instead of `compe023` and `cluster1` (if you are connecting to cluster2) and your own username instead of `username`.
{.is-info}

After running the tunnel command your terminal will appear to be logged into cluster1 and (invisibly to you) an additional connection will now exists between your computer and your interactive session host. 

> It may happen that port 8888 on your own computer is already in use. If so, change the first port number (before `compe023`) to e.g. 9999. Make sure that the second port number (after `compe023`) matches what you saw in Step 4 when starting the Jupyter server.
{.is-warning}

2. Copy the line from your Jupyter Notebook or Jupyter Lab server that begins with `http://127.0.0.1:` including the long token string. 
3. Open a web browser on your own computer and paste the copied line into your web browser. Jupyter Notebook or Jupyter Lab will appear.

> If you have changed your local port number when creating the SSH tunnel, you will also need to change the port number in the url before connecting to it in the web browser.
{.is-warning}

> When running Jupyter Lab session on the cluster, it is important not to select any kernel that you have prepared for Jupyter Lab session in RStudio server, like, for example, a kernel called Python-3.8.2. For Jupyter Lab sessions on the cluster, always choose the `Python 3 (ipykernel)` kernel.
{.is-warning}


## How do I run my Python Notebook through Slurm?

The first thing you will need to do is to convert your `.ipynb` (Interactive PYthon Note Book) file into a regular `.py` python file. There are two ways to do this.

#### nbconvert

nbconvert is a tool used to convert notebooks to other formats, it is accessible through the command line if you are logged in through Jupyter.

```py
jupyter nbconvert --to script my_notebook.ipynb
```
will create a new python script called **my_notebook.py**.

#### Export Notebook

With your notebook open, select <kbd>File</kbd> -> <kbd>Save</kbd> and <kbd>Export Notebook As...</kbd> -> <kbd>Executable Script</kbd>

This option might be less convenient as the exporter saves the python file to your local computer, meaning you will have to drag it back into the file explorer in Jupyter from your downloads folder.

This script can then be run as a regular python script.