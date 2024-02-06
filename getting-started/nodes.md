# Node Types

## Login Nodes

Login nodes are front-end nodes that you log into to access the cluster. These nodes are used for compiling code, modifying applications and workflows, managing data between the different [mounted filesystems](../available-filesystems/available-filesystems.md), and to manage jobs. Login nodes are shared between all users so any processing or compiling should be kept as short as possible to not impact other users.

Submitting jobs is done using a [batch scheduler](../using-batch/batch-overview.md). Chinook uses [Slurm](../using-batch/common-slurm-commands.md). The status of jobs and the nodes can be monitored from the login nodes.

Current login nodes:

chinook03.alaska.edu
chinook04.alaska.edu

## Data Mover Nodes

Data mover nodes are used for transferring data between various [mounted filesystems](../available-filesystems/available-filesystems.md) and to and from RCS managed storage from other servers. ONLINE filesystems may be accessible via SAMBA from the data mover nodes.

Current data mover nodes:

bigdipper.alaska.edu

## Compute Nodes

Compute nodes are where computation is performed and are accessed through the [job scheduler](../using-batch/batch-overview.md). Generally to perform tasks faster than a standard computer or laptop one must make use of parallel processing. 

## Analysis/Bio Nodes

## GPU Nodes
