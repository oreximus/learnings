# Class 8: IP Address Configuration Practical

## IP Configuration Guidelines

### Setting IP Addresses
- **First Octet**: Cannot set all bits to 1 (invalid)
- **Host Bits**: Cannot be all 0s (network address)
- **Host Bits**: Cannot be all 1s (broadcast address)
- **Auto-configuration**: Windows automatically assigns appropriate subnet mask for IP class

## Common Gateway Configurations

### ISP Default Gateways
- **Jio**: 192.168.29.1
- **Airtel**: 192.168.0.1
- **Purpose**: Router's internal IP address for the network

## Network Troubleshooting

### Common Error Messages

#### Host Unreachable
- **Scenario**: Same network IP but device not present in network
- **Cause**: Device is offline or IP conflict
- **Solution**: Check device connectivity and ping response

#### Transmit Failed
- **Scenario**: Different network IP address
- **Cause**: Attempting to communicate across network boundaries without proper routing
- **Solution**: Verify gateway configuration and routing tables

## Practical Example: Class C Configuration

### Network Setup
- **Network**: 192.168.1.0/24
- **Subnet Mask**: 255.255.255.0
- **Gateway**: 192.168.1.1
- **Usable IP Range**: 192.168.1.2 to 192.168.1.254

### Device Assignment
\`\`\`
Device 1: 192.168.1.2
Device 2: 192.168.1.3
Device 3: 192.168.1.4
...
Device 253: 192.168.1.254
\`\`\`

### Reserved Addresses
- **192.168.1.0**: Network address (cannot assign)
- **192.168.1.1**: Gateway (router)
- **192.168.1.255**: Broadcast address (cannot assign)

## Configuration Best Practices
1. Always document IP assignments
2. Use sequential numbering when possible
3. Reserve ranges for different device types
4. Test connectivity after configuration
5. Maintain consistent subnet masks across network
\`\`\`
