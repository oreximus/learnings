# Class 17: Advanced Linux Commands and Text Processing

## Theory Section

### File Linking in Linux

#### Hard Links

- **Definition**: Direct pointer to file content (inode)
- **Characteristics**:
  - Points directly to file data on disk
  - Survives original file deletion
  - Same inode number as original file
  - Cannot cross filesystem boundaries
  - Cannot link to directories

```bash
ln /var/log/messages my_hard_link
```

#### Soft Links (Symbolic Links)

- **Definition**: Pointer to file path/name
- **Characteristics**:
  - Points to file path, not content
  - Breaks if original file is deleted
  - Can cross filesystem boundaries
  - Can link to directories
  - Different inode number

```bash
ln -s /var/log/messages my_soft_link
```

#### Link Comparison

| Feature           | Hard Link            | Soft Link |
| ----------------- | -------------------- | --------- |
| Points to         | File content (inode) | File path |
| Survives deletion | Yes                  | No        |
| Cross filesystems | No                   | Yes       |
| Link directories  | No                   | Yes       |
| Disk space        | None                 | Minimal   |

### Text Viewing Commands

#### less Command

- **Purpose**: View file content page by page
- **Navigation**:
  - Space bar: Next page
  - Page Up/Page Down: Navigate pages
  - Arrow keys: Line by line navigation
  - q: Quit
  - /pattern: Search forward
  - ?pattern: Search backward

#### more Command

- **Purpose**: View file content page by page (older, less featured)
- **Navigation**:
  - Space bar: Next page
  - Enter: Next line
  - q: Quit

### User and System Identification

#### User Information Commands

```bash
id                      # Show user and group IDs
# Output: uid=0(root) gid=0(root) groups=0(root)

whoami                  # Show current username
who -a                  # Show all logged-in users with details
w                       # Show users and their activities
```

#### Terminal Information

```bash
tty                     # Show current terminal device
# Output: /dev/pts/1 (pseudo-terminal)
# Output: /dev/tty2 (physical terminal)
```

### System Information Commands

#### Hostname Commands

```bash
hostname                # Show system hostname
hostname -a             # Show all hostnames and aliases
hostname -i             # Show IP addresses for hostname
hostname -I             # Show all IP addresses
```

#### System Details

```bash
uname -r                # Show kernel version
uname -mrs              # Show machine, release, system info
uname -a                # Show all system information
```

#### Date and Time

```bash
date                    # Show current date and time
cal                     # Show calendar for current month
cal 12 2025            # Show calendar for December 2025
```

#### OS Information

```bash
cat /etc/os-release     # Show OS version information
cat /etc/redhat-release # Show Red Hat family OS info (RHEL/CentOS)
```

## Practical Section

### Hardware Information Commands

#### CPU Information

```bash
lscpu                   # Detailed CPU information
cat /proc/cpuinfo       # Raw CPU information from kernel
```

#### Memory Information

```bash
free -h                 # Memory usage in human-readable format
dmidecode --type 17     # Physical memory module information
cat /proc/meminfo       # Detailed memory information
```

#### Storage Information

```bash
lsblk                   # List block devices in tree format
df -h                   # Disk space usage
du -h /path             # Directory space usage
```

#### Hardware Devices

```bash
lsusb                   # List USB devices
lspci                   # List PCI devices
lshw                    # List all hardware (if installed)
```

### Network Information Commands

#### Network Interfaces

```bash
ifconfig                # Show network interfaces (traditional)
ifconfig -a             # Show all interfaces including inactive
ip addr show            # Modern way to show interfaces
ip a                    # Short form
```

#### Network Configuration

```bash
route -n                # Show routing table
ip route show           # Modern routing table
cat /etc/resolv.conf    # DNS configuration
```

### Command History Management

#### History Commands

