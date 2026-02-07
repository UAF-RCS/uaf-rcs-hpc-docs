# GPU Overview

Chinook has the following GPU nodes available:

* 1x Altus XE2318GT-AIR Login Node (chinookgpu.alaska.edu) with dual AMD EPYC 24-core processors \(48 cores\), 1.5 TB memory, and 8x NVIDIA L40S GPU accelerators
* 4x Altus XE2318GT-AIR Compute Nodes each with dual AMD EPYC 24-core processors \(48 cores per node\), 1.5 TB memory, and 8x NVIDIA L40S GPU accelerators, with 48GB GPU memory each
* 1 x Altus XE5318 Compute Node with dual AMD EPYC 24-core processors \(48 cores per node\), 1.5 TB memory, and 8x NVIDIA H100 GPU accelerators with 80GB GPU memory each

*Due to the limited amount of GPU resources available to the Chinook cluster, RCS will be monitoring misuse of the GPU login node or jobs that request GPU resources but leave the GPUs idle during running. RCS will terminate jobs that or processes are not using allocated GPU resources to maximise access to GPU resources*

## Usage

For information on using Chinook in general please see our [Introduction](../getting-started/introduction.md). Please note that the login node for the GPU nodes is **chinookgpu.alaska.edu**. Knowledge of the [Batch scheduler](../using-batch/batch-overview.md) is also expected.

