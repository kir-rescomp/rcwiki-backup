---
title: Python virtual environment
description: Working with Python virtual environment
published: true
date: 2024-10-08T10:58:33.359Z
tags: python, virtual environment
editor: markdown
dateCreated: 2021-08-17T14:35:19.159Z
---

# Python on the BMRC cluster

# Tabs {.tabset}
## gompi/foss-2022b/GCC/GCCcore-12.2.0
### Working with software modules

There are a number of Python packages already centrally installed on the cluster, which can be loaded using corresponding `module load` command for use in your Python scripts. To list all Python packages available centrally for Python 3.10.8

```
module avail 2>&1 | grep -i python-3.10.8
```

New packages can be installed on demand which is a preferred way to get a new Python package.  

In cases where you may need full control of software packages, installing your own packages via Python virtual environment is the best alternative way.

### Setting up

> The BMRC cluster comprises compute nodes with uniform Skylake (or Skylake-compatible) generations of CPU architecture. Software built for Skylake will run on all compute nodes on the cluster.
{.is-info}

#### Skylake

To maintain continuity with previous setup of the cluster, we will call this Python virtual environment `skylake`.

1. First, login to any of the login nodes on the cluster. Load a suitable version of Python, e.g. Python/3.10.8-GCCcore-12.2.0 

```
module load Python/3.10.8-GCCcore-12.2.0
```

2. To create the virtual environment, run the folowing commands.

```
mkdir -p ~/devel/venv/Python-3.10.8-GCCcore-12.2.0
cd ~/devel/venv/Python-3.10.8-GCCcore-12.2.0
python -m venv skylake
```

This will create a new python virtual environment in the `skylake` sub-folder of `Python-3.10.8-GCCcore-12.2.0`. 

> If you are working with Python 2 module, like `Python/2.7.18-GCCcore-12.2.0-bare`, the command to create virtual environment is, for example, `python -m virtualenv skylake`
{.is-info}

3. Once this is created, activate it before using it by running: 
```
source ~/devel/venv/Python-3.10.8-GCCcore-12.2.0/skylake/bin/activate
```
Notice that your shell prompt changes to reflect virtual environment. 

4. Once the virtual environment is activated, it is a good idea to upgrade the pip package manager, setuptools and wheel:

```
pip install --upgrade pip setuptools wheel
```

5. After that, you can proceed to install software e.g. by using `pip` and `pip install` commands.  Install all packages that you need.

6. Run: 
```
deactivate  
```
to deactivate your skylake environment when you have finished using it.

### Working in virtual environment

When submitting jobs to the queue or running them interactively, you can continue using the `${MODULE_CPU_TYPE}` environment variable to select the correct virtual environment that corresponds to the CPU architecture of the node. This is done to ensure that previous scripts that you have prepared still work without need to modify them. In the interactive mode, when logged into the compute node, it can be done by the following commands:

```
module load Python/3.10.8-GCCcore-12.2.0
source ~/devel/venv/Python-3.10.8-GCCcore-12.2.0/${MODULE_CPU_TYPE}/bin/activate
```
The environment variable MODULE_CPU_TYPE will evaluate to skylake as appropriate.

The following lines can be also added to your job submissions scripts:

```bash
#!/bin/bash

source /well/kir/config/modules.sh
module load Python/3.10.8-GCCcore-12.2.0
source ~/devel/venv/Python-3.10.8-GCCcore-12.2.0/${MODULE_CPU_TYPE}/bin/activate

# Add the commands that need to be executed

```

## gompi/foss-2020a/GCC/GCCcore-9.3.0
### Working with software modules

There are a number of Python packages already centrally installed on the cluster, which can be loaded using corresponding `module load` command for use in your Python scripts. To list all Python packages available centrally for Python 3.8.2

```
module avail 2>&1 | grep -i python-3.8.2
```

New packages can be installed on demand which is a preferred way to get a new Python package.  

In cases where you may need full control of software packages, installing your own packages via Python virtual environment is the best alternative way.

### Setting up

> The BMRC cluster comprises compute nodes with uniform Skylake (or Skylake-compatible) generations of CPU architecture. Software built for Skylake will run on all compute nodes on the cluster.
{.is-info}

#### Skylake

To maintain continuity with previous setup of the cluster, we will call this Python virtual environment `skylake`. 

1. First, login to any of the login nodes on the cluster. Load a suitable version of Python, e.g.  Python/3.8.2-GCCcore-9.3.0 

```
module load Python/3.8.2-GCCcore-9.3.0
```

2. To create the virtual environment, run the folowing commands.

```
mkdir -p ~/devel/venv/Python-3.8.2-GCCcore-9.3.0
cd ~/devel/venv/Python-3.8.2-GCCcore-9.3.0
python -m venv skylake
```

This will create a new python virtual environment in the `skylake` sub-folder of `Python-3.8.2-GCCcore-9.3.0`. 

> If you are working with Python 2 module, like `Python/2.7.18-GCCcore-9.3.0`, the command to create virtual environment is, for example, `python -m virtualenv skylake`
{.is-info}

3. Once this is created, activate it before using it by running: 
```
source ~/devel/venv/Python-3.8.2-GCCcore-9.3.0/skylake/bin/activate
```
Notice that your shell prompt changes to reflect virtual environment. 

4. Once the virtual environment is activated, it is a good idea to upgrade the pip package manager, setuptools and wheel:

```
pip install --upgrade pip setuptools wheel
```

5. After that, you can proceed to install software e.g. by using `pip` and `pip install` commands.  Install all packages that you need.

6. Run: 
```
deactivate  
```
to deactivate your skylake environment when you have finished using it.

### Working in virtual environment

When submitting jobs to the queue or running them interactively, you can continue using the `${MODULE_CPU_TYPE}` environment variable to select the correct virtual environment that corresponds to the CPU architecture of the node. This is done to ensure that previous scripts that you have prepared still work without need to modify them. In the interactive mode, when logged into the compute node, it can be done by the following commands:

```
module load Python/3.8.2-GCCcore-9.3.0
source ~/devel/venv/Python-3.8.2-GCCcore-9.3.0/${MODULE_CPU_TYPE}/bin/activate
```
The environment variable MODULE_CPU_TYPE will evaluate to skylake as appropriate.

The following lines can be also added to your job submissions scripts:

```bash
#!/bin/bash

source /well/kir/config/modules.sh
module load Python/3.8.2-GCCcore-9.3.0
source ~/devel/venv/Python-3.8.2-GCCcore-9.3.0/${MODULE_CPU_TYPE}/bin/activate

# Add the commands that need to be executed

```

 


