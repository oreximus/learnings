# Class 4: IANA and IP Address Distribution

## IANA (Internet Assigned Numbers Authority)
- **IP Address Management**: Global coordination of IP address allocation
- **DNS Management**: Root zone management
- **Protocol Assignment**: Internet protocol parameters

## IP Distribution Hierarchy

### Tier 1 (T1) - International Level
- **From**: IANA
- **To**: Gateway of India (GOI)
- **Connection**: Submarine cables (physical connection)
- **Allocation**: Approximately 80-90% of IP addresses

### Tier 2 (T2) - National Level
- **From**: Gateway of India
- **To**: ISPs (BSNL, Jio, Airtel, etc.)
- **Purpose**: National distribution

### Tier 3 (T3) - Regional Level
- **From**: ISPs
- **To**: Cities (e.g., Indore)
- **Purpose**: Local distribution

## IP Address Types

### Public IP Addresses
- **Source**: Provided by ISPs
- **Scope**: Globally unique
- **Usage**: Internet communication
- **Visibility**: Accessible from anywhere on the internet

### Private IP Addresses
- **Source**: Assigned internally within private networks
- **Scope**: Local network only
- **Usage**: Internal communication
- **Purpose**: Solution to IPv4 address shortage

## Reserved Private IP Ranges

### Class A Private Range
- **Range**: 10.0.0.0 to 10.255.255.255
- **Subnet Mask**: 255.0.0.0 (/8)

### Class B Private Range
- **Range**: 172.16.0.0 to 172.31.255.255
- **Subnet Mask**: 255.255.0.0 (/16)

### Class C Private Range
- **Range**: 192.168.0.0 to 192.168.255.255
- **Subnet Mask**: 255.255.255.0 (/24)

### Special Ranges
- **Carrier-Grade NAT**: 100.64.0.0 to 100.127.255.255
- **Loopback**: 127.0.0.1 to 127.255.255.255

## Network Conflicts
- **Same Network IP**: Cannot communicate outside the network if devices have the same network IP
- **Different Network IP**: Requires routing through gateway
\`\`\`
