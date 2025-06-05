# Class 16: Linux Commands and DHCP Deep Dive

## Linux Server Fundamentals

### SSH Connection
- **Purpose**: Secure remote access to Linux servers
- **Command**: `ssh username@server_ip`
- **Security**: Encrypted communication

### Basic System Information Commands

#### Kernel and System Info
\`\`\`bash
# Check kernel version
uname -r

# Check disk space
df -h

# Check hostname
hostname

# Check current working directory
pwd
\`\`\`

#### Help and Manual System
\`\`\`bash
# General help
help

# Manual pages for commands
man command_name

# Example: Manual for ls command
man ls
\`\`\`

### Network Configuration
- **Link-local IP**: Automatically assigned when no DHCP/static IP configured
- **Range**: 169.254.x.x (APIPA - Automatic Private IP Addressing)

### Terminal Prompt Information
\`\`\`bash
# Format: user@hostname:directory$
root@localhost:~#    # Root user (# symbol)
user@hostname:~$     # Normal user ($ symbol)

# Symbols meaning:
~ : User's home directory
$ : Normal user prompt
# : Root user prompt
\`\`\`

## File and Directory Operations

### Creating Files
\`\`\`bash
# Create empty file
touch filename

# Create file with spaces in name
touch "Armour Infosec"

# Create multiple files
touch file1 file2 file3
\`\`\`

### Viewing File Content
\`\`\`bash
# View file content
cat filename

# Add content to file
cat > filename
# Type content, then Ctrl+D to save

# Append content to file
cat >> filename
\`\`\`

### Directory Operations
\`\`\`bash
# Create single directory
mkdir directory_name

# Create multiple directories
mkdir dir1 dir2 dir3

# Create nested directories
mkdir -p parent/child/grandchild

# Remove empty directory
rmdir directory_name

# Remove nested empty directories
rmdir -p parent/child/grandchild
\`\`\`

### File Deletion
\`\`\`bash
# Delete file with confirmation
rm filename

# Delete file without confirmation
rm -f filename

# Delete with verbose output
rm -vf filename

# Delete files with wildcard pattern
rm -vf A*    # Delete all files starting with 'A'
\`\`\`

## DHCP Advanced Configuration

### DHCP Scope Management

#### 1. Create Scope
- **Scope Name**: Descriptive identifier
- **IP Range**: Start and end addresses
- **Subnet Mask**: Network boundary definition
- **Lease Duration**: IP address reservation time

#### 2. Configure Options
- **Router (Gateway)**: Network exit point
- **DNS Servers**: Name resolution servers
- **Domain Name**: Network domain suffix

#### 3. Activate Scope
- **Purpose**: Enable IP address distribution
- **Status**: Scope must be active to serve clients

### DHCP DORA Process Detailed

#### 1. Discover
- **Client Action**: Broadcasts DHCP Discover message
- **Destination**: 255.255.255.255 (broadcast)
- **Port**: Client uses port 68
- **Information**: Client MAC address, requested options

#### 2. Offer  
- **Server Action**: Responds with IP address offer
- **Source Port**: Server port 67
- **Contents**: Available IP, lease time, server identifier
- **Multiple Servers**: Client may receive multiple offers

#### 3. Request
- **Client Action**: Requests specific IP from chosen server
- **Broadcast**: Informs all servers of choice
- **Contents**: Server identifier, requested IP address

#### 4. Acknowledge
- **Server Action**: Confirms IP assignment
- **Lease Information**: Lease time, renewal time
- **Configuration**: Gateway, DNS, other options

### Wireshark Analysis
\`\`\`bash
# Filter DHCP traffic in Wireshark
udp.port == 67 or udp.port == 68

# DHCP packet types:
# 1 = DHCP Discover
# 2 = DHCP Offer  
# 3 = DHCP Request
# 5 = DHCP ACK
\`\`\`

### DHCP Lease Process
1. **50% of lease time**: Client attempts to renew with original server
2. **87.5% of lease time**: Client broadcasts renewal request
3. **100% of lease time**: Lease expires, client must restart process

### Common DHCP Issues
- **No DHCP Response**: Check server status and network connectivity
- **IP Conflicts**: Verify scope ranges don't overlap
- **Wrong Gateway**: Verify scope options configuration
- **DNS Issues**: Check DNS server configuration in scope options
\`\`\`
