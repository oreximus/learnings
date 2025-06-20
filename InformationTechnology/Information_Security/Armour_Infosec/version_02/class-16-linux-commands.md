# Class 16: Linux Server Fundamentals and DHCP Configuration

## Theory Section - Linux Server Fundamentals

### Remote Server Access

- **SSH (Secure Shell)**: Primary method for remote Linux server access
- **Benefits**: Encrypted communication, secure authentication
- **Usage**: Command-line interface for server management

### Basic Linux Commands

#### System Information Commands

##### Kernel and System Information

```bash
uname -r                    # Show kernel version
uname -a                    # Show all system information
uname -mrs                  # Show machine, release, and system info
```

##### Disk Space and Storage

```bash
df -h                       # Show disk space in human-readable format
du -h directory             # Show directory size
lsblk                       # List block devices
```

##### Hostname Information

```bash
hostname                    # Show current hostname
hostname -a                 # Show all hostnames
hostname -i                 # Show configured IP addresses
hostname -I                 # Show all IP addresses
```

#### Terminal and User Information

##### Terminal Identification

```bash
tty                         # Show current terminal
# Output example: /dev/pts/1
```

**Terminal Types**:

- **tty**: Physical terminals (teletype)
- **pts**: Pseudo-terminal slave (virtual terminals)

##### User Identification

```bash
whoami                      # Show current username
id                          # Show user and group IDs
# Example output: uid=0(root) gid=0(root) groups=0(root)

who -a                      # Show all logged-in users with details
w                           # Show who is logged in and what they're doing
```

#### File Operations

##### Creating Files

```bash
touch filename              # Create empty file
touch "file with spaces"    # Create file with spaces in name
touch file1 file2 file3     # Create multiple files
```

##### Viewing File Contents

```bash
cat filename                # Display entire file content
cat file1 file2             # Display multiple files
cat > filename              # Create file and add content interactively
cat >> filename             # Append content to existing file
```

##### Directory Operations

```bash
mkdir directory             # Create single directory
mkdir dir1 dir2 dir3        # Create multiple directories
mkdir -p path/to/deep/dir   # Create directory structure recursively
```

##### Removing Files and Directories

```bash
rm filename                 # Remove file
rm -f filename              # Force remove without confirmation
rm -vf filename             # Verbose force remove
rm -rf directory            # Remove directory and contents recursively

rmdir directory             # Remove empty directory only
rmdir -p path/to/empty/dirs # Remove empty directory structure
```

##### Advanced File Operations

```bash
rm A*                       # Remove files starting with 'A'
rm -vf file[!1]            # Remove all files except 'file1'
ls {*.txt,*.pdf}           # List files with multiple patterns
```

## Theory Section - DHCP Configuration

### DHCP Server Configuration Options

#### Backup and Restore

- **Backup Options**: Create backups of DHCP configuration
- **Snap Series**: DHCP snapshots for quick recovery
- **Best Practice**: Regular backups before major changes

#### DHCP Policies

1. **Allow List**: Permit specific clients to receive IP addresses
2. **Deny List**: Block specific clients from receiving IP addresses
3. **Ignore**: Server ignores requests from specific clients

#### Policy Configuration

- **Condition-Based**: Policies based on client characteristics
- **MAC Address**: Filter by hardware address
- **Vendor Class**: Filter by device type
- **User Class**: Filter by user-defined criteria

### DHCP Scope Configuration

#### Exclusion Range

- **Purpose**: Exclude specific IP addresses from automatic assignment
- **Usage**: Reserve IPs for static assignment (servers, printers, network equipment)
- **Example**: Exclude 192.168.1.1-192.168.1.50 for static devices

#### Reservations

- **Purpose**: Always assign same IP to specific device
- **Method**: Bind IP address to MAC address
- **Usage**: Servers, printers, network equipment requiring consistent IPs
- **Configuration**: MAC address + desired IP address

#### Lease Duration

