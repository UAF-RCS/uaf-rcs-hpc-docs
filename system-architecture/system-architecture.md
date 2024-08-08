# System Architecture

### Physical Architecture

![](../.gitbook/assets/chinookarchitecture.png)

Chinook currently has five login nodes, with 2 connected to the upgraded environment and 3 to the old environment:

* chinook00.alaska.edu (old environment)
* chinook01.alaska.edu (old environment)
* chinook02.alaska.edu (old environment)
* chinook03.alaska.edu (new environment)
* chinook04.alaska.edu (new environment)

chinook.alaska.edu will point to one of the above login nodes.

All Chinook compute nodes are Intel Relion 1900 compute nodes with dual Intel Xeon E5-2690 v4 14-core processors \(28 cores per node\), and 128GB RAM, Relion XE1112 compute nodes with dual Intel Xeon Gold 6148 20-core processors (40 cores per node) and 192GB RAM or Relion XE1312-AIR compute nodes with dual Intel Xeon Gold 6442Y 24-core processors (48 cores per node) and 256GB RAM.

### Software Architecture <a id="software-architecture"></a>

Chinook currently runs the Rocky 8.7 operating system \(Linux kernel version 4.18\).

Recent versions of the Intel and GNU compiler collections, several different MPI implementations, and core math libraries are available on Chinook. For more details, please refer to the list of [third-party software](../third-party-software/third-party-software.md) maintained on Chinook.

