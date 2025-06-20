# Class 21: Advanced Linux Commands and DNS Server Types

## Theory Section - Advanced Linux Commands

### Creating Links in Linux

#### Hard Links

- **Definition**: Direct pointer to file content (inode)
- **Command**: `ln source_file hard_link_name`
- **Characteristics**:
  - Points directly to file data on disk
  - Survives original file deletion
  - Same inode number as original
  - Cannot cross filesystem boundaries
  - Cannot link to directories
  - Updates reflect in all hard links

```bash
ln /var/log/messages my_hard_link
```

#### Soft Links (Symbolic Links)

- **Definition**: Pointer to file path/name
- **Command**: `ln -s source_file soft_link_name`
- **Characteristics**:
  - Points to file path, not content
  - Breaks if original file is deleted
  - Can cross filesystem boundaries
  - Can link to directories
  - Different inode number
  - More flexible but less robust

```bash
ln -s /var/log/messages my_soft_link
```

### Text Viewing Commands

#### less Command

- **Purpose**: View file content page by page with advanced navigation
- **Navigation Controls**:
  - **Space bar**: Next page
  - **Page Up/Page Down**: Navigate pages
  - **Arrow keys**: Line-by-line movement
  - **q**: Quit viewer
  - **/pattern**: Search forward
  - **?pattern**: Search backward
  - **n**: Next search result
  - **N**: Previous search result

#### more Command

- **Purpose**: Basic page-by-page file viewing (older, less featured)
- **Navigation Controls**:
  - **Space bar**: Next page
  - **Enter**: Next line
  - **q**: Quit viewer

### User and System Identification

#### User Information Commands

```bash
id                          # Show user and group IDs
# Output: uid=0(root) gid=0(root) groups=0(root)

whoami                      # Show current username
who -a                      # Show all logged-in users with details
w                           # Show users and their current activities
```

#### Terminal Information

```bash
tty                         # Show current terminal device
# /dev/pts/1 = pseudo-terminal slave (SSH, terminal emulator)
# /dev/tty2 = physical terminal (console)
```

### System Information Commands

#### Hostname and Network

```bash
hostname                    # Show system hostname
hostname -a                 # Show all hostnames and aliases
hostname -i                 # Show IP addresses for hostname
hostname -I                 # Show all IP addresses assigned to host
```

#### System Details

```bash
uname -r                    # Show kernel version only
uname -mrs                  # Show machine, release, system info
uname -a                    # Show all system information
```

#### Date and Time

```bash
date                        # Show current date and time
cal                         # Show calendar for current month
cal 12 2025                # Show calendar for specific month/year
```

#### Operating System Information

```bash
cat /etc/os-release         # Show detailed OS version information
cat /etc/redhat-release     # Show Red Hat family OS info (RHEL/CentOS)
lsb_release -a             # Show Linux Standard Base info (if available)
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

## Theory Section - DNS Server Types

### DNS Server Categories

#### 1. Root Domain Servers

- **Quantity**: 13 root servers worldwide (A through M)
- **Function**: Provide information about TLD nameservers
- **Content**: Names and IP addresses of TLD nameservers
- **Management**: Various organizations (Verisign, NASA, etc.)
- **Redundancy**: Multiple instances per letter for reliability

#### 2. TLD (Top-Level Domain) Nameservers

- **Function**: Manage domain records for specific TLD
- **Storage**: Delegation information for domains within TLD
- **Content**: NS records pointing to authoritative nameservers
- **Examples**: .com servers, .org servers, country code servers

#### 3. Authoritative Nameservers

- **Function**: Hold actual DNS records for specific domains
- **Content**: A, AAAA, CNAME, MX, TXT, and other DNS records
- **Authority**: Final source of truth for domain information
- **Management**: Controlled by domain owners or their DNS providers

#### 4. Recursive (Caching) DNS Servers

- **Function**: Perform full DNS resolution on behalf of clients
- **Process**: Query root → TLD → authoritative servers
- **Caching**: Store results to improve performance
- **Examples**: ISP DNS servers, Google (8.8.8.8), Cloudflare (1.1.1.1)

#### 5. Forwarding DNS Servers

- **Function**: Forward DNS queries to other DNS servers
- **Configuration**: Configured with specific upstream servers
- **Usage**: Corporate networks, filtered DNS services
- **Benefits**: Centralized control, caching, filtering

### DNS Resolution Process

#### Complete DNS Query Flow

1. **Browser Cache**: Check local browser DNS cache
2. **OS Cache**: Check operating system DNS cache
3. **Hosts File**: Check local hosts file (/etc/hosts or C:\Windows\System32\drivers\etc\hosts)
4. **Recursive DNS Server**: Query configured DNS server (ISP or public)
5. **Root Server Query**: Recursive server queries root servers
6. **TLD Server Query**: Query appropriate TLD servers
7. **Authoritative Server Query**: Query domain's authoritative servers
8. **Response Chain**: Answer travels back through the chain

## Practical Section

### Advanced Command Chaining

#### Multiple Command Execution

```bash
# Sequential execution (regardless of success/failure)
ifconfig; date; ls

