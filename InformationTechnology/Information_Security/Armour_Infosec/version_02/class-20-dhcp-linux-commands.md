# Class 20: DHCP Configuration and Linux Command Chaining

## Theory Section - DHCP Configuration

### DHCP Server Management Options

#### Backup and Restore Options

- **Backup Purpose**: Create snapshots of DHCP configuration
- **Snap Series**: DHCP snapshots and backup series for quick recovery
- **Best Practice**: Regular backups before configuration changes
- **Restore Process**: Quick recovery from known good configurations

#### DHCP Policies

1. **Allow List Policy**

   - **Purpose**: Permit specific clients to receive IP addresses
   - **Criteria**: Based on MAC address, vendor class, user class
   - **Usage**: Secure environments, controlled access

2. **Deny Policy**

   - **Purpose**: Block specific clients from receiving IP addresses
   - **Usage**: Security measure, problematic device isolation
   - **Implementation**: Blacklist approach

3. **Ignore Policy**
   - **Purpose**: DHCP server ignores requests from specific clients
   - **Difference from Deny**: No response sent (stealth mode)
   - **Usage**: Advanced security configurations

#### Policy Configuration Methods

- **Condition-Based Policies**: Configure based on client conditions
- **MAC Address Filtering**: Hardware-based identification
- **Vendor Class Identification**: Device type recognition
- **User Class Options**: Custom client classifications

### DHCP Scope Advanced Configuration

#### Exclusion Range Configuration

- **Purpose**: Exclude specific IP addresses from automatic assignment
- **Usage**: Reserve IPs for static assignment (servers, printers, network equipment)
- **Example**: Exclude 192.168.1.1-192.168.1.50 for infrastructure devices
- **Best Practice**: Document excluded ranges and their purposes

#### DHCP Reservations

- **Purpose**: Always assign the same IP to a specific device
- **Method**: Bind IP address to MAC address
- **Usage**: Servers, printers, network equipment requiring consistent IPs
- **Configuration**: MAC address + desired IP address mapping
- **Advantage**: Combines DHCP convenience with static IP reliability

#### Lease Duration Management

- **Purpose**: Control how long clients retain IP addresses
- **Short Leases**: Better for dynamic environments, more DHCP traffic
- **Long Leases**: Reduce network traffic, better for stable environments
- **Default Windows**: Usually 8 days
- **Considerations**: Network size, device mobility, IP pool size

#### Scope Options vs Server Options

- **Scope Options**: Apply to specific DHCP scope only
- **Server Options**: Apply to all scopes on the server
- **Hierarchy**: Server Options < Scope Options < Reservation Options
- **Common Options**: Gateway, DNS servers, domain name, NTP servers

### HTTP Windows Server Integration

- **HTTP Protocol**: Hypertext Transfer Protocol
- **Integration**: Web-based DHCP management interfaces
- **Remote Management**: Browser-based administration
- **Monitoring**: Web dashboards for DHCP statistics

## Theory Section - Linux Command Chaining

### Command Execution Methods

#### Sequential Command Execution (;)

```bash
ifconfig; date; ls
# Executes commands one after another regardless of success/failure
```

#### Conditional AND Execution (&&)

```bash
ifconfig && date && id
# Executes next command only if previous command succeeds
```

#### Conditional OR Execution (||)

```bash
ifconfig || date || id
# Executes next command only if previous command fails
```

### Background Process Management

#### Running Commands in Background

```bash
ping 8.8.8.8 &
# Runs command in background, returns control to shell
```

#### Background Process Control

```bash
jobs                    # Show background jobs
fg                      # Bring last background job to foreground
bg                      # Send stopped job to background
kill %1                 # Kill job number 1
```

#### Suppressing Output

```bash
ping 8.8.8.8 >/dev/null &
# Run in background without showing output on terminal
```

### Pipe Operations

#### Basic Pipe Concept

- **Purpose**: Take output of one command as input to another
- **Symbol**: | (pipe character)
- **Data Flow**: Command1 | Command2 | Command3

#### Pipe Examples

```bash
# Directory listing with pagination
ls -l /etc/ | less

# Sorting directory contents
ls -l /etc/ | sort

# Searching in file contents
cat /etc/passwd | grep root

# Counting lines in file
cat /etc/passwd | wc -l

# Process sorting by CPU usage
ps aux | sort -nrk 3

# Command chaining with pipes
cat /etc/passwd | grep "root" | sort | uniq
```

## Practical Section - DHCP Implementation

### Windows DHCP Server Configuration

#### Installation Process

1. **Server Manager** → Add Roles and Features
2. **Role-based installation**
3. **Select DHCP Server role**
4. **Complete installation with default settings**
5. **Post-deployment configuration**

