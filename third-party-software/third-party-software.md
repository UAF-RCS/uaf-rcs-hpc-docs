# Third-Party Software

### Software requests

RCS evaluates [third-party software installation requests](https://www.gi.alaska.edu/research-computing-systems/software-request) for widely-used HPC software on a case-by-case basis. Some factors that affect request eligibility are:

* Applicability to multiple or large research groups
* Complexity of the installation process
* Software licensing

If a third-party software installation request is found to be a viable candidate for installation, RCS may elect to install the software through one of several means:

* RPM
* Binary \(pre-built\) distribution
* Source build

If an application or library is available through standard RPM repositories \(Penguin Computing, CentOS, EPEL, ...\) then the RPM may be installed. Users should test the installed software to determine if it meets requirements. If the RPM version does not meet needs, please contact RCS to have alternate installation methods evaluated.

Software that is not installed as an RPM will be installed in a publicly-available location and be accessible via Linux environment modules. If the software is built from source, then RCS will default to using the Intel compiler suite.

If an installation request does not meet our criteria, we will help researchers install it themselves via source, conda, or a container.

### Software Updates

RCS will evaluate software updates yearly, and based on multiple factors may update software packages. RCS will deprecate and hide old modules, keeping at most 3 versions of a software package on the system.