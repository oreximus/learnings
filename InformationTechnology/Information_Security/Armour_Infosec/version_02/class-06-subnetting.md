# Class 6: Subnetting Fundamentals

## Theory Section

### What is Subnetting?

- **Definition**: A subnetwork is a logical subdivision of an IP network
- **Purpose**: Divide large networks into smaller, manageable segments
- **Benefits**: Better organization, improved security, reduced broadcast domains

### Subnet Mask

- **Definition**: 32-bit address that defines network and host portions
- **Structure**: 4 sections (octets) like IP addresses
- **Function**: Network bits ON (1), Host bits OFF (0)

### Default Subnet Masks

#### Class A Default

- **Format**: N.H.H.H
- **Binary**: 11111111.00000000.00000000.00000000
- **Decimal**: 255.0.0.0
- **CIDR**: /8
- **Network Bits**: 8, **Host Bits**: 24

#### Class B Default

- **Format**: N.N.H.H
- **Binary**: 11111111.11111111.00000000.00000000
- **Decimal**: 255.255.0.0
- **CIDR**: /16
- **Network Bits**: 16, **Host Bits**: 16

#### Class C Default

- **Format**: N.N.N.H
- **Binary**: 11111111.11111111.11111111.00000000
- **Decimal**: 255.255.255.0
- **CIDR**: /24
- **Network Bits**: 24, **Host Bits**: 8

## Practical Section

### Classful vs Classless

#### Classful Example

```
IP Address: 192.168.1.10
Default Class C Mask: 255.255.255.0
Result: Traditional Class C network
```

#### Classless Example

```
IP Address: 192.168.1.10
Custom Mask: 255.255.255.128
Result: Classless network (CIDR)
```

### Subnetting Example

#### Original Network

```
Network: 192.168.1.0/24
Default Mask: 255.255.255.0
Hosts Available: 254
```

#### After Subnetting

```
Subnet Mask: 255.255.255.128 (/25)
Network Bits: 25, Host Bits: 7

Subnet 1: 192.168.1.0/25 (192.168.1.1 - 192.168.1.126)
Subnet 2: 192.168.1.128/25 (192.168.1.129 - 192.168.1.254)

Hosts per Subnet: 2^7 - 2 = 126 hosts
Total Subnets: 2^1 = 2 subnets
```

### CIDR (Classless Inter-Domain Routing)

- **Purpose**: More efficient IP address allocation
- **Notation**: IP/prefix length (e.g., 192.168.1.0/25)
- **Advantage**: Variable-length subnet masks
- **Flexibility**: Can create subnets of any size

### Reserved Addresses

#### Network Address

- **Definition**: All network bits ON, all host bits OFF
- **Example**: 192.168.1.0/24
- **Usage**: Identifies the network itself

#### Broadcast Address

- **Definition**: All network bits ON, all host bits ON
- **Example**: 192.168.1.255/24
- **Usage**: Sends to all devices in network

### Subnet Calculation Examples

#### Example 1: /26 Subnetting

```
Original: 192.168.1.0/24
New Mask: /26 (255.255.255.192)

Subnets Created:
1. 192.168.1.0/26 (1-62)
2. 192.168.1.64/26 (65-126)
3. 192.168.1.128/26 (129-190)
4. 192.168.1.192/26 (193-254)

Hosts per Subnet: 62
Total Subnets: 4
```

## Study Questions

1. What are the benefits of subnetting?
2. How do you calculate the number of subnets and hosts?
3. What is the difference between classful and classless addressing?
4. How do network and broadcast addresses work?

## Next Class Preview

- IP address assignment rules
- Valid IP ranges and restrictions
- DHCP conflicts and resolution
