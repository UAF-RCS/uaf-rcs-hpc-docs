# Using the Software Stack

Chinook already has builds of many third-party software packages \([see below](https://www.gi.alaska.edu/research-computing-systems/hpc/chinook/third-party-software#install-list) for a listing\). There are often multiple builds of a particular software package - different versions, different compilers used to build the software, different compile-time flags, et cetera. To avoid conflicts between these many disparate package builds, Chinook employs an _environment module_ system you can use to load and unload different combinations of software packages into your environment.

#### What are Environment Modules? <a id="environment-modules"></a>

The environment modules found on Chinook \(often referred to simply as "modules"\) are Tcl script files that are used to update shell environment variables such as `PATH`, `MANPATH`, and `LD_LIBRARY_PATH`. These variables allow your shell to discover the particular application or library as specified by the module. Some environment modules set additional variables \(such as `PYTHONPATH` or `PERL5LIB`\), while others simply load a suite of other modules.

#### Common module commands

| Command | Result |
| :--- | :--- |
| `module avail` | list all available modules |
| `module avail` _`pkg`_ | list all available modules **beginning** with the string _pkg_ |
| `module load` _`pkg`_ | load a module named _pkg_ |
| `module swap` _`oldnew`_ | attempt to replace loaded module named _old_ with one named _new_ |
| `module unload` _`pkg`_ | unload a module named _pkg_ |
| `module list` | list all currently-loaded modules |
| `module purge` | unload all modules |
| `module show` _`pkg`_ | summarize environment changes made by module named _pkg_\(sometimes incomplete\) |

#### Searching for modules

Because `module avail` will search for the provided string only at the beginning of a module's fully-qualified name, it can be difficult to use `module avail` to search for modules nested in any kind of hierarchy. This is the case on Chinook - **modules are categorized, then named**. Here are some examples:

* `compiler/GCC/`_`version`_
* `devel/CMake/`_`version`_
* `math/GMP/`_`version`_

To find modules for GCC using a pure `module avail` command, you would need to run `module avail compiler/GCC`. This is difficult, because you must already know that the module is in the compiler category.

To make things more complicated, `module avail` is also case-sensitive. Running `module avail devel/cmake` will not find the module named `devel/CMake/`_`version`_.

#### Better module searching

One workaround for these impediments is to combine `module avail` output with `grep`'s full-text case-insensitive string matching ability. The example below additionally uses [Bash file descriptor redirection](http://mywiki.wooledge.org/BashSheet#Redirection) syntax to redirect stderr to stdout because `module avail` outputs to stderr.

```text

```

replacing _pkg_ with the string you are searching for.

RCS is currently evaluating [Lmod](https://www.tacc.utexas.edu/research-development/tacc-projects/lmod) as a replacement for Chinook's current environment modules framework. Lmod has many desirable features, including but not limited to a more user-friendly `module avail` behavior.

For more information on Chinook's module framework, please visit [http://modules.sourceforge.net/index.html](http://modules.sourceforge.net/index.html).  
  


