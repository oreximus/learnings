# Class 15: Windows and Linux File Systems

## Overview

This class compares the file system structures of Windows and Linux, highlighting the key directories and their purposes in each operating system. It also includes a brief guide for partitioning during a CentOS installation.

## Windows File System

The Windows file system is organized around drive letters, with `C:` being the default root drive for the operating system. To see all system files, you must unhide both hidden files and protected operating system files.

* `dir /a` in Command Prompt lists all files, including hidden ones.

#### Key Folders in `C:\`

* **`Program Files`**: Default location for 64-bit installed applications.
* **`Program Files (x86)`**: Default location for 32-bit installed applications on a 64-bit system.
* **`Users`**: Contains a profile folder for each user, storing their personal files, application settings (`AppData`), and desktop.
* **`Windows`**: The core directory for the operating system.
    * **`System32`**: Contains essential system files, libraries (DLLs), and executables for the 64-bit OS.
    * **`WinSxs`** (Windows Side-by-Side): Stores multiple versions of DLLs to prevent conflicts (also known as "DLL Hell").
* **`ProgramData`**: Stores application data that is shared among all users.
* **`pagefile.sys`**: The virtual memory swap file.
* **`PerfLogs`**: Performance Logs.
* **`Recovery`**: Contains files for system recovery options.

---

## Linux File System Hierarchy

The Linux file system is a single hierarchical tree, starting from the root directory `/`.

#### Key Directories in `/`

* **`/`**: The root directory, the top of the file system tree.
* **`/bin`**: Essential user command binaries (e.g., `ls`, `cp`, `mv`) needed for booting and basic functionality.
* **`/sbin`**: Essential system binaries used for system administration (e.g., `reboot`, `fdisk`, `ifconfig`).
* **`/etc`**: System-wide configuration files and shell scripts.
* **`/dev`**: Device files that represent hardware devices (e.g., `/dev/sda` for the first hard disk).
* **`/proc`**: A virtual filesystem providing information about system processes and kernel status.
* **`/var`**: Variable data files, such as logs (`/var/log`), mail spools, and temporary files that are expected to grow in size.
* **`/tmp`**: Temporary files used by the system and users. Files are often deleted upon reboot.
* **`/home`**: Home directories for users, containing their personal files and user-specific configurations.
* **`/root`**: The home directory for the root user (superuser).
* **`/boot`**: Contains files needed for the boot process, including the Linux kernel and the GRUB bootloader.
* **`/lib`** & **`/lib64`**: Essential libraries needed by the binaries in `/bin` and `/sbin`.
* **`/usr`**: Secondary hierarchy for user data, containing the majority of user utilities and applications (`/usr/bin`, `/usr/lib`, `/usr/local`).
* **`/opt`**: Optional application software packages. Often used for third-party software that doesn't follow the standard file system hierarchy.
* **`/mnt`**: A temporary mount point for mounting filesystems.
* **`/srv`**: Site-specific data served by the system, such as data for web servers.

## CentOS Installation Partitioning

When performing a manual "Standard Partition" installation for a server:
1.  **/boot**: Create a partition for `/boot`. A size of **1 GB** is recommended.
2.  **swap**: Create a swap partition. A common rule of thumb is to make it 0.5x to 2x the amount of RAM. For 8 GB of RAM, a **4 GB** swap partition is a reasonable starting point.
3.  **/**: Allocate the remaining disk space to the root (`/`) partition.