```bash
history                 # Show command history
history -c              # Clear current session history
cat ~/.bash_history     # View bash history file

# Execute commands from history
!!                      # Run last command
!2                      # Run command number 2 from history
!if                     # Run last command starting with 'if'
!cat                    # Run last command starting with 'cat'
```

### System Control Commands

#### Shutdown Commands

```bash
shutdown -P now         # Power off immediately
shutdown -P             # Power off after 1 minute
shutdown -h now         # Halt system immediately
shutdown -r now         # Restart immediately
shutdown -c             # Cancel scheduled shutdown

# Alternative commands
poweroff                # Power off system
reboot                  # Restart system
halt                    # Halt system
```

### Advanced File Operations

#### Pattern Matching with rm

```bash
rm A*                   # Remove files starting with 'A'
rm -vf file[!1]        # Remove all files except 'file1'
rm *.{txt,pdf}         # Remove all .txt and .pdf files
```

#### File Listing with Patterns

```bash
ls {*.txt,*.pdf}       # List .txt and .pdf files
ls file[1-3]*          # List files starting with file1, file2, file3
ls *.{doc,docx}        # List Word documents
```

### Text Processing Examples

#### Creating and Viewing Files

```bash
# Create file with content
cat > example.txt << EOF
This is line 1
This is line 2
This is line 3
EOF

# View file with line numbers
cat -n example.txt

# View file with line numbers and end-of-line markers
cat -ne example.txt

# Remove multiple blank lines
cat -s file_with_blanks.txt
```

#### File Linking Examples

```bash
# Create original file
echo "Original content" > original.txt

# Create hard link
ln original.txt hard_link.txt

# Create soft link
ln -s original.txt soft_link.txt

# Check link information
ls -li original.txt hard_link.txt soft_link.txt

# Test link behavior
rm original.txt
cat hard_link.txt    # Still works
cat soft_link.txt    # Broken link
```

### System Monitoring Commands

#### Process Information

```bash
ps aux                  # Show all running processes
top                     # Real-time process viewer
htop                    # Enhanced process viewer (if installed)
```

#### System Load

```bash
uptime                  # System uptime and load average
w                       # Users and system load
```

#### Disk Usage

```bash
df -h                   # Filesystem disk usage
du -sh /path/*          # Directory sizes
iostat                  # I/O statistics (if installed)
```

### Practical Exercises

#### Exercise 1: System Information Gathering

```bash
# Create system info script
cat > sysinfo.sh << 'EOF'
#!/bin/bash
echo "=== System Information ==="
echo "Hostname: $(hostname)"
echo "OS: $(cat /etc/os-release | grep PRETTY_NAME | cut -d'"' -f2)"
echo "Kernel: $(uname -r)"
echo "Uptime: $(uptime -p)"
echo "Memory: $(free -h | grep Mem | awk '{print $3"/"$2}')"
echo "Disk Usage: $(df -h / | tail -1 | awk '{print $3"/"$2" ("$5")"}')"
EOF

chmod +x sysinfo.sh
./sysinfo.sh
```

#### Exercise 2: File Link Testing

```bash
# Create test environment
mkdir link_test
cd link_test

# Create original file
echo "Test content" > original.txt

# Create links
ln original.txt hard_link.txt
ln -s original.txt soft_link.txt

# Check inode numbers
ls -li

# Test deletion behavior
rm original.txt
echo "After deleting original:"
ls -l
cat hard_link.txt 2>/dev/null && echo "Hard link works" || echo "Hard link broken"
cat soft_link.txt 2>/dev/null && echo "Soft link works" || echo "Soft link broken"
```

## Study Questions

1. What happens to hard links and soft links when the original file is deleted?
2. How do you distinguish between physical terminals (tty) and pseudo-terminals (pts)?
3. What information can you gather about system hardware using Linux commands?
4. How does command history help in system administration?

## Next Class Preview

- Command chaining and pipes
- Background process management
- Text processing with grep and other tools
- System monitoring and process control
