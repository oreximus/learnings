# Class 20: Advanced DHCP Configuration and Linux Commands

## DHCP Advanced Configuration Options

### DHCP Backup and Management

#### Backup Options
- **Full Backup**: Complete DHCP server configuration and database
- **Snap Series**: DHCP snapshots for point-in-time recovery
- **Automated Backup**: Scheduled backup operations
- **Database Export**: Export lease database for migration

### DHCP Policies and Access Control

#### 1. Allow List Policy
- **Purpose**: Explicitly permit specific devices
- **Method**: Based on MAC address or device identifier
- **Usage**: High-security environments
- **Configuration**: Add approved MAC addresses to allow list

#### 2. Deny Policy  
- **Purpose**: Block specific clients from receiving IP addresses
- **Method**: Prevent particular MAC addresses from getting DHCP leases
- **Usage**: Security policy enforcement
- **Application**: Block unauthorized or problematic devices

#### 3. Ignore Policy
- **Purpose**: DHCP server ignores specific client requests
- **Behavior**: Server acts as if it doesn't see the client
- **Difference from Deny**: Client receives no response (not even rejection)
- **Usage**: Stealth blocking of devices

### DHCP Policy Configuration

#### Condition-Based Policies
- **MAC Address**: Based on hardware address
- **Vendor Class**: Based on device type/manufacturer
- **User Class**: Based on user-defined classifications
- **Relay Agent**: Based on DHCP relay information

#### Policy Actions
- **Assign Specific Options**: Custom DNS, gateway, etc.
- **Assign to Specific Scope**: Direct to particular IP range
- **Apply Security Settings**: Enhanced security policies
- **Logging and Monitoring**: Special logging for policy matches

### DHCP Scope Advanced Options

#### Exclusion Range
- **Purpose**: Exclude specific IP addresses from automatic assignment
- **Usage**: Reserve IPs for static assignment
- **Example**: Exclude 192.168.1.1-192.168.1.10 for servers
- **Configuration**: Define start and end of excluded range

#### DHCP Reservations
- **Purpose**: Always assign same IP to same device
- **Method**: Based on MAC address
- **Usage**: Servers, printers, network devices
- **Benefits**: Consistent IP addressing for critical devices

#### Lease Duration Management
- **Short Leases**: 1-4 hours for high-turnover networks
- **Medium Leases**: 8-24 hours for typical networks  
- **Long Leases**: 7-30 days for stable networks
- **Considerations**: Balance between IP conservation and flexibility

### DHCP Options Hierarchy

#### Scope Options
- **Scope Level**: Apply to specific IP range only
- **Priority**: Override server options for that scope
- **Examples**: Different gateway per scope, scope-specific DNS

#### Server Options  
- **Server Level**: Apply to all scopes on the server
- **Usage**: When multiple scopes share common settings
- **Examples**: Company-wide DNS servers, NTP servers

## Advanced Linux Commands

### File Linking

#### Hard Links
\`\`\`bash
# Create hard link
ln /var/log/messages my_hard_link

# Characteristics:
# - Points directly to file content (inode)
# - Original file deletion doesn't affect hard link
# - Hard link becomes independent copy
# - Cannot cross filesystem boundaries
\`\`\`

#### Soft Links (Symbolic Links)
\`\`\`bash
# Create soft link
ln -s /var/log/messages my_soft_link

# Characteristics:
# - Points to file path
# - If original file deleted, soft link breaks
# - Can cross filesystem boundaries
# - Shows as link in file listings
\`\`\`

### File Viewing Commands

#### less Command
\`\`\`bash
# View large files with navigation
less /var/log/messages

# Navigation:
# Space: Next page
# b: Previous page  
# Arrow keys: Line by line
# q: Quit
# /search_term: Search within file
\`\`\`

#### more Command
\`\`\`bash
# Basic file viewing
more /var/log/messages

# Navigation:
# Space: Next page
# Enter: Next line
# q: Quit
\`\`\`

### System Identification Commands

#### User and Process Information
\`\`\`bash
# Show user and group information
id
# Output: uid=0(root) gid=0(root) groups=0(root)

# Show current terminal
tty
# Output: /dev/pts/1

# Show current username
whoami

# Show logged in users (detailed)
who -a

# Show logged in users with activity
w
\`\`\`

#### Host Information
\`\`\`bash
# Show hostname
hostname

# Show all hostname aliases
hostname -a

# Show IP addresses
hostname -i

# Show system information
uname -a    # All system information
uname -r    # Kernel version
uname -m    # Machine architecture
\`\`\`

#### Date and Time
\`\`\`bash
# Show calendar
cal
cal 12 2025    # Specific month and year

# Show current date and time
date

# Set date (root only)
date MMDDhhmmYYYY
\`\`\`

### System Information Commands

#### Operating System Information
\`\`\`bash
# OS release information
cat /etc/os-release

# Red Hat specific release info
cat /etc/redhat-release

# Kernel version
uname -r
\`\`\`

#### Hardware Information
\`\`\`bash
# CPU information
lscpu

# USB devices
lsusb

# PCI devices
lspci

# Block devices (storage)
lsblk

# Memory information
free -h

# Detailed memory information
cat /proc/meminfo
\`\`\`

#### Network Information
\`\`\`bash
# Network interfaces (traditional)
ifconfig

# Show all interfaces including inactive
ifconfig -a

# Modern network information
ip addr show    # or ip a

# Routing information
route -n
ip route show

# DNS configuration
cat /etc/resolv.conf
\`\`\`

### Command History Management

#### History Commands
\`\`\`bash
# Show command history
history

# View bash history file
cat ~/.bash_history

# Clear current session history
history -c

# Execute last command
!!

# Execute command by number
!123

# Execute last command starting with text
!ssh    # Last command starting with 'ssh'
\`\`\`

### System Control Commands

#### Shutdown Commands
\`\`\`bash
# Immediate shutdown and power off
shutdown -P now

# Shutdown after 1 minute (default)
shutdown -P

# Shutdown and halt
shutdown -h now

# Shutdown after specific time
shutdown -P +10    # Shutdown in 10 minutes

# Cancel scheduled shutdown
shutdown -c

# Immediate reboot
shutdown -r now
\`\`\`

### Command Execution Techniques

#### Multiple Commands
\`\`\`bash
# Sequential execution (always runs all)
command1; command2; command3

# Conditional execution (AND - stop on failure)
command1 && command2 && command3

# Conditional execution (OR - stop on success)
command1 || command2 || command3
\`\`\`

#### Background Processing
\`\`\`bash
# Run command in background
ping 8.8.8.8 &

# Bring background job to foreground
fg

# List background jobs
jobs

# Run command in background without output
ping 8.8.8.8 > /dev/null &
\`\`\`

#### Command Piping
\`\`\`bash
# Pipe output from one command to another
ls -l /etc/ | less
ls -l /etc/ | sort
cat /etc/passwd | grep root
cat /etc/passwd | wc -l    # Count lines

# Complex piping chain
cat /etc/passwd | grep "root" | sort | uniq
\`\`\`
