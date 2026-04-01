# What is Apptainer

Apptainer is a system that allows users to run applications within a "container" that packages all software dependencies into an "image". This allows a user to run software that may need system libraries that are not available on Chinook. For example software may need a version of GLIBC that is unavailable on Chinook, or software was built on Ubuntu and rebuilding it for CentOS may be difficult. Using a Apptainer container can mitigate these issues.

#### Running Apptainer

You can run a program using the `apptainer exec` command:

```
apptainer exec /usr/local/unsupported/$PROJECT/$IMG ld --version

GNU ld version 2.27-34.base.el7
Copyright (C) 2016 Free Software Foundation, Inc.
This program is free software; you may redistribute it under the terms of
the GNU General Public License version 3 or (at your option) a later version.
This program has absolutely no warranty
```

#### Mounting Directories

By default Apptainer will bind your current working directory and your $HOME directory to the container, allowing those files to be accessed. However if you need other directories to be accessible to the Apptainer image you will have to bind those explicitly using the `--bind` option. For example this will bind a user's `$CENTER1 directory` to `/mnt/center1` in the container:

`apptainer exec --bind $CENTER1:/mnt/center1 /usr/local/unsupported/$PROJECT/$IMG ls /mnt/center1`

If you need to bind multiple directories you will need to separate each "mount pair" with a comma. For example if we wanted to bind `$CENTER1` and `$ARCHIVE` to `/mnt/center1` and `/mnt/archive` in the container:

`apptainer exec --bind $CENTER1:/mnt/center1,$ARCHIVE:/mnt/archive /usr/local/unsupported/$PROJECT/$IMG ls /mnt/archive`

#### Environment Variables

When using the `apptainer exec` command Environment Variables on the host machine are present in your Apptainer container. However if they point to directories or commands that are not in the container then they will not reference anything.

If you need to set an environment variable at runtime you can using the `APPTAINERENV_` prefix before running the command:

```
APPTAINERENV_HELLO=WORLD apptainer exec /usr/local/unsupported/$PROJECT/$IMG env | grep HELLO

HELLO=WORLD
```

Please note that you cannot use this to overwrite an environment variable in the Host environment. If you need to do so, you would need to run the `--cleanenv` flag. You may want to do this if you'd like to set the $CENTER1 or $ARCHIVE variables in your container. Multiple environments can be set by separateing them with a space (` `):

```
APPTAINERENV_CENTER1=/mnt/center1 APPTAINERENV_ARCHIVE=/mnt/archive apptainer exec --cleanenv --bind $CENTER1:/mnt/center1,$ARCHIVE:/mnt/archive /usr/local/unsupported/$PROJECT/$IMG env | grep CENTER1

CENTER1=/mnt/center1
```

#### Using Apptainer in a batch script

Apptainer can be used in a batch script by loading the Apptainer module and running the `apptainer exec` command.

```
#!/bin/bash
#SBATCH --job-name="My Apptainer Job"
#SBATCH --partition=debug
#SBATCH --ntasks=24
#SBATCH --time=00:30:00
#SBATCH --tasks-per-node=24
#SBATCH --output="myjob.%j"

module purge

apptainer exec /usr/local/unsupported/$PROJECT/$IMG /mnt/center1/myScript
```

Additionally if you need to run a set of commands in an Apptainer environment you can use the `apptainer shell` command. This can be useful if the whole pipeline is installed in the container.

```
#!/bin/bash
#SBATCH --job-name="My Apptainer Job"
#SBATCH --partition=debug
#SBATCH --ntasks=24
#SBATCH --time=00:30:00
#SBATCH --tasks-per-node=24
#SBATCH --output="myjob.%j"

module purge

apptainer shell \
    --bind $CENTER1:/mnt/center1 \
    /usr/local/unsupported/$PROJECT/$IMG <<EOF
/mnt/center1/processingScript.py
/mnt/center1/analyzingScript.py
EOF
```
This script will bind $CENTER1 to /mnt/center1 inside the Apptainer container and then execute the commands in between `<<EOF` and `EOF` in a shell in the container, in this example running "processingScript.py" and following that with "analyzingScript.py" which are located in $CENTER1, which has been bound to /mnt/center1 in the container.

#### Creating Images

One advantage to Apptainer as a container solution is that Apptainer does not require admin access to run. Therefore users, if needed, and create or obtain images themselves to run on Chinook.

Images will need to be created on a system that the user has Administrator access to and **users cannot create Apptainer images on Chinook itself**. Information on building a container can be located [via Singularity's documentation](https://sylabs.io/guides/3.2/user-guide/build_a_container.html)