For information about the GPUs available, please see the [GPU Node Types section](#gpu-node-types). This section will focus on using the GPU nodes.

### chinookgpu.alaska.edu

To use the GPU nodes it is recommended to log into **chinookgpu.alaska.edu**. Unlike the rest of Chinook, all nodes with GPUs use AMD's EPYC processors. This means that code or environments compiled or built on the Chinook login nodes (chinook[00-04].alaska.edu) might not work due to the differing CPU architectures. Additionally the current Chinook software stack might not work as intended. RCS is working on building a separate software stack for the GPU nodes.

Custom environments, such as Conda or Mamba environments, or personal package or build managers such as EasyBuild or Spack, should also be built or run on **chinookgpu.gi.alaska.edu** to make sure that the environment is using AMD EPYC compatibile binaries or shared libraries.

### Shared Nodes

Unlike the CPU nodes (nodes in the debug, small, and standard partitions) the GPU nodes are shared. Multiple users can run jobs on the GPU nodes. Resources such as memory and the CPUs are shared among the users on a node, so care should be taken to minimize the impact on oo

### Partitions

There are two GPU partitions:

| Name | Node Count | Max Walltime | GPUs per node | Rules | GPU Type | SBATCH directive |
| :--- | :--- | :---| :--- | :--- | :--- | :--- |
| l40s | 4 | 2 days | 8 | Only request the number of GPUs your code uses | L40S | --partition=l40s --gpus=$NUMBER_OF_GPUS --mem-per-gpu=$MEMORY |
| h100 | 1 | 2 days | 8 | Only request the number of GPUs your code uses | H100 | --partition=h100 --gpus=$NUMBER_OF_GPUS --mem-per-gpu=$MEMORY |

To submit to the partition you'll need to specify the partition (--partition=l40s OR --partition=h100) AND the number of GPUs (--gpus=$NUMBER_OF_GPUS). If the --gpus option is not specified it will default to using all available GPUs and RCS may terminate jobs that have requested GPUs that are left idle.

### CPU and Memory Resources

The GPU nodes have 1TB of memory total and 48 cores available. Due to the shared nature of these nodes we advise setting the **--mem-per-gpu** and **--cpus-per-gpu** in your srun commands or SBATCH scripts to both share resources more equitably and to allow the Slurm job scheduler to schedule allocations more efficiently. We recommend 185G of memory per GPU and 6 cores per GPU, for example **--mem-per-gpu=185G** and **--cpus-per-gpu=6**.

### Slurm

The GPU nodes can be accessed via the standard **srun** and **sbatch** commands, but need to use the following flags:

- **--partition=$GPU_PARTITION**: which type of GPU you want to use, values are l40s or h100
- **--gpus=$NUMBER_OF_GPUS**
- **--mem-per-gpu=$MEM**: the amount of system memory (**not** GPU memory) you want per GPU, our default recommendation is 185G
- **--cpus-per-gpu=$NUMBER_OF_CPUS**: the number of CPUs that you want per CPU, our default recommendation is 6

#### Interactive Example

To run an interactive job on the GPU nodes, using a single GPU you can do the following:

L40S:
```text
chinookgpu> srun -p l40s --gpus=1 --mem-per-gpu=185G --cpus-per-gpu=6 --pty /bin/bash -l
n153> nvidia-smi
Wed Feb  4 10:18:32 2026
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 570.195.03             Driver Version: 570.195.03     CUDA Version: 12.8     |
|-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA L40S                    Off |   00000000:25:00.0 Off |                    0 |
| N/A   39C    P8             34W /  350W |       0MiB /  46068MiB |      0%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+

+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI              PID   Type   Process name                        GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|  No running processes found                                                             |
+-----------------------------------------------------------------------------------------+
```

H100:
```text
chinookgpu> srun -p h100 --gpus=1 --mem-per-gpu=185G --cpus-per-gpu=6 --pty /bin/bash -l
n155> nvidia-smi
Wed Feb  4 10:17:25 2026
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 570.195.03             Driver Version: 570.195.03     CUDA Version: 12.8     |
|-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA H100 80GB HBM3          On  |   00000000:26:00.0 Off |                    0 |
| N/A   34C    P0            104W /  700W |       0MiB /  81559MiB |      0%      Default |
|                                         |                        |             Disabled |
+-----------------------------------------+------------------------+----------------------+

+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI              PID   Type   Process name                        GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|  No running processes found                                                             |
+-----------------------------------------------------------------------------------------+
```

#### SBATCH Template

A sample, commented, SBATCH script is provided below. For more information on using the batch system please see [Using the Batch System](../using-batch/using-the-batch-system.md).

```text
#!/bin/bash
# The partition can be l40s or h100
#SBATCH --partition=l40s
# The time limit for you job before it stops running, this can be up to 48 hours
# Format is DD-HH:MM:SS or HH:MM:SS
#SBATCH --time=01:00:00
# The number of GPUs can be 1-8 per node
#SBATCH --gpus=1
# Default recommendation is 185G
#SBATCH --mem-per-gpu=185G
# Default recommendation is 6
#SBATCH --cpus-per-gpu=6

# Example program to run, replace with your own programs/BASH script
nvidia-smi
```

## GPU Node Types

### Login Node

The GPU login node, chinookgpu.alaska.edu, is intended to provide access to the cluster, to compile and modify applications and workflows, to manage data between mounted filesystems, and to manage jobs. All processing should be very limited and short to avoid impacting other users' activities. Any processing should should be done in [Batch](../using-batch/using-the-batch-system.md) or [interactive](../using-batch/interactive-jobs.md) modes using the **l40s** or **h100** partitions. RCS reserves the right to terminate user processes or sessions to maintain the normal working order of the login node and the cluster.

### GPU Compute Nodes

The GPU compute nodes are where computation is performed and accessed through the [job scheduler](../using-batch/batch-overview.md). Each GPU Compute node have 8 GPUs available to them and are **shared**, which means multiple users can make use of the same node at the same time. Chinook has two GPU types available: the L40S and the H100

### L40S Nodes

The L40S GPU are more suited for small-model training, inference and fine-tuning. They are limited to Floating Point 32-bit operations, and have 48GB of GPU memory, less compared to the H100s. The L40S can also be used for graphics and general GPU computing as well, so long as 64-bit precision is *not* needed.

### H100 Nodes

The H100 GPU are suit for medium to large AI model training, as well as fine-tuning medium to large models. They can handle Floating Point 64-bit operations and are suited for large-scale simulations and deep learning applications that may need more computational power. The H100 also has 80GB of GPU memory.

## GPU Usage Verification

If you suspect that your code is not actually using the GPUs, there are generally some tests that you can run. 

You can run the **nvidia-smi** command which will display how many GPUs are currently running, for example if you run an interactive job requesting 3 GPUs, the following nvidia-smi output should look as follows

```
chinook02> srun -p l40s --gpus=3 --mem-per-gpu=185G --cpu--pty /bin/bash
n151> nvidia-smi
Thu Feb  5 15:30:14 2026
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 570.195.03             Driver Version: 570.195.03     CUDA Version: 12.8     |
|-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA L40S                    Off |   00000000:25:00.0 Off |                    0 |
| N/A   44C    P0             83W /  350W |   41515MiB /  46068MiB |      0%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+
|   1  NVIDIA L40S                    Off |   00000000:28:00.0 Off |                    0 |
| N/A   36C    P8             34W /  350W |       0MiB /  46068MiB |      0%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+
|   2  NVIDIA L40S                    Off |   00000000:45:00.0 Off |                    0 |
| N/A   37C    P8             23W /  350W |       0MiB /  46068MiB |      0%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+

+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI              PID   Type   Process name                        GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|    0   N/A  N/A         3330776      C   ...ma.cpp/build/bin/llama-server      41504MiB |
+-----------------------------------------------------------------------------------------+
```

Often tools or programs that you run may also have methods of checking whether GPUs are available.

PyTorch, a commonly used deep learning framework, has these the **torch.cuda.is_available()** and **torch.cuda.get_device_properties()** functions which may be valuable to run either as a standalone test at the beginning of your batch script or as part of your PyTorch run:

```
# checkGPUs.py
import torch
print("CUDA available: str(torch.cuda.is_available()))
for i in range(torch.cuda.device_count()):
     print(torch.cuda.get_device_properties(i).name)
```

which should display the whether or not CUDA is available and how many of each GPUs it has available:

```
# Output of checkGPUs.py
CUDA available: True
NVIDIA H100 80GB HBM3
NVIDIA H100 80GB HBM3
NVIDIA H100 80GB HBM3
NVIDIA H100 80GB HBM3
NVIDIA H100 80GB HBM3
```

This can be added to an SBATCH script to verify in your output that the GPUs are available and that you're seeing the correct amount.