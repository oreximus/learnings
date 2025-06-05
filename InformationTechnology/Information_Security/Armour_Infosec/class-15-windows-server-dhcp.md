# Class 15: Windows Server and DHCP Configuration

## Linux Run Levels

### System Run Levels Overview
- **Run Level 0**: Halt/Shutdown
- **Run Level 1**: Single-user mode (rescue mode)
- **Run Level 2**: Multi-user mode without networking
- **Run Level 3**: Multi-user mode with networking (no GUI)
- **Run Level 4**: Unused (custom)
- **Run Level 5**: Multi-user mode with GUI
- **Run Level 6**: Reboot

### Checking Run Levels
\`\`\`bash
# Check current run level
runlevel

# Check system target (systemd)
systemctl get-default

# Set default target
systemctl set-default multi-user.target  # Run level 3
systemctl set-default graphical.target   # Run level 5
\`\`\`

## Windows Server DHCP Configuration

### DHCP Server Requirements
- **Unique Server**: Only one DHCP server per network segment
- **Lease Time**: Configuration for IP address reservation duration
- **Firewall**: Allow port 67 (DHCP server) and port 68 (DHCP client)
- **Gateway and DNS**: Must be configured for client functionality

### DHCP Installation Steps

#### 1. Install DHCP Role
1. Open **Server Manager**
2. Click **Add Roles and Features**
3. Select **Role-based or feature-based installation**
4. Choose target server
5. Select **DHCP Server** role
6. Add required features
7. Follow installation wizard
8. Restart server if prompted

#### 2. DHCP Configuration Files
- **Location**: `C:\Windows\System32\dhcp`
- **Purpose**: Contains DHCP server configuration and lease database

### DHCP Scope Configuration

#### Creating a Scope
1. **Scope Name**: Descriptive name for the IP range
2. **IP Range**: Starting and ending IP addresses
3. **Subnet Mask**: Network mask for the scope
4. **Lease Duration**: How long clients can keep IP addresses
5. **Gateway**: Default gateway for clients
6. **DNS Servers**: DNS server addresses for clients

#### Configuration Options
- **With Gateway**: Clients can access other networks
- **Without Gateway**: Clients limited to local network only
- **Activation**: Scope must be activated to serve clients

### DHCP Network Verification

#### Checking for Existing DHCP
- **Method**: Set network adapter to "Obtain IP address automatically"
- **Result**: If IP is provided, DHCP server exists in network
- **Conflict**: Only one DHCP server should exist per LAN segment

#### Disabling Router DHCP
- **Reason**: Avoid conflicts with Windows DHCP server
- **Method**: Access router configuration and disable DHCP
- **Alternative**: Use different IP ranges for each DHCP server

### DHCP Process Overview

#### DORA Process
1. **Discover**: Client broadcasts DHCP discover message
2. **Offer**: Server responds with IP address offer
3. **Request**: Client requests the offered IP address
4. **Acknowledge**: Server confirms the IP assignment

#### Port Configuration
- **Client Port**: 68 (DHCP client)
- **Server Port**: 67 (DHCP server)
- **Protocol**: UDP (User Datagram Protocol)

### Best Practices
1. **Single DHCP Server**: Avoid multiple DHCP servers on same network
2. **IP Reservations**: Reserve specific IPs for servers and printers
3. **Lease Time**: Balance between conservation and convenience
4. **Monitoring**: Regularly check DHCP lease utilization
5. **Backup**: Backup DHCP configuration and database regularly
\`\`\`
