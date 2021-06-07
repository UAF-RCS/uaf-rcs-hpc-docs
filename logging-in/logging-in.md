# Logging In

To log into Chinook, you will need a [user account](https://www.gi.alaska.edu/research-computing-systems/) \(under Services -> New Users\) and Secure Shell \(SSH\) client program.

Use the SSH client you have chosen and installed to connect to `chinook.alaska.edu`. When prompted for a username, either interactively or while configuring the client, you should provide your UA username. You will be prompted for a password upon opening an SSH connection. When this happens, enter your UA password.

The Chinook login nodes are intended to provide access to the cluster, to compile and modify applications and workflows, to manage data between the mounted filesystems, and to manage jobs. Any processing should be very limited and short to avoid impacting other users' activities. [Batch](../using-batch/using-the-batch-system.md) or [interactive](../using-batch/interactive-jobs.md) serial or parallel processing should take place on the compute nodes. RCS reserves the right to terminate user processes or sessions to maintain the normal working order of the login nodes and the cluster.

Chinook is a shared resource and users are asked to be neighborly to your fellow colleagues and students. Some helpful tips to keep in mind: 

* The login nodes are only to be used for compiling and modifying applications/workflows, managing data between the mounted filesystems and managing jobs
* Computationally intensive work is to be done on the [compute nodes](../using-batch/using-the-batch-system.md) or [Linux workstations](http://gi.alaska.edu/research-computing-systems/remote-login)
* Run code in the debug queue before submitting it to the small, standard, bio, or analysis partition to ensure that it works correctly and utilizes all the resources available to the job
* Jobs that are serial in nature or interactive, such as MATLAB, sholid be run in the bio or analysis partition to ensure maximum utilization of our limited resources
* Jobs submitted to the bio or analysis partition must include the amount of memory the job will use \(\#SBATCH --mem=&lt;size\[units\]&gt;\)
* Include a time limit in your batch scripts to help improve the performance of the scheduler in prioritizing jobs



