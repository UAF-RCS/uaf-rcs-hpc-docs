# What is Singularity

Singularity is a system that allows users to run applications within a "container" that packages all software dependencies into an "image". This allows a user to run software that may need system libraries that are not available on Chinook. For example software may need a version of GLIBC that is unavailable on Chinook, or software was built on Ubuntu and rebuilding it for CentOS may be difficult. Using a Singularity container can mitigate these issues.

#### Running Singularity

To run Singularity, the singularity environment module needs to be loaded: `module load singularity`. Afterwards you can run a program using the `singularity exec` command:

```
module load singularity
singularity exec /usr/local/unsupported/SINGULARITY/centos7.img ld --version

GNU ld version 2.27-34.base.el7
Copyright (C) 2016 Free Software Foundation, Inc.
This program is free software; you may redistribute it under the terms of
the GNU General Public License version 3 or (at your option) a later version.
This program has absolutely no warranty
```

#### Mounting Directories

By default Singularity will bind your current working directory and your $HOME directory to the container, allowing those files to be accessed. However if you need other directories to be accessible to the Singularity image you will have to bind those explicitly using the `--bind` option. For example this will be bind a user's `$CENTER1 directory` to `/mnt/center1` in the container:

`singularity exec --bind $CENTER1:/mnt/center1 /usr/local/unsupported/SINGULARITY/centos7.img ls /mnt/center1`

If you need to bind multiple directories you will need to separate each "mount pair" with a comma. For example if we wanted to bind `$CENTER1` and `$ARCHIVE` to `/mnt/center1` and `/mnt/archive` in the container:

`singularity exec --bind $CENTER1:/mnt/center1,$ARCHIVE:/mnt/archive /usr/local/unsupported/SINGULARITY/centos7.img ls /mnt/archive`

#### Environment Variables

When using the `singularity exec` command Environment Variables on the host machine are present in your Singularity container. However if they point to directories or commands that are not in the container than they will not reference anything.

If you need to set an environment variable at runtime you can using the `SINGULARITYENV_` prefix before running the command:

```
SINGULARITYENV_HELLO=WORLD singularity exec /usr/local/unsupported/SINGULARITY/centos7.img env | grep HELLO

HELLO=WORLD
```

Please note that you cannot use this to overwrite an environment variable in the Host environment. If you need to do so, you would need to run the `--cleanenv` flag. You may want to do this if you'd like to set the $CENTER1 or $ARCHIVE variables in your container. Multiple environments can be set by separateing them with a space (` `):

```
SINGULARITYENV_CENTER1=/mnt/center1 SINGULARITYENV_ARCHIVE=/mnt/archive singularity exec --cleanenv --bind $CENTER1:/mnt/center1,$ARCHIVE:/mnt/archive /usr/local/unsupported/SINGULARITY/centos7.img env | grep CENTER1

CENTER1=/mnt/center1
```

#### Using Singularity in a batch script

Singularity can be used in a batch script by loading the Singularity module and running the `singularity exec` command.

```
#!/bin/bash
#SBATCH --job-name="My Singularity Job"
#SBATCH --partition=debug
#SBATCH --ntasks=24
#SBATCH --time=00:30:00
#SBATCH --tasks-per-node=24
#SBATCH --output="myjob.%j"

module purge
module load singularity

singularity exec /usr/local/unsupported/SINGULARITY/centos7.img /mnt/center1/myScript
```

Additionally if you need to run a set of commands in a Singularity environment you can use the `singularity shell` command. This can be useful if the whole pipeline is installed in the container.

```
#!/bin/bash
#SBATCH --job-name="My Singularity Job"
#SBATCH --partition=debug
#SBATCH --ntasks=24
#SBATCH --time=00:30:00
#SBATCH --tasks-per-node=24
#SBATCH --output="myjob.%j"

module purge
module load singularity

singularity shell \
    --bind $CENTER1:/mnt/center1 \
    /usr/local/unsupported/SINGULARITY/centos7.img <<EOF
/mnt/center1/processingScript.py
/mnt/center1/analyzingScript.py
EOF
```
This script will bind $CENTER1 to /mnt/center1 inside the Singularity container and then execute the commands in between `<<EOF` and `EOF` in a shell in the container, in this example running "processingScript.py" and following that with "analyzingScript.py" which are located in $CENTER1, which has been bound to /mnt/center1 in the container.

#### Creating Images

One advantage to Singularity as a container solution is that Singularity does not require admin access to run. Therefore users, if needed, and create or obtain images themselves to run on Chinook.

Images will need to be created on a system that the user has Administrator access to and **users cannot create Singularity images on Chinook itself**. Information on building a container can be located [via Singularity's documentation](https://sylabs.io/guides/3.2/user-guide/build_a_container.html)
