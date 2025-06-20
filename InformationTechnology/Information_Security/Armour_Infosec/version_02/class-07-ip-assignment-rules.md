# Class 7: Rules for Assigning IP Addresses

## Theory Section

### IP Address Assignment Rules

#### 1. Uniqueness

- **Rule**: Each IP address must be unique within its network
- **Conflict Result**: First device gets the IP, subsequent devices fail to configure
- **Impact**: Network connectivity issues, duplicate IP errors

#### 2. Correct Network

- **Rule**: IP network segment must be consistent across the network/subnet
- **Example**: All devices in 192.168.1.0/24 must have 192.168.1.x addresses
- **Impact**: Devices on different networks cannot communicate directly

#### 3. Valid IP Range

- **Rule**: IP addresses must fall within valid ranges for their class
- **Invalid Examples**: 256.1.1.1, 192.168.1.0 (network address), 192.168.1.255 (broadcast)
- **Valid Range**: First usable to last usable address in subnet

#### 4. Avoiding Reserved Addresses

- **Network Address**: All host bits = 0 (e.g., 192.168.1.0/24)
- **Broadcast Address**: All host bits = 1 (e.g., 192.168.1.255/24)
- **Loopback**: 127.0.0.0/8 range
- **Private Ranges**: Must be used appropriately

#### 5. Consistent Subnet Mask

- **Rule**: All devices in same network must use same subnet mask
- **Example**: If gateway uses /24, all devices must use /24
- **Impact**: Incorrect masks cause routing issues

#### 6. Avoid DHCP Conflicts

- **Rule**: Static IPs should not overlap with DHCP pool
- **Best Practice**: Reserve ranges for static assignment
- **Example**: DHCP pool 192.168.1.100-200, Static range 192.168.1.1-99

#### 7. Consistent Gateway Network

- **Rule**: Gateway must be in same network as client devices
- **Example**: If clients are 192.168.1.x/24, gateway must be 192.168.1.y/24
- **Common**: Gateway typically uses first usable IP (192.168.1.1)

## Practical Section

### Reserved Addresses Explained

#### Network Address

```
Network: 192.168.1.0/24
Binary: 11000000.10101000.00000001.00000000
Usage: Identifies the network itself
Cannot be assigned to devices
```

#### Broadcast Address

```
Broadcast: 192.168.1.255/24
Binary: 11000000.10101000.00000001.11111111
Usage: Sends packets to all devices in network
Cannot be assigned to devices
```

### Valid IP Assignment Examples

#### Class C Network (192.168.1.0/24)

```
Network Address: 192.168.1.0 (Reserved)
Gateway: 192.168.1.1 (Typically first usable)
Usable Range: 192.168.1.2 - 192.168.1.254
Broadcast: 192.168.1.255 (Reserved)
Total Usable IPs: 254
```

#### Subnet Example (192.168.1.0/25)

```
Subnet 1:
Network: 192.168.1.0
Usable: 192.168.1.1 - 192.168.1.126
Broadcast: 192.168.1.127

Subnet 2:
Network: 192.168.1.128
Usable: 192.168.1.129 - 192.168.1.254
Broadcast: 192.168.1.255
```

### Common ISP Gateway Examples

```
Jio Default Gateway: 192.168.29.1
Airtel Default Gateway: 192.168.0.1
BSNL Default Gateway: 192.168.1.1
```

### IP Configuration Best Practices

#### Static IP Assignment

```
Server IPs: 192.168.1.1 - 192.168.1.50
Network Equipment: 192.168.1.51 - 192.168.1.99
DHCP Pool: 192.168.1.100 - 192.168.1.200
Reserved: 192.168.1.201 - 192.168.1.254
```

#### Documentation Requirements

- Maintain IP address inventory
- Document static assignments
- Track DHCP reservations
- Monitor for conflicts

## Troubleshooting Common Issues

### Error Messages and Causes

#### "Host Unreachable"

- **Cause**: Same network IP but device not present
- **Solution**: Verify device is powered on and connected

#### "Transmit Failed"

- **Cause**: Different network IP, routing issue
- **Solution**: Check gateway configuration and routing

#### "Duplicate IP Address"

- **Cause**: Same IP assigned to multiple devices
- **Solution**: Change one device's IP address

#### "Invalid IP Configuration"

- **Cause**: Incorrect subnet mask or gateway
- **Solution**: Verify network settings match network design

## Study Questions

1. Why can't network and broadcast addresses be assigned to devices?
2. What happens when two devices have the same IP address?
3. How do you determine the valid IP range for a subnet?
4. What are the consequences of using incorrect subnet masks?

## Next Class Preview

- IP address practical configuration
- Network troubleshooting tools
- Common configuration errors and solutions
