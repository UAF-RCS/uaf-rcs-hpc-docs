# What is Jupyter

[Jupyter](https://jupyter.org/documentation) is an open-source project to support interactive data science and scientific computing. [JupyterLab](https://jupyterlab.readthedocs.io/en/stable/) and [Jupyter Notebook](https://jupyter-notebook.readthedocs.io/en/stable/) are components commonly used components of it. This document is not an introduction or tutorial for using JupyterLab/Jupyter Notebook, but will show how to schedule jobs to use JupyterLab/Jupyter Notebook on Chinook.

JupyterLab/Jupyter Notebook should not be run on the Chinook login nodes as they can consume high amounts of shared resources such as CPU and Memory.

# Prerequisites

Jupyter should be installed in an [Anaconda](https://docs.anaconda.com/anaconda/user-guide/getting-started/) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html) environment. Please contact uaf-rcs@alaska.edu for help with setting up Miniconda/Anaconda environments or view Anaconda's documentation on [managing environments](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html).

# Running JupyterLab/Notebook on Chinook

JupyterLab/Notebook must be run on the compute nodes due to the amount of memory and CPU resources that a Notebook can take. Running JupyterLab/Notebook should be done by submitting a batch script to Slurm on the proper partition. JupyterLab/Notebook should only be run on the **t1/t2small** or **analysis** partition depending on how CPU intensive your JupyterLab/Notebook session is, or the **debug** partition while you are testing your Notebook.

Jobs submitted to Chinook will be run as nodes are available according to the Slurm job scheduler, jobs are **not** guaranteed to run immediately and are subject to the partition time limits. Please see our [documentation on our partitions](../using-batch/available-partitions.md) for more information.

There are two steps to starting a JupyterLab/Notebook instance on Chinook. The first is launching JupyterLab/Notebook on one of the compute nodes via Slurm and the second is setting up an SSH tunnel so you can access the instance via your local web browser.

# Submitting a JupyterLab/Notebook process to Slurm

Starting JupyterLab/Notebook on Chinook is done through a batch script that is submitted to the Slurm job scheduler. For a general overview on the batch scheduler please refer to [our documentation](../using-batch/batch-overview). This will allocate resources on the HPC cluster for your JupyterLab/Notebook instance. First you will need to prepare a script that is similar to this and save it to a file in your $HOME directory:

```
#!/bin/bash

#SBATCH --job-name="Jupyter Debug"
#SBATCH --partition=debug
#SBATCH --ntasks=24
#SBATCH --tasks-per-node=24
#SBATCH --time=00:02:00
#SBATCH --output="Jupyter.%j"

module purge
module load lang/Anaconda3/5.3.0
module load slurm

# Activate your Anaconda Environment. Replace JUPYTERENV with the name of your
# environment
# The eval "$(conda shell.bash hook)" insures that you can load you conda environment
eval "$(conda shell.bash hook)"
conda activate jupyterEnv

# Get info for SSH Tunnel, the node that you are on and your username
NODE=$(hostname -s)
USERNAME=$(whoami)

# Print tunneling instructions
echo "Instructions to create SSH tunnel. On your LOCAL machine run: "
echo "ssh $USERNAME@chinook.alaska.edu -L8888:$NODE:8888 -N"

# Run Jupyter Lab or Notebook
jupyter-lab --no-browser --port=8888 --ip=0.0.0.0

# or jupyter-notebook --no-browser --port=8888 --ip=0.0.0.0

echo "Closing Jupyter"
```

This script will activate an Anaconda environment, run JupyterLab/Notebook and start a JupyterLab/Notebook instance. It will also print the instructions for starting an SSH tunnel.

Once this script is on Chinook you can submit it to the job scheduler with the sbatch command. If we saved this script as "submitJupyterLab.slurm", it would be submitted with:

```
sbatch submitJupyterLab.slurm
```

and you will get a message with the job id number, and it will create an output file called "Jupyter.####" where #### is the Job ID:

```
Submitted batch job 390880
```

and the output in the Jupyter.#### will look like the following:

```
Instructions to create SSH tunnel. On your LOCAL machine run:
ssh $USERNAME@chinook.alaska.edu -L8888:$NODE:8888 -N
```

followed by the JupyterLab/Notebook output. It may take a minute or two for the output from the jupyter-lab or jupyter-notebook command to run and print output. It should have a line toward the bottom that looks as follows:

```
Or copy and paste one of these URLs:
    http://$NODENUMBER:8888/lab?token=285c78fb9d41286cf9ca3ad93ad70098c0a6d1ed36ff4c1b
 or http://127.0.0.1:8888/lab?token=285c78fb9d41286cf9ca3ad93ad70098c0a6d1ed36ff4c1b
```

This process will start the JupyterLab/Notebook instance on the Chinook compute nodes and will also print the instructions for setting up an SSH tunnel to the JupyterLab/Notebook instance.

# Setting up the SSH Tunnel


This step is run on your local machine, **not** Chinook.

On Linux and MacOS you can simply copy the ssh tunnel line from the output of the script.

```
ssh $USERNAME@chinook.alaska.edu -L8888:$NODE:8888 -N
```

$USERNAME will be replaced by your username on Chinook and $NODE will the be node name of the compute node that your job is currently running on. After running this command it should appear that the command is "hanging" but it will be creating an SSH tunnel to the node. You can use CTRL/CMD+C to kill it.

On Windows it will depend on what SSH client you are using. In PuTTY it will be under Change Settings->Connection->SSH->Tunnels and you will add 8888 as the Source port, $NODE:8888 as the Destination, L8888 $NODE:8888 in the Forward ports area. $NODE will be replaced by the node name of the job that you are on and will be output on the script.

# Accessing the JupyterLab/Notebook

After submitting the job to Chinook, and starting the SSH tunnel you should be able to able to go to the "127.0.0.1" URL that the script outputs in your local web browser. You can open your web browser on your local machine and paste the http://127.0.0.1:8888/lab?token=... into your URL bar and it should take you to the JupyterLab/Notebook instance running on the compute node.
