# Class 7: IP Address Assignment Rules

## Rules for Assigning IP Addresses

### 1. Uniqueness
- **Requirement**: Each IP address must be unique within the network
- **Conflict Resolution**: First device gets the IP, subsequent devices are denied
- **Impact**: IP conflicts cause network connectivity issues

### 2. Correct Network Segment
- **Requirement**: All devices must be on the same network or subnet
- **Purpose**: Enables direct communication without routing
- **Example**: All devices in 192.168.1.x network

### 3. Valid IP Range
- **Requirement**: IP addresses must fall within valid ranges
- **Avoid**: Network address (all host bits 0)
- **Avoid**: Broadcast address (all host bits 1)

### 4. Avoiding Reserved Addresses
- **Network Address**: First address in range (e.g., 192.168.1.0)
- **Broadcast Address**: Last address in range (e.g., 192.168.1.255)
- **Loopback**: 127.x.x.x range reserved for localhost

### 5. Consistent Subnet Mask
- **Requirement**: All devices must use the same subnet mask
- **Purpose**: Ensures proper network/host boundary identification
- **Auto-configuration**: Windows automatically applies class-based masks

### 6. Avoid DHCP Conflicts
- **Requirement**: Static IPs should not conflict with DHCP pool
- **Best Practice**: Reserve static IP ranges outside DHCP scope
- **Documentation**: Maintain IP address allocation records

### 7. Consistent Gateway Network
- **Requirement**: Gateway must be on the same network as clients
- **Common Gateways**: 
  - Jio: 192.168.29.1
  - Airtel: 192.168.0.1
- **Purpose**: Enables routing to other networks

## Special Addresses

### Network Address
- **Definition**: All network bits ON, all host bits OFF
- **Purpose**: Identifies the network itself
- **Usage**: Routing table entries

### Broadcast Address
- **Definition**: All network bits ON, all host bits ON
- **Purpose**: Send data to all devices on network
- **Usage**: Network-wide announcements

## Common Error Messages

### Host Unreachable
- **Cause**: Same network IP but device not present
- **Solution**: Verify device connectivity and IP configuration

### Transmit Failed
- **Cause**: Different network IP address
- **Solution**: Check routing or gateway configuration

## Example: Class C IP Assignment
- **Network**: 192.168.1.0/24
- **Usable Range**: 192.168.1.2 to 192.168.1.254
- **Gateway**: 192.168.1.1 (typically)
- **Broadcast**: 192.168.1.255
- **Total Usable**: 253 addresses
\`\`\`
