# Overview

High Performance Computing (HPC) is a method to use multi-processor computing to perform calculations and data analysis that need more resources than are available on a standard desktop or laptop computer. HPC is typically performed on a cluster which is comprised of many `nodes` (servers) each with multiple `cores` (processors). Programs are run on the cluster by submitting them to the `batch scheduler` from a `login node` usually via a `batch script` where they will be placed into a queue and run when resources are available. Nodes are separated into multiple types, such as login, compute, gpu, and analysis nodes.

For more information on nodes please see our [nodes overview](./nodes.md).

To access the cluster you will need to use a `SSH client`, which allows you to remotely access the cluster. To learn more about SSH please see [Logging In](#logging-in).

The general process for running a job on Chinook is as follows:

* Verify that your code can make use of parallel processing, such as by being able to run multiple instances of your code at the same time, it makes of multi-core APIs (such as OpenMP), or makes use of multi-node APIs (such as MPI).
* Copy your code or program and data from your local computer to Chinook via a login or data mover node
* Recompile or verify that your code or program runs on Chinook
* Create a batch script to run your job on the compute nodes
* Submit the batch script to the job scheduler from a login node

# Linux

Chinook runs the Rocky Linux 8 Operating System and is accessible via the command line terminal. To make full use of the Chinook HPC cluster some Linux knowledge is recommended. Plase see our [Linux training overview page](./linux-training-overview.md) for RCS recommended resources.

# Logging In

Use the SSH client you have chosen and installed to connect to `chinook.alaska.edu`. When prompted for a username, either interactively or while configuring the client, you should provide your UA username. You will be prompted for a password upon opening an SSH connection. When this happens, enter your UA password.

For further information please see our [SSH documentation](ssh.md).

The Chinook login nodes are intended to provide access to the cluster, to compile and modify applications and workflows, to manage data between the mounted filesystems, and to manage jobs. Any processing should be very limited and short to avoid impacting other users' activities. [Batch](../using-batch/using-the-batch-system.md) or [interactive](../using-batch/interactive-jobs.md) serial or parallel processing should take place on the compute nodes. RCS reserves the right to terminate user processes or sessions to maintain the normal working order of the login nodes and the cluster.

For further information about the various nodes on Chinoook please see our [Nodes documentation](nodes.md).

Chinook is a shared resource and users are asked to be neighborly to your fellow colleagues and students. Some helpful tips to keep in mind:

* The login nodes are only to be used for compiling and modifying applications/workflows, managing data between the mounted filesystems and managing jobs
* Computationally intensive work is to be done on the [compute nodes](../using-batch/using-the-batch-system.md).
* Run code in the debug queue before submitting it to the small, standard, bio, or analysis partition to ensure that it works correctly and utilizes all the resources available to the job
* Jobs that are serial in nature or interactive, such as non parallel MATLAB scfripts, should be run in the bio or analysis partition to ensure maximum utilization of our limited resources
* Jobs submitted to the bio or analysis partition must include the amount of memory the job will use (#SBATCH --mem=\<size\[units]>)
* Include a time limit in your batch scripts to help improve the performance of the scheduler in prioritizing jobs

# Available Filesystems

There are three filesystems that are available to all Chinook users, $HOME, $CENTER1, and $ARCHIVE, which all serve different purposes. Please see [our available filesystems page](../available-filesystems/available-filesystems.md) for in depth information.

## $HOME
A user's $HOME directory, with a 50GB quota. Compiled programs and small files should be placed here.

## $CENTER1
A scratch (**not backed up** ) parallel filesystem for computational data. Results may be placed here **temporarily**, but should be moved to a different location that is backed up. Large amounts of small files do not work well with the parallel filesystem and may cause slower performance.

## $ARCHIVE
A tape backed, long-term storage filesystem for files that are not accessed frequently. This filesystem is not available on the compute nodes due to slow file access caused by being files being on tape. If possible files should be compressed together into a zip or tar.gz file before being copied to $ARCHIVE and when accessing files from $ARCHIVE, should be "staged" by using the "batch_stage" command before attempting to read/write to a file.

# Software

Software on Chinook is typically accessed via the LMod environment module system, which sets environment variables on the system to allow access to software and libraries. All software installed on a login node is also available on the compute nodes. To view what software is available you can use the "module spider" command which will bring up information about a software module, as well as what needs to be loaded. Common modules to load are the slurm module for job scheduling and typically a compiler toolchain such as intel or foss (gnu compilers). Please see our [LMod documentation](../third-party-software/lmod.md) for more information.

Chinook users may compile their own software, use conda, or containers as well typically placing the files in the $HOME directory. For more information please see our [software overview](../third-party-software/software-overview.md) page.

# Batch Scheduler

Access to the compute nodes is handled via the [Slurm Job Scheduler](https://slurm.schedmd.com/quickstart.html). Chinook users submit "jobs", typically via a batch script to run programs and software on the compute nodes. Each job is placed into a queue that Slurm processes and launches jobs based on resources and priority. RCS uses a multi-factor prioritization scheme to determine a job's priority.

For more information please see our [batch overview](../using-batch/batch-overview.md)