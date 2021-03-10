# Chapter 18: Local Security Principles

## User Accounts
- The Linux kernel allows properly authenticated users to access files and applications
- For each user, the following seven fields are maintained in the `/etc/passwd` file

Field Name | Details | Remarks
--- | --- | ---
Username | User login name | Should be between 1 and 32 characters long
Password | User password (or the character x if the password is stored in the /etc/shadow file) in encrypted format | Is never shown in Linux when it is being typed; this stops prying eyes
User ID (UID) | Every user must have a user id (UID) | UID 0 is reserved for root user. UID's ranging from 1-99 are reserved for other predefined accounts. UID's ranging from 100-999 are reserved for system accounts and groups. Normal users have UID's of 1000 or greater.
Group ID (GID) | The primary Group ID (GID); Group Identification Number stored in the /etc/group file | Is covered in detail in the chapter on Processes
User Info | This field is optional and allows insertion of extra information about the user such as their name | For example: Rufus T. Firefly
Home Directory | The absolute path location of user's home directory | For example: /home/rtfirefly
Shell | The absolute location of a user's default shell | For example: /bin/bash

## Type of Accounts
Linux distinguishes between several account types in order to isolate processes and workloads. Linux has four types of accounts:
1. root
2. System
3. Normal
4. Network

## Operations Requiring root Privileges
- root privileges are required to perform operations such as:
    - Creating, removing and managing user accounts
    - Managing software packages
    - Removing or modifying system files
    - Restarting system services

## Comparing sudo and su
su | sudo
--- | ---
When elevating privilege, you need to enter the root password. Giving the root password to a normal user should never, ever be done. | When elevating privilege, you need to enter the user’s password and not the root password.
Once a user elevates to the root account using su, the user can do anything that the root user can do for as long as the user wants, without being asked again for a password. | Offers more features and is considered more secure and more configurable. Exactly what the user is allowed to do can be precisely controlled and limited. By default the user will either always have to keep giving their password to do further operations with sudo, or can avoid doing so for a configurable time interval.
The command has limited logging features. | The command has detailed logging features.

## sudo Features
- `sudo` has the ability to keep track of unsuccessful attempts at gaining root access.
- Users' authorization for using sudo is based on configuration information stored in the `/etc/sudoers` file and in the `/etc/sudoers.d` directory.
- `/etc/sudoers` contains a lot of documentation in it about how to customize.
- Most Linux distributions now prefer you add a file in the directory `/etc/sudoers.d` with a name the same as the user. This file contains the individual user's sudo configuration, and one should leave the master configuration file untouched except for changes that affect all users.
- You should edit any of these configuration files by using `visudo`, which ensures that only one person is editing the file at a time, has the proper permissions, and refuses to write out the file and exit if there are syntax errors in the changes made.
- By default, `sudo` commands and any failures are logged in `/var/log/auth.log` under the Debian distribution family, and in /`var/log/messages` and/or `/var/log/secure` on other systems

## Process Isolation
- More recent additional security mechanisms that limit risks include
    - **Control Groups (cgroups):** Allows system administrators to group processes and associate finite resources to each cgroup.
    - **Containers:** Makes it possible to run multiple isolated Linux systems (containers) on a single system by relying on cgroups.
    - **Virtualization:** Hardware is emulated in such a way that not only processes can be isolated, but entire systems are run simultaneously as isolated and insulated guests (virtual machines) on one physical host.

## Hardware Security Guidelines
- Lock down workstations and servers
- Protect your network links such that it cannot be accessed by people you do not trust
- Protect your keyboards where passwords are entered to ensure the keyboards cannot be tampered with
- Ensure a password protects the BIOS in such a way that the system cannot be booted with a live or rescue DVD or USB key

## Summary
- The root account has authority over the entire system.
- root privileges may be required for tasks, such as restarting services, manually installing packages and managing parts of the filesystem that are outside your home directory.
- In order to perform any privileged operations such as system-wide changes, you need to use either su or sudo.
- Calls to `sudo` trigger a lookup in the `/etc/sudoers` file, or in the `/etc/sudoers.d` directory, which first validates that the calling user is allowed to use sudo and that it is being used within permitted scope.
- One of the most powerful features of sudo is its ability to log unsuccessful attempts at gaining root access. By default, sudo commands and failures are logged in `/var/log/auth.log` under the Debian family and `/var/log/messages` in other distribution families.
- One process cannot access another process’ resources, even when that process is running with the same user privileges.
- Using the user credentials, the system verifies the authenticity and identity.
- The SHA-512 algorithm is typically used to encode passwords. They can be encrypted, but not decrypted.
- Pluggable Authentication Modules (PAM) can be configured to automatically verify that passwords created or modified using the `passwd` utility are strong enough (what is considered strong enough can also be configured).
- Your IT security policy should start with requirements on how to properly secure physical access to servers and workstations.
- Keeping your systems updated is an important step in avoiding security attacks.