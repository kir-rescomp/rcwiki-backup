---
title: GPU resources
description: Using available GPU resources on the cluster
published: true
date: 2026-04-15T10:41:32.065Z
tags: gpu
editor: markdown
dateCreated: 2023-03-15T12:14:31.689Z
---

# GPU Resources on the BMRC Cluster

## Overview

The BMRC cluster provides GPU-accelerated compute nodes for machine learning, deep learning, and other GPU-intensive workloads. These nodes feature NVIDIA GPUs with varying specifications to suit different computational requirements.

Due to rapidly evolving hardware capabilities, our GPU nodes have considerable variation in CPU, RAM, and GPU configurations. This guide will help you understand the available resources and how to request them efficiently.

* For more  information on GPU and GPU profiling, refer to https://kir-rescomp.github.io/training-gpu-profiling/

---

## GPU Partitions

GPU resources are available through three Slurm partitions:

**Partition Table**

| Partition                  | NUM_GPU | GPU_MEMORY (GB) | Weight | Max Runtime (Hours) | CPUs (Default) | Memory (GB, Default) |
| -------------------------- | ------- | --------------- | ------ | ------------------- | -------------- | -------------------- |
| **Batch Partitions**       |         |                 |        |                     |                |                      |
| `gpu_a100_80gb`            | 24      | 80              | 1.00   | 60                  | 11             | 120                  |
| `gpu_rtx8000_48gb`         | 12      | 48              | 0.72   | 60                  | 7              | 185                  |
| `gpu_a100_40gb`            | 16      | 40              | 0.89   | 60                  | 7              | 90                   |
| `gpu_v100_32gb`            | 2       | 32              | 0.89   | 60                  | 7              | 750                  |
| `gpu_p100_16gb`            | 12      | 16              | 0.66   | 60                  | 5              | 90                   |
| `gpu_v100_16gb`            | 4       | 16              | 0.70   | 60                  | 11             | 60                   |
| `gpu_gh200_144gb`          | 40      | 144             | 2.12   | TBD                 | 72             | TBD                  |
| **Interactive Partitions** |         |                 |        |                     |                |                      |
| `gpu_interactive`                | 18      | 24              | 0.59   | 12                  | 7              | 80                   |

**Partition Selection**

- Use `gpu_inter` for interactive development, debugging, and testing (12-hour limit)
- Use a batch partition for non-interactive workloads — prefer partitions with sufficient GPU memory for your job rather than the largest available
- `gpu_gh200_144gb` is the highest-weight partition; runtime limits are still to be confirmed
- `gpu_v100_32gb` has a very high default memory allocation (750 GB) — only request what your job actually needs

{.is-info}

---

## Available GPU Hardware

### GPU Models Overview

BMRCluster includes five generations of NVIDIA GPUs as of 13.01.2026:

| GPU Model | Memory | Architecture | CUDA Compute | Best For |
|-----------|--------|--------------|--------------|----------|
| **A100** (80GB) | 80GB | Ampere | 8.0 | Large models, highest performance |
| **A100** (40GB) | 40GB | Ampere | 8.0 | Modern ML/DL workloads |
| **Quadro RTX 8000** | 48GB | Turing | 7.5 | Memory-intensive workloads |
| **Quadro RTX 6000** | 24GB | Turing | 7.5 | General ML/DL tasks |
| **V100** | 16-32GB | Volta | 7.0 | Legacy ML/DL (still compatible) |
| **P100** | 16GB | Pascal | 6.0 | ⚠️ Not compatible with PyTorch 2.0+ |

### GPU Distribution by Partition



```bash
# View GPUs in gpu_short partition
sinfo -p gpu_interactive -o "%N %G" -N
```

| GPU Type | GPU Memory | Nodes | GPUs/Node | Total GPUs |
|----------|------------|-------|-----------|------------|
| p100-sxm2-16gb | 16GB | compg009, compg010, compg011, compg013 | 4 | 16 |
| v100-pcie-32gb | 32GB | compg016 | 2 | 2 |
| v100-sxm2-16gb | 16GB | compg027 | 4 | 4 |
| quadro-rtx8000 | 48GB | compg028, compg029, compg030 | 4 | 12 |
| a100-pcie-40gb | 40GB | compg031, compg032 | 4 | 8 |
| a100-pcie-80gb | 80GB | compg035, compg036, compg039-042 | 4 | 24 |


### Detailed Node Specifications

