# Chapter 10: File Operations

## Filesystem Varieties
- Linux supports a number of native filesystem types, expressly created by Linux developers, such as: ext3, ext4, squashfs, btrfs.
- It also offers implementations of filesystems used on other alien operating systems, such as those from: Windows (ntfs, vfat), SGI (xfs), IBM (jfs), MacOS (hfs, hfs+).
- It is often the case that more than one filesystem type is used on a machine, based on considerations such as the size of files, how often they are modified, what kind of hardware they sit on and what kind of access speed is needed, etc.

## Linux Partitions
- Each filesystem on a Linux system occupies a disk partition. Partitions help to organize the contents of disks according to the kind and use of the data contained.
- For example, important programs required to run the system are often kept on a separate partition (known as root or /) than the one that contains files owned by regular users of that system (/home).
- Temporary files created and destroyed during the normal operation of Linux may be located on dedicated partitions. One advantage of this kind of isolation by type and variability is that when all available space on a particular partition is exhausted, the system may still operate normally.

## Mount Points
- Before you can start using a filesystem, you need to mount it on the filesystem tree at a mount point. This is simply a directory (which may or may not be empty) where the filesystem is to be grafted on.

## Mounting and Unmounting
- The `mount` command is used to attach a filesystem (which can be local to the computer or on a network) somewhere within the filesystem tree. The basic arguments are the device node and mount point.  For example,
```sh
# Attach the filesystem contained in the disk partition associated with the /dev/sda5 device node, into the filesystem tree at the /home mount point.
$ sudo mount /dev/sda5 /home

# Unmount the partition
$ sudo umount /home
```

- If you want it to be automatically available every time the system starts up, you need to edit `/etc/fstab` accordingly (the name is short for filesystem table).
- The system, however, will mount additional special filesystems required for normal operation, which are not enumerated in /etc/fstab .
```sh
# Display mounted filesystems
$ mount

# Display information about mounted filesystem
$ df -Th

$ cat /proc/mounts
```

## NFS and Network Filesystems
- Many system administrators mount remote users' home directories on a server in order to give them access to the same files and configuration files across multiple client systems.
- The most common such filesystem is named simply NFS (the Network Filesystem).

## Filesystem Architecture
- The `/bin` directory contains executable binaries, essential commands used to boot the system or in single-user mode, and essential commands required by all system users, such as `cat, cp, ls, mv, ps, and rm`.
- The `/sbin` directory is intended for essential binaries related to system administration, such as fsck and ip
- Commands that are not essential (theoretically) for the system to boot or operate in single-user mode are placed in the `/usr/bin` and `/usr/sbin` directories. Historically, this was done so `/usr` could be mounted as a separate filesystem that could be mounted at a later stage of system startup

- Certain filesystems, like the one mounted at `/proc`, are called pseudo-filesystems because they have no permanent presence anywhere on the disk.
- The `/proc` filesystem contains virtual files (files that exist only in memory) that permit viewing constantly changing kernel data
- The `/proc` filesystem is very useful because the information it reports is gathered only as needed and never needs storage on the disk.
```sh
# Some important entries in /proc are:
$ cat /proc/cpuinfo
$ cat /proc/interrupts
$ cat /proc/meminfo
$ cat /proc/mounts
$ cat /proc/partitions
$ cat /proc/version
```

- The `/dev` directory contains device nodes, a type of pseudo-file used by most hardware and software devices, except for network devices.

- The /var directory contains files that are expected to change in size and content as the system is running (var stands for variable), such as the entries in the following directories:
    - System log files: `/var/log`
    - Packages and database files: `/var/lib`
    - Print queues: `/var/spool`
    - Temporary files: `/var/tmp`

- The `/etc` directory is the home for system configuration files. It contains no binary programs, although there are some executable scripts
- For example, `/etc/resolv.conf` tells the system where to go on the network to obtain host name to IP address mappings (DNS).
- Note that `/etc` is for system-wide configuration files and only the superuser can modify files there. User-specific configuration files are always found under their home directory.

- The `/boot` directory contains the few essential files needed to boot the system. For every alternative kernel installed on the system there are four files:
    1. vmlinuz: The compressed Linux kernel, required for booting.
    2. initramfs: The initial ram filesystem, required for booting, sometimes called initrd, not initramfs.
    3. config: The kernel configuration file, only used for debugging and bookkeeping.
    4. System.map: Kernel symbol table, only used for debugging.
- The Grand Unified Bootloader (GRUB) files such as `/boot/grub/grub.conf` or `/boot/grub2/grub2.cfg` are also found under the `/boot` directory.

- `/lib` contains libraries (common code shared by applications and needed for them to run) for the essential programs in `/bin` and `/sbin`.
- These library filenames either start with `ld` or `lib`.


- The `/usr` directory tree contains theoretically non-essential programs and scripts (in the sense that they should not be needed to initially boot the system) and has at least the following sub-directories:

