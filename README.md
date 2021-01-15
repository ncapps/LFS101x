# Notes from Introduction to Linux: LFS101x

## Notes
1. [Chapter 1: The Linux Foundation](ch01/README.md)
2. [Chapter 2: Linux Philosophy and Concepts](ch02/README.md)
3. [Chapter 3: Linux Basics and System Startup](ch03/README.md)

## Bring up a virtual machine
```sh

vagrant up # Starts a virtual machine

vagrant ssh # SSH into the machine
# Local project directory is available at /vagrant

# To enable graphical interface
export INSTALL_DESKTOP=true
vagrant reload
vagrant rdp

# Delete the machine
vagrant destroy
```
