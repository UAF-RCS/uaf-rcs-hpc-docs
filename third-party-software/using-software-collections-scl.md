# Using Software Collections \(SCL\)

Software Collections, also known as SCLs, provide additional versions of system tools to be installed and used alongside the default version. This extends the lifetime and utility of the OS on chinook.

## Using an SCL

To run an executable from a particular SCL, type the following command at a shell prompt:

```text
$ scl enable software_collection... 'command...'
```

Or, alternatively, use the following:

```text
$ scl enable software_collection... -- command...
```

Replace "software\_collection" with a space-separated list of SCLs you want to use, and "command" with the command you want to run. For example, to start a session with python version 3.6.X:

```text
$ scl enable rh-python36 -- bash -l
```

When in an SCL session, the `exit` command will end the session. A second `exit` command will have to be executed to end the login session.

## Using an SCL in a SLURM Job

In order to use an SCL in a batch job, the job script either has to launch using `scl` to load the desired software, or the job script has to execute another script that does so. To launch a `bash` script \(including a job script\) that loads the python 3.6.X SCL, for example, put the following as the first line.

```text
#!/usr/bin/scl enable rh-python36 -- /bin/bash
```

Until the script exits, any python commands or scripts will then be executed using python 3.6.9 instead of the system default.

Alternately, individual commands, or scripts, can be executed using the `scl` command to load desired SCLs just for the duration of that command. For example, put the following in a job script to execute a python script using python 3.6.X instead of the system default version.

```text
/usr/bin/scl enable rh-python36 ./test.py
```

If you are passing command line arguments to your script you will need to enclose your script and command in double quots:

```text
/usr/bin/scl enable rh-python36 "./test.py -n arg1"
```

## More Information

`scl` usage information is available with the "-h" option.

`man scl` displays the man page.

[https://wiki.centos.org/AdditionalResources/Repositories/SCL](https://wiki.centos.org/AdditionalResources/Repositories/SCL)