<details>
<summary>Click to view full node specifications table</summary>

| Node | GPU Type | GPUs | GPU RAM/card | CPU cores/slot | RAM/slot | CPU Arch |
|------|----------|------|--------------|----------------|----------|----------|
| compg009 | p100-sxm2-16gb | 4 | 16GB | 6 | 91GB | Skylake |
| compg010 | p100-sxm2-16gb | 4 | 16GB | 6 | 91GB | Skylake |
| compg011 | p100-sxm2-16gb | 4 | 16GB | 6 | 91GB | Skylake |
| compg013 | p100-sxm2-16gb | 4 | 16GB | 6 | 91GB | Skylake |
| compg016 | v100-pcie-32gb | 2 | 32GB | 6 | 750GB | Skylake |
| compg019 | quadro-rtx6000 | 4 | 24GB | 10 | 91GB | Skylake |
| compg027 | v100-sxm2-16gb | 4 | 16GB | 12 | 60GB | Skylake |
| compg028 | quadro-rtx8000 | 4 | 48GB | 8 | 187GB | Skylake |
| compg029 | quadro-rtx8000 | 4 | 48GB | 8 | 187GB | Skylake |
| compg030 | quadro-rtx8000 | 4 | 48GB | 8 | 187GB | Skylake |
| compg031 | a100-pcie-40gb | 4 | 40GB | 8 | 91GB | Skylake |
| compg032 | a100-pcie-40gb | 4 | 40GB | 8 | 91GB | Skylake |
| compg033 | a100-pcie-40gb | 4 | 40GB | 8 | 91GB | Skylake |
| compg035 | a100-pcie-80gb | 4 | 80GB | 8 | 91GB | Skylake |
| compg036 | a100-pcie-80gb | 4 | 80GB | 8 | 91GB | Skylake |
| compg039 | a100-pcie-80gb | 4 | 80GB | 12 | 128GB | Skylake |
| compg040 | a100-pcie-80gb | 4 | 80GB | 12 | 128GB | Skylake |
| compg041 | a100-pcie-80gb | 4 | 80GB | 12 | 128GB | Skylake |
| compg042 | a100-pcie-80gb | 4 | 80GB | 12 | 128GB | Skylake |

</details>

---

## Submitting GPU Jobs

#### ⚠️ NOTE  : From 13.04.2026 on-wards, all GPU jobs will require us to specify the Slurm account `gpu_kir.prj` .i.e.

- If it is a `srun` session,

```bash
srun --account gpu_kir.prj....
```
or the short-hand `srun -A gpu_kir.prj` 

- If it is a `sbatch` script, 

```
#SBATCH --account gpu_kir.prj
```


### Basic GPU Request

The recommended methods for requesting GPUs are `--gres` or `--gpus-per-node`:

**Using --gres (Generic Resource Scheduling):**
```bash
sbatch --account gpu_kir.prj -p gpu_v100_16gb --gres gpu:N your_script.sh
```

**Using --gpus-per-node:**
```bash
sbatch --account gpu_kir.prj -p gpu_v100_16gb --gpus-per-node N your_script.sh
```

Where `N` is the number of GPUs required per node (maximum of 4 on most nodes).

**Example:**
```bash
sbatch --account gpu_kir.prj -p gpu_v100_16gb --gres gpu:1 train_model.sh
```

### Understanding Command Syntax

When checking GPU availability with `sinfo`:

```bash
sinfo --account gpu_kir.prj -p gpu_v100_16gb -o "%N %G" -N
```

- `sinfo` - Query Slurm partition and node information
- `-p gpu_v100_16gb` - Specify partition to query
- `-o "%N %G"` - Output format:
  - `%N` - Node name
  - `%G` - Generic resources (GRES), showing GPU specifications
- `-N` - Node-oriented format (one line per node)

### Requesting Specific GPU Types - Only needed for `gpu_interactive` 

You can request a particular GPU model using the full GRES specification:

```bash
sbatch -p  --gres gpu:a100-pcie-80gb:1 your_script.sh
```
`gpu_interactive` is the only partition with multiple GPU types, 
This requests 2 A100 80GB GPUs.

### Using GPU Constraints (Recommended)

Constraints allow you to specify acceptable GPU classes, giving the scheduler flexibility while meeting your requirements:

```bash
sbatch -p gpu_interactive --gpus-per-node 1 --constraint "a100|rtx8000" your_script.sh
```

**Available constraint features:**

