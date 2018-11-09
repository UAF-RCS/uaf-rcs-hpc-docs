# Complier Toolchains

Compiler toolchains are modules that bundle together a set of compiler, MPI, and numerical library modules. To use a compiler toolchain, load the compiler toolchain module and all the submodules will be loaded. This will set variables such as PATH, CPATH, LIBRARY\_PATH, LD\_LIBRARY\_PATH, and others. Other variable conventions such as CC and CXX are not automatically defined.

Since Chinook is an Intel-based HPC cluster, RCS defaults to compiling software using Intel-based compiler toolchains.

| Toolchain Name | Version | Comprises |
| :--- | :--- | :--- |
| foss | 2016b | GNU Compiler Collection 5.4.0, Penguin-modified OpenMPI 1.10.2, OpenBLAS 0.2.18, FFTW 3.3.4, ScaLAPACK 2.0.2 |
| pic-intel | 2016b | Intel Compiler Collection 2016.3.210 \(2016 update 3\), Penguin-modified OpenMPI 1.10.6, Intel Math Kernel Library \(MKL\) 11.3.3.210 |

