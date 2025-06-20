# Class 8: IP Address Practical Configuration

## Theory Section

### IP Configuration Principles

- Cannot set IP by making first octet bit pattern invalid for class
- Cannot leave all host bits as 0 (network address)
- Cannot set all host bits as 1 (broadcast address)
- Auto subnet mask assignment based on IP class recognition

### Common Gateway Configurations

```
Jio Router: 192.168.29.1/24
Airtel Router: 192.168.0.1/24
BSNL Router: 192.168.1.1/24
```

## Practical Section

### Class C IP Assignment Example

#### Network: 192.168.1.0/24

```
Network Address: 192.168.1.0 (Reserved)
Gateway: 192.168.1.1
Available for Assignment: 192.168.1.2 - 192.168.1.254
Broadcast Address: 192.168.1.255 (Reserved)
Total Assignable: 253 addresses
```

#### Recommended Assignment Strategy

```
Infrastructure:
- Gateway: 192.168.1.1
- DNS Servers: 192.168.1.2-3
- Network Equipment: 192.168.1.4-20

Servers:
- Static Servers: 192.168.1.21-50

Workstations:
- Static Workstations: 192.168.1.51-100
- DHCP Pool: 192.168.1.101-200
- Reserved/Future: 192.168.1.201-254
```

### Error Scenarios and Troubleshooting

#### Common Error Messages

##### "Host Unreachable"

```
Cause: Same network IP but device not present in network
Example: Pinging 192.168.1.50 when no device has this IP
Solution: Verify target device IP and connectivity
```

##### "Transmit Failed"

```
Cause: Different network IP, routing failure
Example: Device on 192.168.1.x trying to reach 192.168.2.x without proper gateway
Solution: Check gateway configuration and routing table
```

##### "Duplicate IP Address Detected"

```
Cause: Same IP assigned to multiple devices
Solution: Change IP on one of the conflicting devices
```

### Subnet Mask Auto-Detection

```
IP Range 1.0.0.0 - 126.255.255.255    → Class A → 255.0.0.0
IP Range 128.0.0.0 - 191.255.255.255  → Class B → 255.255.0.0
IP Range 192.0.0.0 - 223.255.255.255  → Class C → 255.255.255.0
```

### Practical Exercises

#### Exercise 1: Basic IP Configuration

1. Configure static IP: 192.168.1.10/24
2. Set gateway: 192.168.1.1
3. Test connectivity to gateway
4. Test internet connectivity

#### Exercise 2: IP Conflict Resolution

1. Assign same IP to two devices
2. Observe conflict behavior
3. Resolve by changing one IP
4. Verify resolution

#### Exercise 3: Network Troubleshooting

1. Configure incorrect gateway
2. Test connectivity issues
3. Identify problem using ping/tracert
4. Correct configuration

## Study Questions

1. How does the system automatically determine subnet mask?
2. What steps would you take to troubleshoot IP connectivity issues?
3. Why is proper IP planning important in network design?
4. How do you resolve IP address conflicts?

## Next Class Preview

- Network topologies
- Physical network design
- Network devices and their functions
