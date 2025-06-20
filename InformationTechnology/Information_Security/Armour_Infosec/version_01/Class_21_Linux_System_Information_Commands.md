# Class 21: Linux System Information Commands

## Overview

This class covers a wide range of Linux commands used to get information about the system, users, hardware, and network. It also introduces the concept of creating hard and soft links.

## 1. Creating Links with `ln`

In Linux, a link is a pointer to a file. There are two types:

#### Hard Links

* **Description**: A hard link is a direct pointer to the file's content (inode). It's like a mirror copy of the file. If the original file is deleted, the hard link and the file's content remain accessible.
* **Command**: `ln /path/to/original/file /path/to/hard_link`.

#### Soft Links (Symbolic Links)

* **Description**: A soft link is a pointer to the *path* of another file, similar to a shortcut in Windows. If the original file is deleted or moved, the soft link becomes broken and will fail.
* **Command**: `ln -s /path/to/original/file /path/to/soft_link`.

## 2. Paging Commands: `less` and `more`

These commands are used to view the content of large files one page at a time. `less` is more modern and feature-rich.

* **Usage**: `ls -l /etc | less`
* **Navigation**:
    * `Space bar` / `Page Down`: Move forward one page.
    * `Page Up`: Move back one page.
    * `Arrow keys`: Move up or down one line.
    * `q`: Quit.

## 3. User and System Identification

* **`id`**: Displays user identity (UID), group identity (GID), and the groups a user belongs to.
* **`whoami`**: Prints the username of the current user.
* **`who`**: Shows who is currently logged into the system. `who -a` provides detailed information.
* **`w`**: A combination of `who` and `uptime`, showing who is logged on and what they are doing.
* **`tty`**: Prints the filename of the terminal connected to standard input. `pts` stands for pseudo-terminal slave, used for remote connections like SSH.

## 4. Host and OS Information

* **`hostname`**: Displays the system's hostname.
    * `-i`: Shows the IP address associated with the hostname.
    * `-I`: Shows all configured network interface IP addresses.
* **`uname`**: Prints system information.
    * `-r`: Kernel release version.
    * `-mrs`: Machine type, kernel release, and kernel name.
* **`cat /etc/os-release`**: Shows detailed OS identification, including name and version.
* **`cat /etc/redhat-release`**: Specific command for Red Hat family OSes.

## 5. Hardware Information

* **`lscpu`**: Displays detailed information about the CPU architecture.
* **`lsusb`**: Lists all USB devices connected to the system.
* **`lspci`**: Lists all PCI devices.
* **`lsblk`**: Lists block devices (like hard drives and partitions).
* **`free -h`**: Shows memory usage (RAM and swap) in a human-readable format.
* **`dmidecode`**: Dumps a computer's DMI (SMBIOS) table contents in a human-readable format. `--type 17` shows memory device information.

## 6. Date and Time

* **`date`**: Displays the current system date and time.
* **`cal`**: Displays a calendar for the current month. `cal <month> <year>` shows a specific month.

## 7. Networking Commands

* **`ifconfig`** or **`ip a`**: Lists all network interfaces and their configuration (IP address, MAC address, etc.). `ip address` and `ip addr` are aliases for `ip a`.
* **`route -n`**: Displays the kernel's IP routing table.
* **`cat /etc/resolv.conf`**: Shows the DNS servers the system is configured to use.

## 8. Shutdown Commands

* **`shutdown -P now`** or **`shutdown -h now`**: Shut down and power off/halt the system immediately. `-P` is for power off, `-h` is for halt.
* **`shutdown -c`**: Cancel a pending shutdown.
* **`reboot`**: Restart the system.

