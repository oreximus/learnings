# Class 14: Windows and Linux File Systems

## Windows File System Structure

### Accessing Hidden Files
- **Method 1**: Show hidden files and folders in File Explorer options
- **Method 2**: Show system hidden files in folder properties
- **Command**: `dir /a` (shows all files including hidden)

### Important Directories in C:\

#### Program Files
- **Purpose**: Contains installed 64-bit applications
- **Default Location**: C:\Program Files\
- **Architecture**: x64 applications

#### Program Files (x86)
- **Purpose**: Contains installed 32-bit applications  
- **Default Location**: C:\Program Files (x86)\
- **Architecture**: x86 applications

#### ProgramData
- **Purpose**: Application data shared across all users
- **Visibility**: Hidden by default
- **Contents**: Configuration files, shared data

#### Users
- **Purpose**: Contains user profiles
- **Structure**: Individual folders for each user account
- **Contents**: Documents, Desktop, Downloads, etc.

#### Windows Directory
- **System32**: Core Windows system files (64-bit)
- **SysWOW64**: 32-bit system files on 64-bit systems
- **WinSxS**: Windows Side-by-Side store
- **Temp**: Temporary system files
- **Logs**: System log files

#### Other Important Directories
- **Recovery**: System recovery files
- **System Volume Information**: System restore points
- **$Recycle.Bin**: Recycle bin storage
- **PerfLogs**: Performance monitoring logs
- **pagefile.sys**: Virtual memory file
- **swapfile.sys**: Swap file for Windows apps

## Linux File System Structure

### Root Directory (/)
- **Purpose**: Root of entire file system hierarchy
- **Contains**: All files and directories in the system
- **Significance**: Starting point for all paths

### Essential Directories

#### /bin
- **Purpose**: Essential user binaries (ls, cp, mv)
- **Usage**: Commands needed for booting and single-user mode
- **Access**: Available to all users

#### /sbin  
- **Purpose**: Essential system binaries (init, fsck, reboot)
- **Usage**: System administration commands
- **Access**: Typically for root user

#### /lib and /lib64
- **Purpose**: Libraries needed for /bin and /sbin binaries
- **lib64**: 64-bit specific libraries
- **Function**: Shared libraries and kernel modules

#### /etc
- **Purpose**: System-wide configuration files
- **Contents**: Startup scripts, service configurations
- **Examples**: /etc/passwd, /etc/fstab, /etc/hosts

#### /dev
- **Purpose**: Device files
- **Type**: Special files representing hardware devices
- **Examples**: /dev/sda (hard drive), /dev/tty (terminals)

#### /proc
- **Purpose**: Virtual filesystem for kernel and process information
- **Type**: Memory-based filesystem
- **Contents**: Real-time system information

#### /var
- **Purpose**: Variable data
- **Contents**: Logs, spool files, temporary files
- **Subdirectories**: /var/log, /var/tmp, /var/spool

#### /tmp
- **Purpose**: Temporary files
- **Cleanup**: Usually cleared on reboot
- **Permissions**: World-writable with sticky bit

#### /usr
- **Purpose**: Secondary hierarchy for user applications
- **Structure**: /usr/bin, /usr/lib, /usr/share
- **Contents**: User utilities and applications

#### /boot
- **Purpose**: Boot-related files
- **Contents**: Kernel images, GRUB configuration
- **Importance**: Critical for system startup

#### /opt
- **Purpose**: Optional software packages
- **Usage**: Third-party software installations
- **Structure**: Each package in separate subdirectory

#### /home
- **Purpose**: User home directories
- **Structure**: /home/username
- **Contents**: User files, personal configurations

#### /root
- **Purpose**: Root user's home directory
- **Location**: Separate from /home
- **Access**: Root user only

#### /mnt and /media
- **Purpose**: Mount points for temporary filesystems
- **/mnt**: Manual mount points
- **/media**: Automatic mount points (USB drives, etc.)

## CentOS Installation Partitioning

### Recommended Partition Scheme
1. **/boot**: 1 GB
   - Purpose: Boot files and kernel images
   - File system: ext4

2. **Swap**: 4 GB (for 8 GB RAM system)
   - Purpose: Virtual memory
   - Calculation: Usually 0.5x to 2x RAM size

3. **/**: Remaining space
   - Purpose: Root filesystem
   - File system: ext4 or xfs
   - Contains: All other directories

### Installation Steps
1. Choose "Standard Partition" installation
2. Create /boot partition (1 GB)
3. Create swap partition (4 GB)
4. Create root (/) partition (remaining space)
5. Click "Done" to proceed
\`\`\`
