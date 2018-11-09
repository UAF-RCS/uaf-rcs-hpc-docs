# Common Slurm Commands

#### sacct <a id="sacct"></a>

The `sacct` command is used for viewing information about submitted jobs. This can be useful for monitoring job progress or diagnosing problems that occurred during job execution. By default, `sacct` will report the job ID, job name, partition, account, allocated CPU cores, job state, and the exit code for all of the current user's jobs that have been submitted since midnight of the current day.

`sacct`'s output, as with most Slurm informational commands, can be customized in a large number of ways. Here are a few of the more useful options:

| Command | Result |
| :--- | :--- |
| `sacct --starttime 2016-03-01` | select jobs since midnight of March 1, 2016 |
| `sacct --allusers` | select jobs from all users \(default is only the current user\) |
| `sacct --accounts=account_list` | select jobs whose account appears in a comma-separated list of accounts |
| `sacct --format=field_names` | print fields specified by a comma-separated list of field names |
| `sacct --helpformat` | print list of fields that can be specified with `--format` |

For more information on `sacct`, please visit [https://slurm.schedmd.com/sacct.html](https://slurm.schedmd.com/sacct.html).

#### sbatch <a id="sbatch"></a>

The `sbatch` command is used for submitting jobs to the cluster. Although it is possible to supply command-line arguments to `sbatch`, it is generally a good idea to put all or most resource requests in the [batch script](https://www.gi.alaska.edu/research-computing-systems/hpc/chinook/using-batch-system#batch-scripts) for reproducibility.

Sample usage:

```text

```

On successful batch submission, `sbatch` will print out the new job's ID. `sbatch` may fail if the resources requested cannot be satisfied by the indicated partition.

For more information on `sbatch`, please visit [https://slurm.schedmd.com/sbatch.html](https://slurm.schedmd.com/sbatch.html).

#### scontrol <a id="scontrol"></a>

The `scontrol` command is used for monitoring and modifying queued or running jobs. Although many `scontrol` subcommands apply only to cluster administration, there are some that may be useful for users:

| Command | Result |
| :--- | :--- |
| `scontrol hold job_id` | place hold on job specified by job\_id |
| `scontrol release job_id` | release hold on job specified by job\_id |
| `scontrol show reservation` | show details on active or pending reservations |
| `scontrol show nodes` | show hardware details for compute nodes |

For more information on `scontrol`, please visit [https://slurm.schedmd.com/scontrol.html](https://slurm.schedmd.com/scontrol.html).

#### sinfo <a id="sinfo"></a>

The `sinfo` command is used for viewing compute node and partition status. By default, `sinfo`will report the ID, partition, job name, user, state, time elapsed, nodes requested, nodes held by running jobs, and reason for being in the queue for queued jobs.

`sinfo`'s output, as with most Slurm informational commands, can be customized in a large number of ways. Here are a few of the more useful options:

| Command | Result |
| :--- | :--- |
| `sinfo --partition=t1standard` | show node info for the partition named 't1standard' |
| `sinfo --summarize` | group by partition, aggregate state by A/I/O/T \(Available/Idle/Other/Total\) |
| `sinfo --reservation` | show Slurm reservation information |
| `sinfo --format=format_tokens` | print fields specified by `format_tokens` |
| `sinfo --Format=field_names` | print fields specified by comma-separated `field_names` |

There are a large number of fields hidden by default that can be displayed using `--format` and `--Format`. Refer to the `sinfo`'s manual page for the complete list of fields.

For more information on `sinfo`, please visit [https://slurm.schedmd.com/sinfo.html](https://slurm.schedmd.com/sinfo.html).

#### smap <a id="smap"></a>

The `smap` command is an ncurses-based tool useful for viewing the status of jobs, nodes, and node reservations. It aggregates data exposed by other Slurm commands, such as [sinfo](https://www.gi.alaska.edu/research-computing-systems/hpc/chinook/using-batch-system#sinfo) and [squeue](https://www.gi.alaska.edu/research-computing-systems/hpc/chinook/using-batch-system#squeue).

| Command | Result |
| :--- | :--- |
| `sinfo -i 15` | Run sinfo, refreshing every 15 seconds |

For more information on `smap`, please visit [https://slurm.schedmd.com/smap.html](https://slurm.schedmd.com/smap.html).

#### squeue <a id="squeue"></a>

The `squeue` command is used for viewing job status. By default, `squeue` will report the ID, partition, job name, user, state, time elapsed, nodes requested, nodes held by running jobs, and reason for being in the queue for queued jobs.

`squeue`'s output, as with most Slurm informational commands, can be customized in a large number of ways. Here are a few of the more useful options:

| Command | Result |
| :--- | :--- |
| `squeue --user=user_list` | filter by a comma-separated list of usernames |
| `squeue --start` | print expected start times of pending jobs |
| `squeue --format=format_tokens` | print fields specified by `format_tokens` |
| `squeue --Format=field_names` | print fields specified by comma-separated `field_names` |

The majority of `squeue`'s customization is done using `--format` or `--Format`. The lowercase `--format` allows for controlling which fields are present, their alignments, and other contextual details such as whitespace, but comes at the cost of readability and completeness \(not all fields can be specified using the provided tokens\). In contrast, the capitalized `--Format` accepts a complete set of verbose field names, but offers less flexibility with contextual details.

As an example, the following command produces output identical to `squeue --start`:

```text
squeue --format="%.18i %.9P %.8j %.8u %.2t %.19S %.6D %20Y %R" --sort=S --states=PENDING
```

`--Format` can produce equivalent \(but not identical\) output:

```text
squeue --Format=jobid,partition,name,username,state,starttime,numnodes,schednodes,reasonlist --sort=S --states=PENDING
```

For more information on `squeue`, please visit [https://slurm.schedmd.com/squeue.html](https://slurm.schedmd.com/squeue.html).

#### sreport <a id="sreport"></a>

The `sreport` command is used for generating job and cluster usage reports. Statistics will be shown for jobs run since midnight of the current day by default. Although many of `sreport`'s reports are more useful for cluster administrators, there are some commands that may be useful to users:

| Command | Result |
| :--- | :--- |
| `sreport cluster AccountUtilizationByUser -t Hours start=2016-03-01` | report hours used since Mar 1, 2016, grouped by account |
| `sreport cluster UserUtilizationByAccount -t Hours start=2016-03-01 Users=$USER` | report hours used by the current user since Mar 1, 2016 |

For more information on `sreport`, please visit [https://slurm.schedmd.com/sreport.html](https://slurm.schedmd.com/sreport.html).

#### srun <a id="srun"></a>

The `srun` command is used to launch a parallel job step. Typically, `srun` is invoked from a Slurm batch script to perform part \(or all\) of the job's work. `srun` may be used multiple times in a batch script, allowing for multiple program runs to occur in one job.

Alternatively, `srun` can be run directly from the command line on a login node, in which case `srun` will first create a resource allocation for running the job. Use command-line keyword arguments to specify the parameters normally used in batch scripts, such as `--partition`, `--nodes`, `--ntasks`, and others. For example, `srun --partition=debug --nodes=1 --ntasks=8 whoami` will obtain an allocation consisting of 8 cores on 1 node and then run the command `whoami` on all of them.

Please note that `srun` **does not inherently parallelize programs** - it simply runs many independent instances of the specified program in parallel across the nodes assigned to the job. Put another way, `srun` will launch a program in parallel, but makes no guarantee that the program is designed to be run in parallel at any degree.

See [Interactive Jobs](https://www.gi.alaska.edu/research-computing-systems/hpc/chinook/using-batch-system#interactive-jobs) for an example of how to use `srun`to allocate and run an interactive job \(i.e. a job whose input and output are attached to your terminal\).

A note about MPI: `srun` is designed to run MPI applications without the need for using `mpirun`or `mpiexec`, but this ability is currently not available on Chinook. It may be made available in the future. Until then, please refer to the directions on how to [run MPI applications on Chinook](https://www.gi.alaska.edu/research-computing-systems/hpc/chinook/using-batch-system#batch-scripts-mpi) below.

For more information on `srun`, please visit [https://slurm.schedmd.com/srun.html](https://slurm.schedmd.com/srun.html).

#### sview <a id="sview"></a>

The `sview` command is a graphical interface useful for viewing the status of jobs, nodes, partitions, and node reservations. It aggregates data exposed by other Slurm commands, such as [sinfo](https://www.gi.alaska.edu/research-computing-systems/hpc/chinook/using-batch-system#sinfo), [squeue](https://www.gi.alaska.edu/research-computing-systems/hpc/chinook/using-batch-system#squeue), and [smap](https://www.gi.alaska.edu/research-computing-systems/hpc/chinook/using-batch-system#smap), and refreshes every few seconds.

For more information on `sview`, please visit [https://slurm.schedmd.com/sview.html](https://slurm.schedmd.com/sview.html).

