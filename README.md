# Notes from Introduction to Linux: LFS101x

## Notes
1. [Chapter 1: The Linux Foundation](ch01/README.md)
2. [Chapter 2: Linux Philosophy and Concepts](ch02/README.md)
3. [Chapter 3: Linux Basics and System Startup](ch03/README.md)
4. [Chapter 4: Graphical Interface](ch04/README.md)
5. [Chapter 5: System Configuration from the Graphical Interface](ch05/README.md)
6. [Chapter 6: Common Applications](ch06/README.md)
7. [Chapter 7: Command Line Operations](ch07/README.md)
8. [Chapter 8: Finding Linux Documentation](ch08/README.md)
9. [Chapter 9: Processes](ch09/README.md)
10. [Chapter 10: File Operations](ch10/README.md)
11. [Chapter 11: Text Editors](ch11/README.md)
12. [Chapter 12: User Environment](ch12/README.md)
13. [Chapter 13: Manipulating Text](ch13/README.md)
14. [Chapter 14: Network Operations](ch14/README.md)
15. [Chapter 15: The Bash Shell and Basic Scripting](ch15/README.md)
16. [Chapter 16: More on Bash Shell Scripting](ch16/README.md)

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