Directory Name | Usage
--- | ---
`/usr/include` | Header files used to compile applications
`/usr/lib` | Libraries for programs in /usr/bin and /usr/sbin
`/usr/lib64` | 64-bit libraries for 64-bit programs in /usr/bin and /usr/sbin
`/usr/sbin` | Non-essential system binaries, such as system daemons
`/usr/share` | Shared data used by applications, generally architecture-independent
`/usr/src` | Source code, usually for the Linux kernel
`/usr/local` | Data and programs specific to the local machine. Subdirectories include bin, sbin, lib, share, include, etc.
`/usr/bin` | This is the primary directory of executable commands on the system

## Comparing Files with diff
- `diff` is used to compare files and directories
- You can compare three files at once using `diff3`, which uses one file as the reference basis for the other two.
- A patch file contains the deltas (changes) required to update an older version of a file to the new one. The patch files are actually produced by running diff with the correct options, as in:
```sh
$ diff -Nur originalfile newfile > patchfile
# apply changes to an entire directory tree
$ patch -p1 < patchfile
# OR just one file
$ patch originalfile patchfile
```
- In Linux, one cannot assume that a file named file.txt is a text file and not an executable program
- The real nature of a file can be ascertained by using the `file` utility

## Backing Up Data
- `cp` can only copy files to and from destinations on the local machine (unless you are copying to or from a filesystem mounted using NFS)
- `rsync` can also be used to copy files from one machine to another. `rsync` is very efficient when recursively copying one directory tree to another, because only the differences are transmitted over the network
```sh
# recursively backup a directory
$ rsync -r project-X archive-machine:archives/project-X
# a good combination of options
$ rsync --progress -avrxH  --delete sourcedir destdir
```
- Linux uses a number of methods to compress data

Command | Usage
--- | ---
`gzip` | The most frequently used Linux compression utility
`bzip2` | Produces files significantly smaller than those produced by gzip
`xz` | The most space-efficient compression utility used in Linux
`zip` | Is often required to examine and decompress archives from other operating systems

- `gzip` is the most often used Linux compression utility.

Command | Usage
--- | ---
`gzip *` | Compresses all files in the current directory; each file is compressed and renamed with a .gz extension
`gzip -r projectX` | Compresses all files in the projectX directory, along with all files in all of the directories under projectX
`gunzip foo` | De-compresses foo found in the file foo.gz. Under the hood, the gunzip command is actually the same as gzip –d

- `xz` is the most space efficient compression utility used in Linux

Command | Usage
--- | ---
`xz *` | Compresses all of the files in the current directory and replaces each file with one with a .xz extension
`xz foo` | Compresses foo into foo.xz using the default compression level (-6), and removes foo if compression succeeds
`xz -dk bar.xz` | Decompresses bar.xz into bar and does not remove bar.xz even if decompression is successful
`xz -dcf a.txt b.txt.xz > abcd.txt` | Decompresses a mix of compressed and uncompressed files to standard output, using a single command
`xz -d *.xz` | Decompresses the files compressed using xz

- The `zip` program is not often used to compress files in Linux, but is often required to examine and decompress archives from other operating systems

Command | Usage
--- | ---
`zip backup *` | Compresses all files in the current directory and places them in the backup.zip
`zip -r backup.zip ~` | Archives your login directory (~) and all files and directories under it in backup.zip
`unzip backup.zip` | Extracts all files in backup.zip and places them in the current directory

- You can optionally compress while creating an archive with `tar`

Command | Usage
--- | ---
`tar xvf mydir.tar` | Extract all the files in mydir.tar into the mydir directory
`tar zcvf mydir.tar.gz mydir` | Create the archive and compress with gzip
`tar jcvf mydir.tar.bz2 mydir` | Create the archive and compress with bz2
`tar Jcvf mydir.tar.xz mydir` | Create the archive and compress with xz
`tar xvf mydir.tar.gz` | Extract all the files in mydir.tar.gz into the mydir directory. Note: You do not have to tell tar it is in gzip format

- The `dd` program is very useful for making copies of raw disk space

## Summary
- The filesystem tree starts at what is often called the root directory (or trunk, or /).
- The Filesystem Hierarchy Standard (FHS) provides Linux developers and system administrators a standard directory structure for the filesystem.
- Partitions help to segregate files according to usage, ownership, and type.
- Filesystems can be mounted anywhere on the main filesystem tree at a mount point. Automatic filesystem mounting can be set up by editing `/etc/fstab`.
- NFS (Network File System) is a useful method for sharing files and data through the network systems.
- Filesystems like `/proc` are called pseudo filesystems because they exist only in memory.
- `/root` (slash-root) is the home directory for the root user.
- `/var` may be put in its own filesystem so that growth can be contained and not fatally affect the system.
- `/boot` contains the basic files needed to boot the system.
- `patch` is a very useful tool in Linux. Many modifications to source code and configuration files are distributed with patch files, as they contain the deltas or changes to go from an old version of a file to the new version of a file.
- File extensions in Linux do not necessarily mean that a file is of a certain type.
- `cp` is used to copy files on the local machine, while `rsync` can also be used to copy files from one machine to another, as well as synchronize contents.
- `gzip`, `bzip2`, `xz` and `zip` are used to compress files.
- `tar` allows you to create or extract files from an archive file, often called a tarball. You can optionally compress while creating the archive, and decompress while extracting its contents.
- `dd` can be used to make large exact copies, even of entire disk partitions, efficiently.
