# Interactive Jobs

## Command Line Interactive Jobs  <a id="cmdline-inter"></a>

Interactive jobs are possible on Chinook using `srun`:

`chinook:~$ srun -p debug --nodes=1 --exclusive --pty /bin/bash`

The above command will reserve one node in the debug partition and launch an interactive shell job. The `--pty` option executes task zero in pseudo terminal mode and implicitly sets --unbuffered and --error and --output to /dev/null for all tasks except task zero, which may cause those tasks to exit immediately.

## Displaying X Windows from Interactive Jobs  <a id="window-inter"></a>

Slurm has an "x11" flag (**--x11**) that enables X11 forwarding over SSH, and displays application windows from a compute node back to the local display. Please make sure to [enable graphics when connecting to a Chinook login node](../getting-started/ssh.md#enabling-graphics). The flag can be used like so:

`chinook:~$ srun -p debug --nodes=1 --x11 --pty /bin/bash`

