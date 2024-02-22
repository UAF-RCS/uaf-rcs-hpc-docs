# Compiling from Source Code

Compiling C, C++, and Fortran code on Chinook is reasonably similar to how it is done on regular Linux systems, with some important differences. This page will try to outline both areas, focusing mostly on the differences.

#### Available Compilers

Two default compiler suites are available on Chinook, the Intel OneAPI and the GNU Compiler Collection.


The default compiler suites on Chinook are the [Intel oneAPI](https://www.intel.com/content/www/us/en/developer/tools/oneapi/overview.html) which provides the classic `icc`, `icpc`, and `ifort` compilers and the new `icx`, `icpx`, and `ifx` compilers 

The [GNU Compiler Collection](https://gcc.gnu.org/) is also available and maintained on Chinook, providing `gcc`, `g++`, and `gfortran`. GNU compiler compatibility is ubiquitous across free and open-source software projects, which includes much scientific software.

For documentation on each of these compiler suites, please refer to the following:

* [Intel oneAPI documentation](https://www.intel.com/content/www/us/en/developer/tools/oneapi/documentation.html#gs.5c11ya)
* [GCC Documentation/](https://gcc.gnu.org/onlinedocs/)

#### Open-source Linear Algebra / FFT

The following free and open-source linear algebra and fast Fourier transform libraries have been built using GCC and are available for use:

* OpenBLAS \(includes LAPACK\)
* ScaLAPACK
* FFTW

#### Intel MKL

The [Intel Math Kernel Library \(MKL\)](https://software.intel.com/en-us/articles/intel-math-kernel-library-documentation/) is available for use on Chinook. MKL offers Intel-tuned versions of all of the above open-source libraries, effectively replacing them.

For more information on linking against MKL, see Intel's [MKL Linking Quick Start](https://software.intel.com/en-us/node/528511). Of particular note is the online [MKL Link Line Advisor](https://software.intel.com/en-us/articles/intel-mkl-link-line-advisor), which will generate appropriate link flag strings for your needs.

For more information on MKL itself, see Intel's [MKL documentation](https://software.intel.com/en-us/articles/intel-math-kernel-library-documentation/).

