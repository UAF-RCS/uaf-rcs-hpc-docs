# Available Filesystems

On account creation, a new RCS HPC user is given ownership of a subdirectory created on each of the following major filesystems. The paths to each of these subdirectories are recorded in your shell's environment variables, making it easy to use these paths on the command line.

The major filesystems available on Chinook are typically referred to by the Bash syntax used to expand the corresponding environment variable. These names are used below.

The following protocols for transferring files are supported on Chinook:

* Secure Copy \(SCP\)
* SSH File Transfer Protocol \(SFTP\)
* rsync \(client-to-client only, no daemon\)

## $HOME  <a id="home"></a>

* The $HOME filesystem is accessible from the Chinook login and compute nodes, and bigdipper.rcs.alaska.edu.
* Default $HOME quota: 10 GB
* The $HOME filesystem is backed up regularly.

## $CENTER1  <a id="center"></a>

* **$CENTER1 is a scratch storage space and is not backed up.** For long term storage please copy your files off of $CENTER1.
* The $CENTER1 scratch filesystem is accessible from the Chinook login and compute nodes, and bigdipper.rcs.alaska.edu.
* The path to user directories on $CENTER1 is /center1/PROJECTID/UAusername
* Files are no longer purged on $CENTER1, but project quotas are in effect.
* Default $CENTER1 quotas are set to 1 TB **per project**. All project users share this quota.
* For information on getting better IO performance using $CENTER, see our [Lustre Striping Guide](https://uaf-rcs.gitbook.io/uaf-rcs-storage-docs/lustre_striping_guide).

## $ARCHIVE  <a id="archive"></a>

* The $ARCHIVE filesystem is accessible from the Chinook login nodes and bigdipper.rcs.alaska.edu.
* Files stored in $ARCHIVE will be written to tape and taken offline over time. Use the "batch\_stage" command to bring the files back online prior to viewing the contents of the file or copying the data off $ARCHIVE.
* To stage directories run "batch\_stage -r &lt;DIRECTORY&gt;". For more help and samples run "batch\_stage -h".
* If you have a legacy ARSC username, a symbolic link has been created linking your /archive/u1/uaf/ARSCusername directory to your /archive/u1/uaf/UAusername directory.

## Viewing Quotas  <a id="quotas"></a>

You can view your storage quotas and usage through the `show_storage` command. `show_storage`will show the quota and usage for $HOME, $ARCHIVE, and $CENTER1, if they are mounted on the machine that you are on.

```text
$ show_storage 
Filesystem   Used_GiB    Soft_GiB   Hard_GiB      Files  Soft Files Hard Files
========== ==========  ========== ========== ==========  ========== ==========
$HOME            0.00       10.00      11.00         16     1000000    1100000

===================================$CENTER1===================================
Project      Used_GiB    Soft_GiB   Hard_GiB      Files  Soft Files Hard Files
========== ==========  ========== ========== ==========  ========== ==========
RCSCLASS         0.25     1024.00    1126.40       1471           0          0
```

`show_storage` can also be used to determine how much usage is being consumed by each directory in the main project directory through the use of the `-d PROJECTID` flag. PROJECTID is the Unix group of a specific project. Depending on your usage, this command may take some time to complete.

```text
$ show_storage -d rcsclass
/import/c1/RCSCLASS      GiB
=================== ========
uaguest_rclass8         0.00
uaguest_rclass9         0.00
uaguest_rclass2         0.00
uaguest_rclass3         0.00
uaguest_rclass1         0.00
uaguest_rclass10        0.00
uaguest_rclass7         0.00
uaguest_rclass4         0.00
uaguest_rclass5         0.00
demos                   0.24
uaguest_rclass6         0.00
```

The `du` command can be used to display how much storage is being used by specific directories. `du -h /center1/PROJECTID/path/to/directory` will list the storage used by each directory in `/center1/PROJECTID/path/to/directory`

```text
$ du -h /center1/RCSCLASS/uaguest_rclass1
53K /center1/RCSCLASS/uaguest_rclass1/data
106K  /center1/RCSCLASS/uaguest_rclass1
```

`du -sh /center1/PROJECTID/path/to/directory` will sum up the total storage used by a directory.

```text
$ du -sh /center1/RCSCLASS/uaguest_rclass1/data
53K /center1/RCSCLASS/uaguest_rclass1/data
```

