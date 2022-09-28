# Miniconda

[Conda](https://conda.io/projects/conda/en/latest/index.html) is a manager for packages, dependencies, and environments for Python. It also allows installation of other software in the form of precompiled binaries.

[Miniconda](https://docs.conda.io/en/latest/miniconda.html) is a minimal installer for conda, and our recommendation if you need to use Conda due to the smaller overhead compared to Anaconda as well as not including many superfluous packages. Miniconda can be installed in any directory you have write access to.

# Installation

The easiest way to install Miniconda is to download the latest version from the [Miniconda repository](https://repo.anaconda.com/miniconda/) and running the script.

On Chinook you can do so with these instructions
```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
chmod u+x Miniconda3-latest-Linux-x86_64.sh
./Miniconda3-latest-Linux-x86_64.sh
```
and follow the directions in the script.

After logging out and back into the system Miniconda should be available.

# Best Practices on Chinook

Miniconda is a convenient and easy way to install Python and software packages that works extremely well on local desktops, but there are some best practices to keep in mind when running on an HPC system such as Chinook.

* Mixing Software Modules and Miniconda environments may lead to incompatibilities. In general only load the slurm module when using a conda environment.
* Miniconda and conda environments should never be installed in $ARCHIVE
* The $HOME and $CENTER1 have quotas on the number of files you may have. Python environments tend to generate a lot of files, so please be cautious of how many environments you have and how many packages you are installing. You can run
```
du -s --inodes $HOME

or

show_storage
```
to view how many files you currently have in your home directory.
* Unused environments should be deleted

# Using Conda with sbatch

When running a job on the compute nodes via sbatch you will need to initialize conda and load your environment in your script. For example:

```
#!/bin/bash
#SBATCH --ntasks=24
#SBATCH --tasks-per-node=24
#SBATCH --partition=t1small
#SBATCH --time=01:00:00
#SBATCH --job-name="Conda_Example.%j"

module purge
module load slurm

ulimit -l unlimited

eval "$(conda shell.bash hook)"
conda activate $ENVIRONMENT 
python script.py
```

replacing $ENVIRONMENT with the name of your Miniconda environment.
