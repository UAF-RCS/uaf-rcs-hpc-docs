# Batch Overview

The general principle behind batch processing is automating repetitive tasks. Single tasks are known as _jobs_, while a set of jobs is known as a _batch_. This distinction is mostly academic, since the terms _job_ and _batch job_ are now mostly synonymous, but here we'll use the terms separately.

There are three basic steps in a batch or job-oriented workflow:

1. Copy input data from archival storage to scratch space
2. Run computational tasks over the input data
3. Copy output to archival storage

On Chinook the first and last steps must occur on _login nodes_, and the computation step on _compute nodes_. This is enforced by the login nodes having finite CPU [ulimits](https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins.html#index-ulimit) set and [$ARCHIVE](https://www.gi.alaska.edu/research-computing-systems/hpc/chinook/filesystems#archive) not being present on the compute nodes.

Depending on the scale and characteristics of a particular job, different jobs may require different combinations of computational resources. Garnering these resources is a combination of:

* Choosing which [partition](https://www.gi.alaska.edu/research-computing-systems/hpc/chinook/using-batch-system#available-partitions) to submit the job to
* Choosing what resources to request from the partition

This is done by writing [batch scripts](https://www.gi.alaska.edu/research-computing-systems/hpc/chinook/using-batch-system#batch-scripts) whose directives specify these resources.

