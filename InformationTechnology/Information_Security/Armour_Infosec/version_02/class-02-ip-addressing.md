# Class 2: IP Addressing Fundamentals

## Theory Section

### What is an IP Address?

- **IP Address**: Internet Protocol Address
- Unique identifier for devices in a network
- Essential for network communication and routing

### IP Versions

#### IPv4 (Internet Protocol Version 4)

- **Size**: 32-bit address
- **Structure**: Divided into four sections (octets), each containing 8 bits
- **Range**: 0 to 255 for each octet
- **Format**: xxx.xxx.xxx.xxx (e.g., 192.168.1.1)
- **Total Possible Addresses**: 4,294,967,296 (approximately 4.3 billion)
- **Current Status**: Nearly exhausted, still widely used

#### IPv6 (Internet Protocol Version 6)

- **Size**: 128-bit address
- **Structure**: Divided into eight sections, each containing 16 bits
- **Format**: xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx
- **Total Possible Addresses**: 340,282,366,920,938,463,463,374,607,431,768,211,456
- **Current Status**: Gradually being adopted worldwide

## Practical Section

### IPv4 Address Examples

```
192.168.1.1    - Common home router address
10.0.0.1       - Private network address
172.16.0.1     - Private network address
8.8.8.8        - Google DNS server
```

### IPv6 Address Examples

```
2001:0db8:85a3:0000:0000:8a2e:0370:7334  - Full format
2001:db8:85a3::8a2e:370:7334             - Compressed format
::1                                       - Loopback address
```

### Key Concepts

1. **Uniqueness**: Each device must have a unique IP address within its network
2. **Hierarchy**: IP addresses have network and host portions
3. **Routing**: IP addresses enable packet routing across networks
4. **Address Exhaustion**: IPv4 addresses are limited, leading to IPv6 adoption

## Study Questions

1. Why do we need IP addresses?
2. What are the main differences between IPv4 and IPv6?
3. How many devices can theoretically be addressed with IPv4?
4. Why is IPv6 necessary?

## Next Class Preview

- Classful IP addressing
- Network classes (A, B, C, D, E)
- Subnet masks and network identification
