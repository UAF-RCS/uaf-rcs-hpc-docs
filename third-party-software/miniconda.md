# Miniconda

[Mamba](https://github.com/mamba-org/mamba) is a reimplementation of the Conda package manager in C++, with a focus on increasing the speed and efficiency, especially with solving dependencies. Mamba is RCS' recommendation for a Conda package manager.

[Conda](https://conda.io/projects/conda/en/latest/index.html) is a manager for packages, dependencies, and environments for Python. It also allows installation of other software in the form of precompiled binaries.

[Miniconda](https://docs.conda.io/en/latest/miniconda.html) is a minimal installer for conda, and our recommendation if you need to use Conda due to the smaller overhead compared to Anaconda as well as not including many superfluous packages. Miniconda can be installed in any directory you have write access to.

# Installation

The easiest way to install Mamba is to followed the [Miniforge3 instructions](https://github.com/conda-forge/miniforge?tab=readme-ov-file#install).

On Chinook you can do so with these instructions
```
wget "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
chmod u+x Miniforge3-Linux-x86_64.sh
./Miniforge3-Linux-x86_64.sh
```
and follow the directions in the script.

After logging out and back into the system Mamba should be available.

# Best Practices on Chinook

Mamba is a convenient and easy way to install Python and software packages that works extremely well on local desktops, but there are some best practices to keep in mind when running on an HPC system such as Chinook.

* Mixing Software Modules and Mamba environments may lead to incompatibilities. In general only load the slurm module when using a conda environment.
* Mamba and conda environments should never be installed in $ARCHIVE
* The $HOME and $CENTER1 have quotas on the number of files you may have. Python environments tend to generate a lot of files, so please be cautious of how many environments you have and how many packages you are installing. You can run
```
du -s --inodes $HOME

or

show_storage
```
to view how many files you currently have in your home directory.
* Unused environments should be deleted
* We recommend installing large conda environments into an Apptainer container to cut down on the number of files used as well as speed up accessing yoour environment

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