- `p100` - P100 GPUs (16GB)
- `v100` - V100 GPUs (16-32GB)
- `rtx6000` - Quadro RTX 6000 (24GB)
- `rtx8000` - Quadro RTX 8000 (48GB)
- `a100` - A100 GPUs (40GB or 80GB)

**Example: Request modern GPUs only**
```bash
sbatch -p gpu_short --gpus-per-node 2 --constraint "rtx8000|a100" your_script.sh
```



---

## ⚠️ IMPORTANT: P100 GPU Compatibility Warning

### Problem: PyTorch 2.0+ and Modern ML Frameworks

> **P100 GPUs Not Compatible with Modern ML/DL Libraries**
> 
> **P100 GPUs MUST be excluded for any workflow using PyTorch 2.0+ or modern deep learning frameworks.**
{.is-danger}

**Why?**
- P100 GPUs have CUDA Compute Capability 6.0
- PyTorch 2.0+ requires CUDA Compute Capability 7.0 or higher
- Modern ML frameworks (TensorFlow 2.12+, JAX, etc.) have similar requirements
- Jobs will **fail** with cryptic CUDA errors if run on P100s

### How to Exclude P100 GPUs

**Method 1: Use constraints (Recommended)**
```bash
sbatch -p  --gpus-per-node 1 --constraint "v100|rtx6000|rtx8000|a100" your_script.sh
```

**Method 2: Request specific GPU types**
```bash
# Request A100 80GB GPUs
sbatch -p gpu_short --gres gpu:a100-pcie-80gb:1 your_script.sh

# Request any A100
sbatch -p gpu_short --gpus-per-node 1 --constraint "a100" your_script.sh

# Request RTX 8000
sbatch -p gpu_short --gres gpu:quadro-rtx8000:1 your_script.sh
```

### Recommended GPUs for ML/DL Workloads

For PyTorch, TensorFlow, JAX, and other modern deep learning frameworks:

| Priority | GPU Model | Memory | Use Case |
|----------|-----------|--------|----------|
| 🥇 Best | A100 (80GB) | 80GB | Large language models, massive datasets |
| 🥇 Best | A100 (40GB) | 40GB | General ML/DL, best performance |
| 🥈 Good | Quadro RTX 8000 | 48GB | Large models, memory-intensive |
| 🥈 Good | Quadro RTX 6000 | 24GB | Standard ML/DL workloads |
| 🥉 Compatible | V100 | 16-32GB | Older generation, still works |
| ❌ Avoid | P100 | 16GB | Will not work with PyTorch 2.0+ |

---

## Interactive GPU Sessions

### Using gpu_interactive Partition (Recommended)

For development, debugging, and interactive work:

```bash
srun -p gpu_interactive --gres gpu:1 --pty bash
```

- Time limit: 12 hours
- Available on: compg009, compg010 (P100 GPUs)
- Best for: Code development, testing, Jupyter notebooks

> **Interactive on Other Partitions**
> 
> You can also request interactive sessions on other partitions:
> ```bash
> srun -p gpu_short --gres gpu:a100-pcie-40gb:1 --pty bash
> ```
{.is-info}

---

## Example Job Scripts

### Basic PyTorch Training Job

```bash
#!/bin/bash

#SBATCH --account				gpu_kir.prj
#SBATCH --partition 		gpu_a100_80gb
#SBATCH --gpus-per-node 1
#SBATCH --mem 					64G
#SBATCH --cpus-per-task 8
#SBATCH --job-name 			my_training_job
#SBATCH --output			 logs/%j.out

# Load modules
module load Python/3.11.3-GCCcore-12.3.0

# Activate your environment
source ~/venvs/pytorch/bin/activate

# Run training script
python train_model.py --epochs 50 --batch-size 32
```

### Multi-GPU Training Job

```bash
#!/bin/bash

#SBATCH --account				gpu_kir.prj
#SBATCH --partition			gpu_a100_40gb
#SBATCH --gres 					gpu:4
#SBATCH --mem 					200G
#SBATCH --cpus-per-task 32
#SBATCH --job-name			multi_gpu_training

module load Python/3.11.3-GCCcore-12.3.0
source ~/venvs/pytorch/bin/activate

# Multi-GPU training with PyTorch DDP
torchrun --nproc_per_node=4 train_distributed.py
```

### Memory-Intensive Job

