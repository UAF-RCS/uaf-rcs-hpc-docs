# Available Filesystems

On account creation, a new RCS HPC user is given ownership of a subdirectory created on each of the following major filesystems. The paths to each of these subdirectories are recorded in your shell's environment variables, making it easy to use these paths on the command line.

The major filesystems available on Chinook are typically referred to by the Bash syntax used to expand the corresponding environment variable. These names are $HOME, $CENTER1, and $ARCHIVE and are used below.

The following protocols for transferring files are supported on Chinook:

* Secure Copy \(SCP\)
* SSH File Transfer Protocol \(SFTP\)
* rsync \(client-to-client only, no daemon\)
* Globus

## $HOME  <a id="home"></a>

* The $HOME filesystem is accessible from the Chinook login and compute nodes, and bigdipper.alaska.edu.
* Default $HOME quota: 50 GB
* The $HOME filesystem is backed up regularly.

## $CENTER1  <a id="center"></a>

* **$CENTER1 is a scratch storage space and is not backed up.** For long term storage please copy your files off of $CENTER1.
* The $CENTER1 scratch filesystem is accessible from the Chinook login and compute nodes, and bigdipper.alaska.edu.
* The path to user directories on $CENTER1 is /center1/PROJECTID/UAusername
* Files are not purged on $CENTER1, but project quotas are in effect.
* Default $CENTER1 quotas are set to 1 TB **per project**. All project users share this quota.
* For information on getting better IO performance using $CENTER, see our [Lustre Striping Guide](https://uaf-rcs.gitbook.io/uaf-rcs-storage-docs/lustre_striping_guide).

## $ARCHIVE  <a id="archive"></a>

* The $ARCHIVE filesystem is accessible from the Chinook login nodes and bigdipper.alaska.edu.
* Files stored in $ARCHIVE will be written to tape and taken offline over time. Use the "batch\_stage" command to bring the files back online prior to viewing the contents of the file or copying the data off $ARCHIVE.
* To stage directories run "batch\_stage -r &lt;DIRECTORY&gt;". For more help and samples run "batch\_stage -h".

## Viewing Quotas  <a id="quotas"></a>

You can view your storage quotas and usage through the `show_storage` command. `show_storage` will show the quota and usage for $HOME, $ARCHIVE, and $CENTER1, if they are mounted on the machine that you are on.

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

In the `$HOME` and `$CENTER1` directories the `du` command can be used to display how much storage is being used by specific directories. `du -h /center1/PROJECTID/path/to/directory` will list the storage used by each directory in `/center1/PROJECTID/path/to/directory`

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

In the $ARCHIVE and $ONLINE directories you must use the `sdu` command. This command can be used to display how much storage is being used by specific directories. `sdu -h /archive/PROJECTID/path/to/directory` will list the storage used by each directory in `/archive/PROJECTID/path/to/directory`

```text
$ sudo sdu -h /archive/RCSCLASS/
4.0K	/archive/RCSCLASS/uaguest_rclass3
4.0K	/archive/RCSCLASS/uaguest_rclass10
4.0K	/archive/RCSCLASS/uaguest_rclass4
4.0K	/archive/RCSCLASS/uaguest_rclass5
4.0K	/archive/RCSCLASS/uaguest_rclass6
4.0K	/archive/RCSCLASS/uaguest_rclass7
152K	/archive/RCSCLASS/uaguest_rclass8/chinook_test
156K	/archive/RCSCLASS/uaguest_rclass8
4.0K	/archive/RCSCLASS/uaguest_rclass9
4.0K	/archive/RCSCLASS/uaguest_rclass1/Chinook_Test
156K	/archive/RCSCLASS/uaguest_rclass1
343K	/archive/RCSCLASS
```

`sdu -sh /archive/PROJECTID/path/to/directory` will sum up the total storage used by a directory.

```text
$ sdu -sh /archive/RCSCLASS/uaguest_rclass1
156K	/archive/RCSCLASS/uaguest_rclass1
```
