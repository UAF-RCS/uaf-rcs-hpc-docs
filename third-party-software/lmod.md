# Using the Software Stack

Chinook already has builds of many third-party software packages that are used by multiple projects on Chinook. There are often multiple builds of a particular software package - different versions, different compilers used to build the software, different compile-time flags, et cetera. To avoid conflicts between these many disparate package builds, Chinook employs the Lmod environment module system which you can use to load and unload different combinations of software packages into your environment.

### What are Environment Modules? <a id="environment-modules"></a>

We use the Lmod enviornment module system on Chinook for its expanded capabilities over the Tcl environment module system. 

The environment modules found on Chinook \(often referred to simply as "modules"\) are Lua script files that are used to update shell environment variables such as `PATH`, `MANPATH`, and `LD_LIBRARY_PATH`. These variables allow your shell to discover the particular application or library as specified by the module. Some environment modules set additional variables \(such as `PYTHONPATH` or `PERL5LIB`\), while others simply load a suite of other modules.

### Toolchains <a id="toolchains"></a>

Software on chinook is built using Toolchains, which are a selection of compilers and various software, such as MPI or BLAS, that are commonly needed for software packages. Toolchains allow us to simplify our software builds and guarantees that modules that were built with the same toolchain will work together when both are loaded.

We use two toolchains to build our software and generally try to build all software using both. These toolchains are the foss (Free Open Source Software) and intel.

####

### Common commands and loading modules

* module list - will show the current modules you have loaded
* module load moduleName/version - will load a module named moduleName, at a specific version
* module unload moduleName/version - will unload a module
* module avail (or module av) - show all available modules to load, based on the modules you have loaded
* module spider moduleName - search for a specific moduleName. The output will list what needs to be loaded to be able to load the module you searched for
* module keyword - search all modules for a specific keyword

Loading modules will only be active for the current session you are in. Each time you log into Chinook you will need to reload any modules. If you wish to avoid this you can add any module commands to your .bashrc.

You should also reload any modules in batch scripts you submit to Slurm.

#### Hierarchical Naming Scheme <a id="hierarchical-naming-scheme"></a>

Note: If you just wish to see the maximum amount of modules for our two main toolchains (intel and foss/GNU) you should run the following commands:

```
module load intel/2022a
module avail
```

or

```
module load foss/2022a
module avail
```

Our current module setup uses a Hierarchical Naming Scheme for loading modules. Modules are presented in a hierarchy of different levels, starting from a top "core" level (typically compilers and other system software) then going to a "compiler" level (for software build with a specific compiler toolchain), followed by an "MPI" level (software build with a specific compiler + MPI toolchain).

Each level will act as a "gateway" to the next level down, meaning you must load a compiler module at the "core" level to see modules at the "compiler" level with the "module avail" command.

If you wish to see the maximum amount of modules available for the GCC suite of compilers you can run:

module load foss/2022a

or for the Intel suite of compilers:

module load intel/2022a

and "module avail" will show all available modules build using the GCC or Intel compilers.

With no modules loaded:

```
module avail
---------------------------- /usr/share/modulefiles ----------------------------
   pmi/pmix-x86_64    slurm/22.05.4

---------------------- /usr/local/modules/easybuild/Core -----------------------
   Bison/3.8.2            M4/1.4.19            flex/2.6.4      ncurses/6.2
   CUDA/11.7.0            OpenSSL/1.1          foss/2022a      pkgconf/1.8.0
   GCC/11.3.0             binutils/2.38        gettext/0.21    zlib/1.2.12
   GCCcore/11.3.0         binutils/2.40 (D)    gompi/2022a
   Java/11.0.16   (11)    bzip2/1.0.8          intel/2022a
```

After loading the foss toolchain:
```
module load foss/2022a
module avail
---------- /usr/local/modules/easybuild/MPI/GCC/11.3.0/OpenMPI/4.1.4 -----------
   AUGUSTUS/3.5.0          RMBlast/2.13.0
   BLAST+/2.13.0           RepeatMasker/4.1.4
   Boost.MPI/1.79.0        ScaLAPACK/2.2.0-fb             (L)
   CDO/2.0.5               SciPy-bundle/2022.05
   ESMF/8.3.0              SuiteSparse/5.13.0-METIS-5.1.0
   FFTW.MPI/3.3.10  (L)    ecCodes/2.24.2
   GDAL/3.5.0              h5py/3.7.0
   HDF5/1.13.1             mpi4py/3.1.4
   HMMER/3.3.2             ncview/2.1.8
   MAKER/3.01.04           netCDF-C++4/4.3.1
   NCO/5.0.3               netCDF-Fortran/4.5.4
   R/4.2.2                 netCDF/4.9.0

--------------- /usr/local/modules/easybuild/Compiler/GCC/11.3.0 ---------------
   BCFtools/1.17      FFTW/3.3.10     (L)    OpenBLAS/0.3.20   (L
)
   BLIS/0.9.0         FlexiBLAS/3.2.0 (L)    OpenMPI/4.1.4     (L
)
...
```
