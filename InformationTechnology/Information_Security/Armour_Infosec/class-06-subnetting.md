# Class 6: Subnetting and Subnet Masks

## Subnet Mask Fundamentals
- **Size**: 32-bit address
- **Structure**: 4 sections (octets)
- **Purpose**: Distinguishes network portion from host portion
- **Rule**: Network bits are ON (1), host bits are OFF (0)

## Default Subnet Masks by Class

### Class A Default
- **Format**: N.H.H.H
- **Binary**: 11111111.00000000.00000000.00000000
- **Decimal**: 255.0.0.0
- **CIDR**: /8
- **Network Bits**: 8
- **Host Bits**: 24

### Class B Default
- **Format**: N.N.H.H
- **Binary**: 11111111.11111111.00000000.00000000
- **Decimal**: 255.255.0.0
- **CIDR**: /16
- **Network Bits**: 16
- **Host Bits**: 16

### Class C Default
- **Format**: N.N.N.H
- **Binary**: 11111111.11111111.11111111.00000000
- **Decimal**: 255.255.255.0
- **CIDR**: /24
- **Network Bits**: 24
- **Host Bits**: 8

## Subnetting Concepts

### Definition
- **Subnetting**: Logical subdivision of an IP network
- **Purpose**: Efficient use of IP addresses and network organization

### Classful vs Classless
- **Classful**: IP Address + Default Class Subnet Mask
- **Classless**: IP Address + Any Subnet Mask (CIDR)

## Subnetting Example

### Custom Subnet Mask
- **Subnet Mask**: 11111111.11111111.11111111.10000000
- **Decimal**: 255.255.255.128
- **CIDR**: /25
- **Network Bits**: 25
- **Host Bits**: 7
- **Subnets Created**: 2^1 = 2 subnets
- **Hosts per Subnet**: 2^7 - 2 = 126 hosts

## CIDR (Classless Inter-Domain Routing)
- **Purpose**: More flexible addressing scheme
- **Notation**: IP/prefix length (e.g., 192.168.1.0/24)
- **Benefits**: Efficient address allocation, route aggregation
\`\`\`
