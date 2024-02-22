# Complier Toolchains

Compiler toolchains are modules that bundle together a set of compiler, MPI, and numerical library modules. To use a compiler toolchain, load the compiler toolchain module and all the submodules will be loaded. This will set variables such as PATH, CPATH, LIBRARY\_PATH, LD\_LIBRARY\_PATH, and others. Other variable conventions such as CC and CXX are not automatically defined.

RCS defaults to a best effort attempt to install software for both the FOSS (Free Open Source Software) and Intel toolchains.

Two MPI libraries are provided, OpenMPI for the foss toolchain and Intel MPI for the intel toolchain.

| Toolchain Name | Version | Comprises |
| :--- | :--- | :--- |
| foss | 2022a | GCCcore 11.3.0, OpenMPI 4.1.4, OpenBLAS 0.3.20, FFTW 3.3.10, ScaLAPACK 2.2.0 |
| intel | 2023a | GCCcore 12.3.0, Intel MPI 2021.9.0, Intel Math Kernel Library 2023.1.0 |