# Overview

High Performance Computing (HPC) is a method to use multi-processor computing to perform calculations and data analysis that need more resources than are available on a standard desktop or laptop computer. HPC is typically performed on a cluster which is comprised of many `nodes` (servers) each with multiple `cores` (processors). Programs are run on the cluster by submitting them to the `batch scheduler` from a `login node` usually via a `batch script` where they will be placed into a queue and run when resources are available.

The general process for running a job on Chinook is as follows:

* Verify that your code can make use of parallel processing, such as by being able to run multiple instances of your code at the same time, it makes of multi-core APIs (such as OpenMP), or makes use of multi-node APIs (such as MPI).
* Copy your code or program and data from your local computer to Chinook via a login or data mover node
* Recompile or verify that your code or program runs on Chinook
* Create a batch script to run your job on the compute nodes 

# Logging In

Use the SSH client you have chosen and installed to connect to `chinook.alaska.edu`. When prompted for a username, either interactively or while configuring the client, you should provide your UA username. You will be prompted for a password upon opening an SSH connection. When this happens, enter your UA password.

For further information please see our [SSH documentation](ssh.md).

The Chinook login nodes are intended to provide access to the cluster, to compile and modify applications and workflows, to manage data between the mounted filesystems, and to manage jobs. Any processing should be very limited and short to avoid impacting other users' activities. [Batch](../using-batch/using-the-batch-system.md) or [interactive](../using-batch/interactive-jobs.md) serial or parallel processing should take place on the compute nodes. RCS reserves the right to terminate user processes or sessions to maintain the normal working order of the login nodes and the cluster.

For further information about the various nodes on Chinoook please see our [Nodes documentation](nodes.md).

Chinook is a shared resource and users are asked to be neighborly to your fellow colleagues and students. Some helpful tips to keep in mind:

* The login nodes are only to be used for compiling and modifying applications/workflows, managing data between the mounted filesystems and managing jobs
* Computationally intensive work is to be done on the [compute nodes](../using-batch/using-the-batch-system.md).
* Run code in the debug queue before submitting it to the small, standard, bio, or analysis partition to ensure that it works correctly and utilizes all the resources available to the job
* Jobs that are serial in nature or interactive, such as MATLAB, should be run in the bio or analysis partition to ensure maximum utilization of our limited resources
* Jobs submitted to the bio or analysis partition must include the amount of memory the job will use (#SBATCH --mem=\<size\[units]>)
* Include a time limit in your batch scripts to help improve the performance of the scheduler in prioritizing jobs

# Terminology