```bash
#!/bin/bash

#SBATCH --account				gpu_kir.prj
#SBATCH --partition 		gpu_rtx8000_48gb
#SBATCH --gpus-per-node	2
#SBATCH --mem-per-gpu 	150G
#SBATCH --cpus-per-task 16
#SBATCH --job-name		 	memory_intensive

module load Python/3.11.3-GCCcore-12.3.0
source ~/venvs/tensorflow/bin/activate

python train_large_model.py
```

---

## Best Practices

### 1. Choose the Right Partition
- Use `gpu_short` by default (4-hour limit, all nodes available)
- Only use `gpu_long` if you genuinely need >4 hours
- Use `gpu_interactive` for development and testing

### 2. Request Appropriate Resources
- Don't over-request GPUs, CPUs, or RAM
- Test with 1 GPU before scaling to multiple GPUs
- Use `--constraint` to allow scheduler flexibility

### 3. Exclude P100 for Modern ML/DL
- Always add `--constraint "v100|rtx6000|rtx8000|a100"` for PyTorch/TensorFlow jobs
- Or request specific GPU types: `--gres gpu:a100-pcie-40gb:1`

### 4. Monitor Your Jobs
- Check GPU utilization with `nvidia-smi` in interactive sessions
- Review job efficiency after completion with `seff <job_id>`
- Adjust resource requests based on actual usage

### 5. Plan for Node Heterogeneity
- Different nodes have different CPU/RAM allocations
- Check the detailed specifications table if you need specific resources
- Use constraints to ensure consistent hardware across array jobs

---

## Quick Reference

### Common Commands

```bash
# View available GPUs in a partition
sinfo -p gpu_v100_16gb -o "%N %G" -N

# Check GPU queue status
squeue -p gpu_v100_16gb

# Submit basic GPU job
sbatch --account gpu_kir.prj --partition gpu_v100_16gb --gres gpu:1 script.sh


# Interactive session
srun --account gpu_kir.prj --partition gpu_interactive --gres gpu:1 --pty bash

# Check GPU usage (when on a GPU node)
nvidia-smi
```

### GPU Type Quick Reference

```bash
# P100 GPUs (⚠️ avoid for PyTorch 2.0+)
--gres gpu:p100-sxm2-16gb:N

# V100 GPUs
--gres gpu:v100-pcie-32gb:N
--gres gpu:v100-sxm2-16gb:N

# RTX GPUs
--gres gpu:quadro-rtx6000:N
--gres gpu:quadro-rtx8000:N

# A100 GPUs
--gres gpu:a100-pcie-40gb:N
--gres gpu:a100-pcie-80gb:N
```

---

### Advanced Options

> **Contact KIR Research Computing Manager First**
> 
> The following options (`--gpus`, `--gpus-per-task`, `--gpus-per-socket`) are relevant for MPI workloads and can lead to blocking reservations. **Please contact KIR Research Computing Manager prior to using these options.**
{.is-warning}

---

## Resource Allocation

### CPU Cores

**Default allocation:** Each GPU slot comes with a default number of CPU cores (see table above).

**Modify CPU allocation:**
```bash
# Specify CPUs per GPU
sbatch -p gpu_v100_16gb --gres gpu:2 --cpus-per-gpu 4 your_script.sh

# Or specify total CPUs for the job
sbatch -p gpu_v100_16gb --gres gpu:2 -c 16 your_script.sh
```

### System Memory (RAM)

**Default allocation:** 60GB of system RAM per GPU slot.

**Total RAM available:** `RAM per slot × number of GPUs requested`

**Modify RAM allocation:**

```bash
# Specify RAM per GPU
sbatch -p gpu_v100_16gb --gres gpu:2 --mem-per-gpu 100G your_script.sh

# Or specify total RAM for the job
sbatch -p gpu_v100_16gb --gres gpu:2 --mem 200G your_script.sh
```

**Example:** Requesting 2 GPUs will give you 120GB RAM by default (60GB × 2).

> You can request up to the `RAM per slot` limit shown in the detailed node specifications table. For example, compg028 has 187GB per slot, so requesting 4 GPUs on that node could give you up to 748GB total RAM.
{.is-info}


## Getting Help

If you encounter issues or have questions:

- Check job output files for error messages
- Use `scontrol show job <job_id>` to see job details
- Contact KIR Research Computing Manager on kir-rc@kennedy.ox.ac.uk
- For MPI or advanced GPU scheduling, contact KIR Research Computing Manager first to discuss limits 


