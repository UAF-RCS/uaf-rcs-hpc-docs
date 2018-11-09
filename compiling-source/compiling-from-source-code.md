# Compiling from Source Code

Compiling C, C++, and Fortran code on Chinook is reasonably similar to how it is done on regular CentOS systems, with some important differences. This page will try to outline both areas, focusing mostly on the differences.

#### Available Compilers

The default compiler suite on Chinook is the [Intel Parallel Studio XE Composer Edition](https://software.intel.com/en-us/intel-parallel-studio-xe), providing `icc`, `icpc`, and `ifort`. Intel compilers are designed for best performance on Intel processors, which can be taken advantage of on Chinook.

The [GNU Compiler Collection](https://gcc.gnu.org/) is also available and maintained on Chinook, providing `gcc`, `g++`, and `gfortran`. GNU compiler compatibility is ubiquitous across free and open-source software projects, which includes much scientific software.

For docmentation on each of these compiler suites, please refer to the following:

* [https://software.intel.com/en-us/intel-parallel-studio-xe-support/documentation](https://software.intel.com/en-us/intel-parallel-studio-xe-support/documentation)
* [https://gcc.gnu.org/onlinedocs/](https://gcc.gnu.org/onlinedocs/)

#### Open-source Linear Algebra / FFT

The following free and open-source linear algebra and fast Fourier transform libraries have been built using GCC and are available for use:

* OpenBLAS \(includes LAPACK\)
* ScaLAPACK
* FFTW

#### Intel MKL

The [Intel Math Kernel Library \(MKL\)](https://software.intel.com/en-us/articles/intel-math-kernel-library-documentation/) is available for use on Chinook. MKL offers Intel-tuned versions of all of the above open-source libraries, effectively replacing them.

For more information on linking against MKL, see Intel's [MKL Linking Quick Start](https://software.intel.com/en-us/node/528511). Of particular note is the online [MKL Link Line Advisor](https://software.intel.com/en-us/articles/intel-mkl-link-line-advisor), which will generate appropriate link flag strings for your needs.

For more information on MKL itself, see Intel's [MKL documentation](https://software.intel.com/en-us/articles/intel-math-kernel-library-documentation/).