#### DHCP Scope Creation

```
Scope Configuration:
Name: Main Office Network
Description: Primary network for office devices
IP Range: 192.168.1.100 - 192.168.1.200
Subnet Mask: 255.255.255.0
Lease Duration: 8 days
Default Gateway: 192.168.1.1
DNS Servers: 192.168.1.1, 8.8.8.8
Domain Name: company.local
```

#### Advanced DHCP Configuration

```
Exclusions:
192.168.1.1 - 192.168.1.99 (Infrastructure devices)

Reservations:
Server01: MAC 00:11:22:33:44:55 → IP 192.168.1.10
Printer01: MAC AA:BB:CC:DD:EE:FF → IP 192.168.1.20
Switch01: MAC BB:CC:DD:EE:FF:AA → IP 192.168.1.30

Policies:
Allow Policy: Only company devices (based on MAC OUI)
Deny Policy: Known problematic devices
```

### DHCP Testing and Verification

#### Client-Side Testing

```cmd
# Windows client commands
ipconfig /release       # Release current IP lease
ipconfig /renew         # Request new IP from DHCP
ipconfig /all           # Show detailed network configuration
```

```bash
# Linux client commands
sudo dhclient -r eth0   # Release IP lease
sudo dhclient eth0     # Request new IP lease
ip addr show eth0       # Show interface configuration
```

#### Server-Side Monitoring

- **DHCP Console**: Monitor active leases and statistics
- **Event Viewer**: Check DHCP service logs
- **Performance Monitor**: Track DHCP performance counters
- **Network Monitoring**: Wireshark for DHCP packet analysis

## Practical Section - Linux Command Examples

### Advanced Command Chaining

#### System Information Gathering

```bash
# Comprehensive system info
uname -a && cat /etc/os-release && free -h && df -h

# Network information chain
ifconfig && route -n && cat /etc/resolv.conf

# Process monitoring chain
ps aux | grep -v grep | sort -nrk 3 | head -10
```

#### File Processing Chains

```bash
# Find and process log files
find /var/log -name "*.log" | xargs grep -l "error" | head -5

# User account analysis
cat /etc/passwd | cut -d: -f1,3,6 | sort -t: -k2 -n

# Disk usage analysis
du -h /var/log/* | sort -hr | head -10
```

### Background Process Management

#### Long-Running Tasks

```bash
# Start backup in background
tar -czf backup.tar.gz /home/user/ &

# Monitor system resources
top &

# Network monitoring
ping -c 1000 8.8.8.8 > ping_results.txt &
```

#### Process Control Examples

```bash
# Start multiple background jobs
ping google.com &
ping yahoo.com &
ping microsoft.com &

# List all jobs
jobs

# Bring specific job to foreground
fg %2

# Kill specific background job
kill %1
```

### Text Processing with Pipes

#### Log Analysis

```bash
# Analyze web server logs
cat /var/log/apache2/access.log | grep "404" | wc -l

# Find most common IP addresses
cat /var/log/apache2/access.log | awk '{print $1}' | sort | uniq -c | sort -nr | head -10

# Error analysis
grep -i error /var/log/syslog | tail -20 | less
```

#### System Monitoring

```bash
# Memory usage by process
ps aux | sort -nrk 4 | head -10

# Network connections
netstat -tuln | grep LISTEN | sort

# Disk usage summary
df -h | grep -v tmpfs | sort -k5 -nr
```

### Practical Exercises

#### Exercise 1: DHCP Configuration

1. **Install DHCP Server Role**
2. **Create Scope**: 192.168.1.100-200
3. **Configure Exclusions**: 192.168.1.1-99
4. **Add Reservations**: For server and printer
5. **Test Client Configuration**

#### Exercise 2: Command Chaining Practice

```bash
# Create system report
echo "=== System Report ===" > system_report.txt
date >> system_report.txt
uname -a >> system_report.txt
free -h >> system_report.txt
df -h >> system_report.txt
ps aux | head -10 >> system_report.txt
```

#### Exercise 3: Background Process Management

```bash
# Start monitoring tasks
ping -c 100 8.8.8.8 > ping1.txt &
ping -c 100 1.1.1.1 > ping2.txt &
top -b -n 5 > top_output.txt &

# Monitor and control
jobs
wait  # Wait for all background jobs to complete
```

## Study Questions

1. What are the advantages of DHCP policies over simple IP assignment?
2. How do command chaining operators (;, &&, ||) differ in behavior?
3. When would you use background processes in system administration?
4. How do pipes enable complex text processing workflows?

## Next Class Preview

- DNS server types and configuration
- Advanced text processing with grep and sed
- System monitoring and log analysis
- Network troubleshooting techniques