# Conditional AND execution (stop on failure)
ifconfig && date && id

# Conditional OR execution (continue until success)
command1 || command2 || command3
```

#### Background Process Management

```bash
# Run command in background
ping 8.8.8.8 &

# Run without terminal output
ping 8.8.8.8 >/dev/null &

# Manage background jobs
jobs                        # List background jobs
fg                          # Bring last job to foreground
bg                          # Send stopped job to background
kill %1                     # Kill job number 1
```

### Pipe Operations

#### Basic Pipe Usage

```bash
# Directory listing with pagination
ls -l /etc/ | less

# Sort directory contents
ls -l /etc/ | sort

# Search in command output
ps aux | grep apache

# Count lines in file
cat /etc/passwd | wc -l
```

#### Advanced Pipe Chains

```bash
# Complex text processing
cat /etc/passwd | grep "root" | sort | uniq

# Process analysis
ps aux | sort -nrk 3 | head -10

# Log analysis
cat /var/log/syslog | grep error | tail -20 | less

# Network analysis
netstat -tuln | grep LISTEN | sort
```

### DNS Server Configuration Examples

#### Windows DNS Server Configuration

```
Primary DNS Zone Configuration:
Zone Name: company.local
Zone Type: Primary
Dynamic Updates: Secure only
Aging/Scavenging: Enabled

Forwarders Configuration:
Primary: 8.8.8.8
Secondary: 1.1.1.1
Timeout: 5 seconds
```

#### Linux BIND DNS Server Configuration

```bash
# /etc/named.conf example
options {
    directory "/var/named";
    forwarders { 8.8.8.8; 1.1.1.1; };
    recursion yes;
    allow-query { any; };
};

zone "company.local" IN {
    type master;
    file "company.local.zone";
    allow-update { none; };
};
```

### Practical Exercises

#### Exercise 1: Link Testing

```bash
# Create test environment
mkdir link_test && cd link_test

# Create original file
echo "Original content" > original.txt

# Create hard and soft links
ln original.txt hard_link.txt
ln -s original.txt soft_link.txt

# Test link behavior
ls -li  # Check inode numbers
rm original.txt
cat hard_link.txt    # Should work
cat soft_link.txt    # Should fail
```

#### Exercise 2: System Information Script

```bash
#!/bin/bash
# System information gathering script

echo "=== System Information Report ==="
echo "Generated on: $(date)"
echo
echo "Hostname: $(hostname)"
echo "OS: $(cat /etc/os-release | grep PRETTY_NAME | cut -d'"' -f2)"
echo "Kernel: $(uname -r)"
echo "Uptime: $(uptime -p)"
echo
echo "=== Hardware Information ==="
echo "CPU: $(lscpu | grep 'Model name' | cut -d':' -f2 | xargs)"
echo "Memory: $(free -h | grep Mem | awk '{print $2}')"
echo "Disk: $(df -h / | tail -1 | awk '{print $2}')"
echo
echo "=== Network Information ==="
ip addr show | grep -E "inet.*global" | awk '{print $2}' | head -5
```

#### Exercise 3: DNS Testing

```bash
# DNS resolution testing script
#!/bin/bash

domains=("google.com" "cloudflare.com" "github.com")
dns_servers=("8.8.8.8" "1.1.1.1" "9.9.9.9")

for domain in "${domains[@]}"; do
    echo "Testing $domain:"
    for dns in "${dns_servers[@]}"; do
        result=$(nslookup $domain $dns 2>/dev/null | grep "Address:" | tail -1 | awk '{print $2}')
        echo "  $dns: $result"
    done
    echo
done
```

## Study Questions

1. What are the practical differences between hard links and soft links?
2. How do different types of DNS servers work together in the resolution process?
3. What are the advantages of using command pipes for text processing?
4. How can background processes improve system administration efficiency?

## Next Class Preview

- Advanced text processing with grep and regular expressions
- DNS record management and troubleshooting
- System monitoring and log analysis
- Network diagnostic tools and techniques
