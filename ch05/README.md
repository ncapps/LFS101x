# Chapter 5: System Configuration from the Graphical Interface

## Debian Packaging
- dpkg is the underlying package manager for these systems. It can install, remove, and build packages. Unlike higher-level package management systems, it does not automatically download and install packages and satisfy their dependencies.
- the higher-level package management system is the Advanced Package Tool (APT) system of utilities. Generally, while each distribution within the Debian family uses APT, it creates its own user interface on top of it (for example, apt, apt-get, aptitude, synaptic, Ubuntu Software Center, Update Manager, etc).

## Red Hat Package Manager (RPM)
- Red Hat Package Manager (RPM) is the other package management system popular on Linux distributions. It was developed by Red Hat, and adopted by a number of other distributions, including SUSE/penSUSE, Mageia, CentOS, Oracle Linux, and others.
- The higher-level package manager differs between distributions: Red Hat family distributions historically used the repository format used by yum , however, RHEL/CentOS 8 and Fedora have moved over to using dnf, which is mostly backwards compatible with yum.