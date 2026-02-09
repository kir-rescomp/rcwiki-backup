---
title: Installing CGAT
description: Ways to install CGAT pipeline
published: true
date: 2024-08-02T14:08:37.686Z
tags: cgat
editor: markdown
dateCreated: 2021-10-04T08:58:25.780Z
---

# Installing CGAT on BMRC cluster

CGAT core provides a powerful and flexible framework for writing best-practise bioinformatics pipelines using Python3 and Ruffus. For more details please read the [publication](/https://doi.org/10.12688/f1000research.18674.2).

The code is maintained on GitHub here: https://github.com/cgat-developers/cgat-core

> Use of Python virtual environment is a recommended way to install CGAT on the BMRC cluster. 
{.is-info}

Alternatively, CGAT-core can be installed using conda. 

## Installing CGAT-core using a Python virtual environment

1. Set up and activate your Python virtual environment as described in [Python virtual environment](/python_venv) section. 

2. Update pip, setuptools and wheel: 

```
pip install --upgrade pip setuptools wheel
```

3. Install dependencies:

```
pip install apsw gevent numpy==1.24 pandas paramiko pep8 pytest pytest-pep8 drmaa pyyaml ruffus six sqlalchemy
```

4. Clone the repository:

First, change into an appropriate location, such as your development folder:

```
cd ~/devel
```
and then clone the repository:

```
git clone https://github.com/cgat-developers/cgat-core.git
```

5. Run setup:

```
cd cgat-core
python setup.py develop
```

6. Configure DRMAA and the queue:

To enable the pipelines to talk to the SLURM scheduler on the cluster via the drmaa library, you need to set and export the DRMAA_LIBRARY_PATH environment variable:

```
export SLURM_CONF=/run/slurm/conf/slurm.conf 
export DRMAA_LIBRARY_PATH=/usr/lib64/libdrmaa.so 

```
It is recommended to add these lines to your .bashrc and also include them in a job submission script that will execute a CGAT pipeline.

In order for the pipelines to be able to submit jobs you need to set the queue manager to `slurm` in a `.cgat.yml` configuration file in your home directory:

```
cluster:
    queue_manager: slurm
    queue: short
```

## Installing CGAT-apps

CGAT Apps is a collection of scripts to aid the analysis of high-throughput sequencing data within the CGAT pipeline.

To install CGAT Apps:

1. Activate your Python virtual environment. 

2. Install dependencies:

```
pip install cython pysam
```

3. Clone the repository:

```
cd ~/devel
git clone https://github.com/cgat-developers/cgat-apps.git
```

4. Load the compatible `SAMtools` module and run the setup:

`For gompi/foss-2020a/GCC/GCCcore-9.3.0 toolset:`

```
cd cgat-apps
module load SAMtools/1.10-GCC-9.3.0
python setup.py develop
```

`For gompi/foss-2022b/GCC/GCCcore-12.2.0 toolset:`

```
cd cgat-apps
module load SAMtools/1.17-GCC-12.2.0
python setup.py develop
```

## Installing CGAT-flow

GCAT Flow is a set of ruffus-based pipelines in comparative genomics and NGS analysis. 
To install CGAT Flow (after installing CGAT-core):

1. Activate your Python virtual environment. 

3. Clone the repository:

```
cd ~/devel
git clone https://github.com/cgat-developers/cgat-flow.git
```

4. Load the compatible `BEDtools` and `Kent_tools` modules and run the setup:

`For gompi/foss-2020a/GCC/GCCcore-9.3.0 toolset:`
```
cd cgat-flow
module load BEDTools/2.29.2-GCC-9.3.0
module load Kent_tools/422-foss-2020a
python setup.py develop
```

`For gompi/foss-2022b/GCC/GCCcore-12.2.0 toolset:`
```
cd cgat-flow
module load BEDTools/2.30.0-GCC-12.2.0
module load Kent_tools/450-GCC-12.2.0
python setup.py develop
```