- **Purpose**: Control how long clients keep IP addresses
- **Considerations**:
  - Short leases: Better for dynamic environments
  - Long leases: Reduce DHCP traffic, better for stable environments
- **Default**: Usually 8 days for Windows DHCP

#### Scope Options

- **Purpose**: Provide additional network configuration to clients
- **Common Options**:
  - Default Gateway (Router)
  - DNS Servers
  - Domain Name
  - NTP Servers
  - WINS Servers

#### Server Options

- **Purpose**: Apply settings to all scopes on the server
- **Usage**: Global settings that apply to multiple scopes
- **Hierarchy**: Server options < Scope options < Reservation options

## Practical Section

### Linux Command Practice

#### File Creation and Manipulation

```bash
# Create files with different methods
touch example.txt
echo "Hello World" > greeting.txt
cat > story.txt << EOF
This is a story
with multiple lines
EOF
```

#### Directory Structure Creation

```bash
# Create complex directory structure
mkdir -p project/{src,docs,tests}/{main,backup}
tree project  # View the structure (if tree is installed)
```

#### File Pattern Matching

```bash
# Create test files
touch file1.txt file2.txt file3.pdf document.pdf

# List specific patterns
ls *.txt        # All .txt files
ls file[1-2]*   # file1 and file2 with any extension
ls {*.txt,*.pdf} # All .txt and .pdf files
```

### DHCP Server Setup

#### Windows DHCP Server Configuration

##### Installation Process

1. **Server Manager** → Add Roles and Features
2. **Role-based installation**
3. **Select DHCP Server role**
4. **Complete installation**
5. **Post-deployment configuration**

##### Scope Creation

```
Scope Name: Main Network
IP Range: 192.168.1.100 - 192.168.1.200
Subnet Mask: 255.255.255.0
Lease Duration: 8 days
Gateway: 192.168.1.1
DNS: 192.168.1.1, 8.8.8.8
```

##### Exclusions and Reservations

```
Exclusions: 192.168.1.1 - 192.168.1.99 (Static devices)
Reservations:
- Server01: MAC 00:11:22:33:44:55 → IP 192.168.1.10
- Printer01: MAC AA:BB:CC:DD:EE:FF → IP 192.168.1.20
```

#### DHCP Testing and Verification

##### Client Testing

```cmd
# Windows client
ipconfig /release       # Release current IP
ipconfig /renew         # Request new IP from DHCP
ipconfig /all           # Show detailed configuration
```

```bash
# Linux client
sudo dhclient -r eth0   # Release IP
sudo dhclient eth0     # Request new IP
ip addr show eth0       # Show interface configuration
```

##### Server Monitoring

- **DHCP Console**: Monitor active leases
- **Event Viewer**: Check DHCP service logs
- **Performance Monitor**: Track DHCP performance counters

### Network Information Commands

#### Linux Networking Commands

```bash
# Network interface information
ifconfig                # Show network interfaces (traditional)
ip addr show            # Show network interfaces (modern)
ip a                    # Short form of ip addr show

# Routing information
route -n                # Show routing table
ip route show           # Modern routing table display

# DNS configuration
cat /etc/resolv.conf    # Show DNS configuration

# Network connectivity testing
ping -c 4 8.8.8.8       # Ping with count limit
traceroute google.com   # Trace route to destination
```

#### System Resource Commands

```bash
# Memory information
free -h                 # Show memory usage in human-readable format

# CPU information
lscpu                   # Detailed CPU information
cat /proc/cpuinfo       # Raw CPU information

# Hardware information
lsusb                   # List USB devices
lspci                   # List PCI devices
dmidecode --type 17     # Memory module information
```

## Study Questions

1. What is the difference between tty and pts terminals?
2. How do DHCP exclusions differ from reservations?
3. What are the advantages of using SSH for server management?
4. How do you troubleshoot DHCP client connectivity issues?

## Next Class Preview

- Advanced Linux commands and text processing
- File permissions and ownership
- Process management and system monitoring
- Network troubleshooting tools
