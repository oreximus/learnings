# Class 16: Linux Basic Commands and System Information

## Theory Section

### Linux Command Structure

- **Format**: command [options] [arguments]
- **Case Sensitivity**: Linux commands are case-sensitive
- **Help**: Most commands support --help option or man pages

### System Information Commands

#### Kernel and System Information

```bash
uname -r                    # Show kernel version
uname -a                    # Show all system information
uname -mrs                  # Show machine, release, and system info
```

#### Disk Space and Storage

```bash
df -h                       # Show disk space in human-readable format
du -h directory             # Show directory size
lsblk                       # List block devices
```

#### Hostname Information

```bash
hostname                    # Show current hostname
hostname -a                 # Show all hostnames
hostname -i                 # Show configured IP addresses
hostname -I                 # Show all IP addresses
```

### Terminal and User Information

#### Terminal Identification

```bash
tty                         # Show current terminal
# Output example: /dev/pts/1
```

**Terminal Types**:

- **tty**: Physical terminals (teletype)
- **pts**: Pseudo-terminal slave (virtual terminals)

#### User Identification

```bash
whoami                      # Show current username
id                          # Show user and group IDs
# Example output: uid=0(root) gid=0(root) groups=0(root)

who -a                      # Show all logged-in users with details
w                           # Show who is logged in and what they're doing
```

## Practical Section

### File Operations

#### Creating Files

```bash
touch filename              # Create empty file
touch "file with spaces"    # Create file with spaces in name
touch file1 file2 file3     # Create multiple files
```

#### Viewing File Contents

```bash
cat filename                # Display entire file content
cat file1 file2             # Display multiple files
cat > filename              # Create file and add content interactively
cat >> filename             # Append content to existing file
```

#### Directory Operations

```bash
mkdir directory             # Create single directory
mkdir dir1 dir2 dir3        # Create multiple directories
mkdir -p path/to/deep/dir   # Create directory structure recursively
```

#### Removing Files and Directories

```bash
rm filename                 # Remove file
rm -f filename              # Force remove without confirmation
rm -vf filename             # Verbose force remove
rm -rf directory            # Remove directory and contents recursively

rmdir directory             # Remove empty directory only
rmdir -p path/to/empty/dirs # Remove empty directory structure
```

#### Advanced File Operations

```bash
rm A*                       # Remove files starting with 'A'
rm -vf file[!1]            # Remove all files except 'file1'
ls {*.txt,*.pdf}           # List files with multiple patterns
```

### Hardware Information Commands

#### CPU Information

```bash
lscpu                       # Detailed CPU architecture information
cat /proc/cpuinfo          # Raw CPU information from kernel
nproc                      # Number of processing units available
```

#### Memory Information

```bash
free -h                     # Memory usage in human-readable format
cat /proc/meminfo          # Detailed memory information
dmidecode --type 17        # Physical memory module information
```

#### Storage and Hardware

```bash
lsblk                       # List block devices in tree format
lsusb                       # List USB devices
lspci                       # List PCI devices
lshw                        # List all hardware (comprehensive)
```

### Network Information Commands

#### Network Interfaces

```bash
ifconfig                    # Show network interfaces (traditional)
ifconfig -a                 # Show all interfaces including inactive
ip addr show                # Modern way to show network interfaces
ip a                        # Short form of ip addr show
```

#### Network Configuration

```bash
route -n                    # Show routing table (traditional)
ip route show               # Modern routing table display
cat /etc/resolv.conf        # DNS configuration file
```

### System Control Commands

#### Shutdown and Restart

```bash
shutdown -P now             # Power off immediately
shutdown -P +5              # Power off after 5 minutes
shutdown -h now             # Halt system immediately
shutdown -r now             # Restart immediately
shutdown -c                 # Cancel scheduled shutdown

# Alternative commands
poweroff                    # Power off system
reboot                      # Restart system
halt                        # Halt system
```

### Command History Management

#### History Commands

```bash
history                     # Show command history with line numbers
history -c                  # Clear current session history
cat ~/.bash_history         # View persistent bash history file

# Execute commands from history
!!                          # Run last command
!n                          # Run command number n from history
!string                     # Run last command starting with 'string'
!?string                    # Run last command containing 'string'
```

### Date and Time Commands

```bash
date                        # Show current date and time
cal                         # Show calendar for current month
cal 12 2025                # Show calendar for specific month/year
```

### Operating System Information

```bash
cat /etc/os-release         # Show detailed OS version information
cat /etc/redhat-release     # Show Red Hat family OS info (RHEL/CentOS)
lsb_release -a             # Show Linux Standard Base info (if available)
```

## Study Questions

1. What is the difference between tty and pts terminals?
2. How do you find detailed information about system hardware?
3. What are the different ways to create and remove files and directories?
4. How does command history help in system administration?

## Next Class Preview

- Advanced Linux commands and text processing
- File permissions and ownership
- Process management and system monitoring
- Network troubleshooting tools
