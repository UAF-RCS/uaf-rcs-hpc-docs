# Batch Scripts

Batch scripts are plain-text files that specify a job to be run. They consist of batch scheduler \(Slurm\) directives which specify the resources requested for the job, followed by a script used to successfully run a program.

Here is a simple example of a batch script that will be accepted by Slurm on Chinook:

```text
#!/bin/bash
#SBATCH --partition=debug
#SBATCH --ntasks=24
#SBATCH --tasks-per-node=24
#If running on the bio or analysis queue add:
#SBATCH --mem=214G

echo "Hello world"
```

On submitting the batch script to Slurm using `sbatch`, the job's ID is printed:

```text
$ ls
hello.slurm
$ sbatch hello.slurm
Submitted batch job 8137
```

Among other things, Slurm stores what the current working directory was when `sbatch` was run. Upon job completion \(nearly immediate for a trivial job like the one specified by `hello.slurm`\), output is written to a file in that directory.

```text
$ ls
hello.slurm  slurm-8137.out
$ cat slurm-8137.out
Hello world
```

#### Running an MPI Application <a id="batch-scripts-mpi"></a>

Here is what a batch script for an MPI application might look like:

```text
#!/bin/sh

#SBATCH --partition=t1standard
#SBATCH --ntasks=<NUMTASKS>
#SBATCH --tasks-per-node=24
#SBATCH --mail-user=<USERNAME>@alaska.edu
#SBATCH --mail-type=BEGIN
#SBATCH --mail-type=END
#SBATCH --mail-type=FAIL
#SBATCH --output=<APPLICATION>.%j

ulimit -s unlimited
ulimit -l unlimited

# Load any desired modules, usually the same as loaded to compile
. /etc/profile.d/modules.sh
module purge
module load toolchain/intel/2023
module load slurm

cd $SLURM_SUBMIT_DIR
# Launch the MPI application
mpirun -np $SLURM_NTASKS ./<APPLICATION>
```

* &lt;APPLICATION&gt;: The executable to run in parallel
* &lt;NUMTASKS&gt;: The number of parallel tasks requested from Slurm
* &lt;USERNAME&gt;: Your Chinook username \(same as your UA username\)

There are many environment variables that Slurm defines at runtime for jobs. Here are the ones used in the above script:

* $SLURM\_JOB\_ID: The job's numeric id
* $SLURM\_NTASKS: The value supplied as &lt;NUMTASKS&gt;
* $SLURM\_SUBMIT\_DIR: The current working directory when "sbatch" was invoked

