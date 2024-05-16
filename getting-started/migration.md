# Migration Overview

The new Chinook environment is intended to be similar to the old Chinook environment with a newer operating system, Rocky Linux 8, as well as updated software packages. A newer module system, called Lmod, has replaced the old Tcl modules system, and newer 40 and 48-core nodes have been added to Chinook.

# Important Changes

* chinook03.alaska.edu and chinook04.alaska.edu are the login nodes.
* The [Lmod](https://lmod.readthedocs.io/en/latest/) module system has replaced Tcl Modules. Please see our [documentation](../third-party-software/lmod.md) for how it differs from the old module system
* Software packages have been updated or removed and the RCS [third party software installation policies](../third-party-software/third-party-software.md) have been updated. Please see [here](../third-party-software/maintained-software-packages.md) for our current list of maintained software
* Due to the variety of CPU processors on our nodes jobs may not run if they are using the 48-core nodes combined with the 40 or 28 core nodes.
** The behavior of this is that jobs will seem as if they have "stalled" and are running on 48-core and other nodes at the same time. 
** Software built with the Intel toolchain will work
** software built via Anaconda, the foss toolchain, or software that relies on the GCC suite of compilers will run into issues. To make sure that your job does not run into this issue add the "#SBATCH --constraint=Haswell|Broadwell|Skylake" sbatch directive to your scripts. Or sbatch command
