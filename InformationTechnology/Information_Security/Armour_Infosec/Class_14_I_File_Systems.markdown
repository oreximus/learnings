# Class 14-I: File Systems

## Overview
This class compares Windows and Linux file systems and covers CentOS installation.

## Windows File System
- **Root**: `C:\`
- **Key Directories**:
  - **Program Files**: 64-bit application installations.
  - **Program Files (x86)**: 32-bit application installations.
  - **ProgramData**: Shared application data.
  - **Users**: User profiles and data.
  - **Windows**:
    - **System32**: Core system files.
    - **WinSxS**: Side-by-side component storage.
    - **Temp**: Temporary files.
    - **Logs**: System logs.
  - **Recycle Bin**: Deleted files storage.
  - **PerfLogs**: Performance logs.
  - **pagefile.sys, swapfile.sys**: Virtual memory files.
  - **DumpStack.log**: Crash logs.
- **Command**: `dir /a` (show all files, including hidden).

## Linux File System
- **Root**: `/`
- **Key Directories**:
  - **/bin**: Essential user binaries (e.g., `ls`, `cp`).
  - **/sbin**: System binaries (e.g., `init`, `fsck`).
  - **/lib, /lib64**: Libraries for binaries.
  - **/etc**: Configuration files.
  - **/dev**: Device files.
  - **/proc**: Kernel and process information.
  - **/var**: Variable data (e.g., logs).
  - **/tmp**: Temporary files.
  - **/usr**: User applications and libraries.
  - **/boot**: Bootloader files (e.g., GRUB).
  - **/opt**: Third-party software.
  - **/srv**: Service data.
  - **/home**: User home directories.
  - **/root**: Root user’s home directory.
  - **/mnt**: Mount points for devices.

## CentOS Installation
- **Partitioning**:
  - **/boot**: 1 GB for bootloader files.
  - **Swap**: 2x RAM (e.g., 4 GB for 8 GB RAM).
  - **/**: Root partition for remaining space.
- **Type**: Standard Partition (not LVM for simplicity).
- **Steps**:
  1. Select Standard Partition.
  2. Allocate 1 GB to `/boot`.
  3. Allocate swap space (e.g., 4 GB).
  4. Allocate remaining space to `/`.
  5. Complete installation.

## Corrections
- Clarified Windows file system directories and their purposes.
- Corrected swap space recommendation (2x RAM is a general guideline).