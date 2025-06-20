# Class 20: DHCP Configuration and Management

## Theory Section

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

## Practical Section

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

#### Server-Side Monitoring

- **DHCP Console**: Monitor active leases and statistics
- **Event Viewer**: Check DHCP service logs
- **Performance Monitor**: Track DHCP performance counters
- **Network Monitoring**: Wireshark for DHCP packet analysis

### DHCP DORA Process Detailed

#### DORA Explained

- **D**iscover: Client broadcasts to find DHCP servers
- **O**ffer: DHCP server offers IP address and configuration
- **R**equest: Client requests the offered configuration
- **A**cknowledge: Server acknowledges and finalizes lease

#### DORA Process Details

1. **DHCP Discover**:

   - Client broadcasts on 255.255.255.255
   - Contains client MAC address
   - Requests IP configuration

2. **DHCP Offer**:

   - Server responds with available IP
   - Includes lease time and options
   - May include gateway, DNS, etc.

3. **DHCP Request**:

   - Client accepts offered configuration
   - May reject other offers
   - Confirms selection

4. **DHCP Acknowledge**:
   - Server confirms lease
   - Client configures network interface
   - Lease timer starts

### DHCP Configuration Best Practices

#### IP Address Planning

```
Network: 192.168.1.0/24

Infrastructure (Static):
- Gateway: 192.168.1.1
- DNS Servers: 192.168.1.2-3
- Network Equipment: 192.168.1.4-20

Servers (Static/Reserved):
- Static Servers: 192.168.1.21-50
- DHCP Reservations: 192.168.1.51-80

Workstations:
- DHCP Pool: 192.168.1.100-200
- Reserved/Future: 192.168.1.201-254
```

#### Monitoring and Maintenance

- **Regular Backup**: Schedule automatic DHCP database backups
- **Lease Monitoring**: Monitor lease utilization and availability
- **Event Logging**: Enable and review DHCP event logs
- **Performance Monitoring**: Track DHCP server performance metrics

### Troubleshooting DHCP Issues

#### Common Problems

1. **No IP Address Assigned**: DHCP server not responding
2. **Wrong IP Range**: Client receiving unexpected IP
3. **Lease Conflicts**: Multiple clients with same IP
4. **DNS Issues**: DHCP not providing correct DNS servers

#### Diagnostic Steps

1. **Check DHCP Service**: Verify service is running
2. **Review Scope Configuration**: Confirm scope is active and has available IPs
3. **Check Network Connectivity**: Ensure client can reach DHCP server
4. **Review Event Logs**: Check for DHCP-related errors
5. **Test with Different Client**: Isolate client-specific issues

## Study Questions

1. What are the advantages of DHCP policies over simple IP assignment?
2. How do exclusions and reservations work together in DHCP planning?
3. What factors should be considered when setting lease duration?
4. How does the DORA process ensure reliable IP address assignment?

## Next Class Preview

- Linux command chaining and pipes
- Background process management
- Text processing and filtering
- System monitoring techniques
