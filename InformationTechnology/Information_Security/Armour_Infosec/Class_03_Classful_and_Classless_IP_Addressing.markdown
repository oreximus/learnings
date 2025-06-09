# Class 03: Classful and Classless IP Addressing

## Overview
This class explains classful and classless IP addressing schemes, focusing on IPv4 classes, their ranges, and calculations.

## Classful IP Addressing

### Class A
- **Range**: 0.0.0.0 to 127.255.255.255
- **Binary**: First bit is 0 (e.g., 0xxxxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx)
- **Network Bits**: 8
- **Host Bits**: 24
- **Total Networks**: 2⁷ - 2 = 126 (subtracting 0.0.0.0 and 127.0.0.0 for special use)
- **Hosts per Network**: 2²⁴ - 2 = 16,777,214 (subtracting network and broadcast addresses)
- **Reserved For**: Large organizations, ISPs, and governments
- **Default Subnet Mask**: 255.0.0.0 (/8)

### Class B
- **Range**: 128.0.0.0 to 191.255.255.255
- **Binary**: First two bits are 10 (e.g., 10xxxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx)
- **Network Bits**: 16
- **Host Bits**: 16
- **Total Networks**: 2¹⁴ = 16,384
- **Hosts per Network**: 2¹⁶ - 2 = 65,534
- **Reserved For**: Medium-sized organizations and institutions
- **Default Subnet Mask**: 255.255.0.0 (/16)

### Class C
- **Range**: 192.0.0.0 to 223.255.255.255
- **Binary**: First three bits are 110 (e.g., 110xxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx)
- **Network Bits**: 24
- **Host Bits**: 8
- **Total Networks**: 2²¹ = 2,097,152
- **Hosts per Network**: 2⁸ - 2 = 254
- **Reserved For**: Small networks
- **Default Subnet Mask**: 255.255.255.0 (/24)

### Class D
- **Range**: 224.0.0.0 to 239.255.255.255
- **Binary**: First four bits are 1110 (e.g., 1110xxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx)
- **Purpose**: Multicast addressing
- **Description**: Used for multicast groups, not for individual hosts.

### Class E
- **Range**: 240.0.0.0 to 255.255.255.255
- **Binary**: First four bits are 1111 (e.g., 1111xxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx)
- **Purpose**: Reserved for experimental use
- **Description**: Not used in public networks.

## Classless IP Addressing
- **Classless Inter-Domain Routing (CIDR)**: Replaces classful addressing by allowing flexible subnet masks (e.g., /25, /26) to allocate IP addresses more efficiently.
- **Example**: 192.168.1.0/24 (classful) vs. 192.168.1.0/25 (classless, splitting into smaller subnets).

## Corrections
- The original calculations for Class A and B networks were incorrect (listed as 2⁷-2). Corrected to 2⁷-2 for Class A and 2¹⁴ for Class B.
- Clarified that Class D and E are not used for traditional host addressing.