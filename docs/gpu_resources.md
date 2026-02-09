---
title: GPU resources
description: Using available GPU resources on the cluster
published: true
date: 2026-01-13T10:29:30.479Z
tags: gpu
editor: markdown
dateCreated: 2023-03-15T12:14:31.689Z
---

# GPU Resources on the BMRC Cluster

## Overview

The BMRC cluster provides GPU-accelerated compute nodes for machine learning, deep learning, and other GPU-intensive workloads. These nodes feature NVIDIA GPUs with varying specifications to suit different computational requirements.

Due to rapidly evolving hardware capabilities, our GPU nodes have considerable variation in CPU, RAM, and GPU configurations. This guide will help you understand the available resources and how to request them efficiently.

---

## GPU Partitions

GPU resources are available through three Slurm partitions:

| Partition | Purpose | Time Limit | Nodes Available |
|-----------|---------|------------|-----------------|
| `gpu_interactive` | Interactive development and testing | 12 hours | 2 nodes (compg009, compg010) with P100 GPUs |
| `gpu_short` | General batch jobs, short runs | 4 hours | All GPU nodes |
| `gpu_long` | Long-running batch jobs | 60 hours | Subset of GPU nodes |

> **Partition Selection**
> - Use `gpu_interactive` for code development, debugging, and interactive work
> - Use `gpu_short` whenever possible for batch jobs (it has access to all nodes)
> - Use `gpu_long` only for jobs that genuinely need more than 4 hours (limited node availability)
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

#### gpu_short Partition

```bash
# View GPUs in gpu_short partition
sinfo -p gpu_short -o "%N %G" -N
```

| GPU Type | GPU Memory | Nodes | GPUs/Node | Total GPUs |
|----------|------------|-------|-----------|------------|
| p100-sxm2-16gb | 16GB | compg009, compg010, compg011, compg013 | 4 | 16 |
| v100-pcie-32gb | 32GB | compg016 | 2 | 2 |
| v100-sxm2-16gb | 16GB | compg027 | 4 | 4 |
| quadro-rtx8000 | 48GB | compg028, compg029, compg030 | 4 | 12 |
| a100-pcie-40gb | 40GB | compg031, compg032 | 4 | 8 |
| a100-pcie-80gb | 80GB | compg035, compg036, compg039-042 | 4 | 24 |

#### gpu_long Partition

```bash
# View GPUs in gpu_long partition
sinfo -p gpu_long -o "%N %G" -N
```

| GPU Type | GPU Memory | Nodes | GPUs/Node | Total GPUs |
|----------|------------|-------|-----------|------------|
| p100-sxm2-16gb | 16GB | compg009, compg010, compg011 | 4 | 12 |
| v100-pcie-32gb | 32GB | compg016 | 2 | 2 |
| quadro-rtx6000 | 24GB | compg019 | 4 | 4 |
| quadro-rtx8000 | 48GB | compg028, compg029 | 4 | 8 |
| a100-pcie-40gb | 40GB | compg031, compg032, compg033 | 4 | 12 |
| a100-pcie-80gb | 80GB | compg035, compg036, compg039-041 | 4 | 20 |

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

### Basic GPU Request

The recommended methods for requesting GPUs are `--gres` or `--gpus-per-node`:

**Using --gres (Generic Resource Scheduling):**
```bash
sbatch -p gpu_short --gres gpu:N your_script.sh
```

**Using --gpus-per-node:**
```bash
sbatch -p gpu_short --gpus-per-node N your_script.sh
```

Where `N` is the number of GPUs required per node (maximum of 4 on most nodes).

**Example:**
```bash
sbatch -p gpu_short --gres gpu:1 train_model.sh
```

### Understanding Command Syntax

When checking GPU availability with `sinfo`:

```bash
sinfo -p gpu_short -o "%N %G" -N
```

- `sinfo` - Query Slurm partition and node information
- `-p gpu_short` - Specify partition to query
- `-o "%N %G"` - Output format:
  - `%N` - Node name
  - `%G` - Generic resources (GRES), showing GPU specifications
- `-N` - Node-oriented format (one line per node)

### Requesting Specific GPU Types

You can request a particular GPU model using the full GRES specification:

```bash
sbatch -p gpu_short --gres gpu:a100-pcie-80gb:1 your_script.sh
```

This requests 2 A100 80GB GPUs.

### Using GPU Constraints (Recommended)

Constraints allow you to specify acceptable GPU classes, giving the scheduler flexibility while meeting your requirements:

```bash
sbatch -p gpu_short --gpus-per-node 1 --constraint "a100|rtx8000" your_script.sh
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
sbatch -p gpu_short --gpus-per-node 1 --constraint "v100|rtx6000|rtx8000|a100" your_script.sh
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
#SBATCH -p gpu_short
#SBATCH --gres gpu:1
#SBATCH --constraint "rtx8000|a100"
#SBATCH --mem 64G
#SBATCH -c 8
#SBATCH -J my_training_job
#SBATCH -o logs/%j.out
#SBATCH -e logs/%j.err

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
#SBATCH -p gpu_short
#SBATCH --gres gpu:4
#SBATCH --constraint "a100"
#SBATCH --mem 200G
#SBATCH -c 32
#SBATCH -J multi_gpu_training

module load Python/3.11.3-GCCcore-12.3.0
source ~/venvs/pytorch/bin/activate

# Multi-GPU training with PyTorch DDP
torchrun --nproc_per_node=4 train_distributed.py
```

### Memory-Intensive Job

```bash
#!/bin/bash
#SBATCH -p gpu_short
#SBATCH --gres gpu:quadro-rtx8000:2
#SBATCH --mem-per-gpu 150G
#SBATCH -c 16
#SBATCH -J memory_intensive

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
sinfo -p gpu_short -o "%N %G" -N

# Check GPU queue status
squeue -p gpu_short

# Submit basic GPU job
sbatch -p gpu_short --gres gpu:1 script.sh

# Submit job excluding P100s
sbatch -p gpu_short --gpus-per-node 1 --constraint "a100|rtx8000" script.sh

# Interactive session
srun -p gpu_interactive --gres gpu:1 --pty bash

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
sbatch -p gpu_short --gres gpu:2 --cpus-per-gpu 4 your_script.sh

# Or specify total CPUs for the job
sbatch -p gpu_short --gres gpu:2 -c 16 your_script.sh
```

### System Memory (RAM)

**Default allocation:** 60GB of system RAM per GPU slot.

**Total RAM available:** `RAM per slot × number of GPUs requested`

**Modify RAM allocation:**

```bash
# Specify RAM per GPU
sbatch -p gpu_short --gres gpu:2 --mem-per-gpu 100G your_script.sh

# Or specify total RAM for the job
sbatch -p gpu_short --gres gpu:2 --mem 200G your_script.sh
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


