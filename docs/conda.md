---
title: Conda
description: Working with Conda
published: true
date: 2026-01-30T21:47:11.834Z
tags: conda, anaconda, miniconda
editor: markdown
dateCreated: 2021-09-06T15:49:05.150Z
---


# Conda with Miniforge3 

# Tabs {.tabset}
## gompi/foss-2022b/GCC/GCCcore-12.2.0

> It is recommended where possible to use Python virtual environments in preference to conda. This is because Python virtual environments tend to include only the minimum of what is required whereas conda can also install non-python software that may cause incompatibilities with other software on the cluster.
Also, we **do not recommend** using Anaconda modules as of mid-2025 due to licensing complications. 
{.is-warning}

Those wishing to use conda on the BMRC cluster should load one of the Miniforge3 modules. You can see which versions are available by running:

```
module avail Miniforge3
```

### Conda configuration

> By default, conda will store your environments and downloaded packages in your home directory under `~/.conda` - this will quickly cause your home directory to run out of space. To prevent this from happening, configure conda to use your file directory instead.
{.is-info}

1. Log into any of the login nodes.

2. Create a dedicated conda folder in your `~/devel` folder with subdirectories for packages and environments. 

```
mkdir ~/devel/conda
```

3. Using your favourite text editor, create the file `~/.condarc` in your home directory containing the following:

```
channels:
  - conda-forge
  - bioconda
 
pkgs_dirs:
  - ~/devel/conda/${MODULE_CPU_TYPE}/pkgs
envs_dirs:
  - ~/devel/conda/${MODULE_CPU_TYPE}/envs
```

### Skylake

To maintain continuity with previous setup of the cluster, this virtual environment will be placed in `skylake` subdirectory. 

1. Initialise base conda environment, using the `Anaconda3/2023.07-2` module as an example:

```
module load Miniforge3/24.1.2-0
source $(conda info --base)/etc/profile.d/conda.sh
```

2. Create and activate a new local environment, for example, `my-env`:

```
conda create --name my-env
conda activate my-env
```

3. Packages can be then installed into the active local environment, as required. The example, command below installs the `scipy` package into the active environment. 

```
conda install scipy
```

4. To deactivate first local and then the base environments run the following command twice, when you have finished working with the conda environment:

```
conda deactivate
```

### Using Conda environment

Initialise the base environmnet and then activate the required local conda environment after starting an interactive `srun` session or in a `sbatch` script:

```
module load Miniforge3/24.1.2-0
source $(conda info --base)/etc/profile.d/conda.sh
conda activate my-env
```

## gompi/foss-2020a/GCC/GCCcore-9.3.0

> It is recommended where possible to use Python virtual environments in preference to conda. This is because Python virtual environments tend to include only the minimum of what is required whereas conda can also install non-python software that may cause incompatibilities with other software on the cluster.
{.is-warning}

Those wishing to use conda on the BMRC cluster should load one of the Anaconda modules. You can see which versions are available by running:

```
module avail Miniforge3/24.1.2-0
```

### Conda configuration

> By default, conda will store your environments and downloaded packages in your home directory under `~/.conda` - this will quickly cause your home directory to run out of space. To prevent this from happening, configure conda to use your file directory instead.
{.is-info}

1. Log into any of the login nodes.

2. Create a dedicated conda folder in your `~/devel` folder with subdirectories for packages and environments. 

```
mkdir ~/devel/conda
```

3. Using your favourite text editor, create the file `~/.condarc` in your home directory containing the following:

```
channels:
  - conda-forge
  - bioconda
 
pkgs_dirs:
  - ~/devel/conda/${MODULE_CPU_TYPE}/pkgs
envs_dirs:
  - ~/devel/conda/${MODULE_CPU_TYPE}/envs
```

### Skylake

To maintain continuity with previous setup of the cluster, this virtual environment will be placed in `skylake` subdirectory. 

1. Initialise base conda environment, using the `Miniforge3/24.1.2-0` module as an example:

```
module load Miniforge3/24.1.2-0
eval "$(conda shell.bash hook)"
```

2. Create and activate a new local environment, for example, `my-env`:

```
conda create --name my-env
conda activate my-env
```

3. Packages can be then installed into the active local environment, as required. The example, command below installs the `scipy` package into the active environment. 

```
conda install scipy
```

4. To deactivate first local and then the base environments run the following command twice, when you have finished working with the conda environment:

```
conda deactivate
```

### Using Conda environment

Initialise the base environmnet and then activate the required local conda environment after starting an interactive `srun` session or in a `sbatch` script:

```
module load Miniforge3/24.1.2-0
eval "$(conda shell.bash hook)"
conda activate my-env
```
