# Class 3: Classful IP Addressing

## Theory Section

### Classful IP Addressing

Traditional method of IP address allocation based on predefined classes.

#### Class A Networks

- **Binary Pattern**: 0xxxxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx
- **Range**: 0.0.0.0 to 127.255.255.255
- **Network Format**: N.H.H.H (Network.Host.Host.Host)
- **Default Subnet Mask**: 255.0.0.0 (/8)
- **Network Bits**: 8 bits
- **Host Bits**: 24 bits
- **Total Networks**: 2^7 - 2 = 126 networks
- **Hosts per Network**: 2^24 - 2 = 16,777,214 hosts
- **Reserved For**: Large networks (governments, ISPs, large organizations)

#### Class B Networks

- **Binary Pattern**: 10xxxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx
- **Range**: 128.0.0.0 to 191.255.255.255
- **Network Format**: N.N.H.H (Network.Network.Host.Host)
- **Default Subnet Mask**: 255.255.0.0 (/16)
- **Network Bits**: 16 bits
- **Host Bits**: 16 bits
- **Total Networks**: 2^14 = 16,384 networks
- **Hosts per Network**: 2^16 - 2 = 65,534 hosts
- **Reserved For**: Medium-sized networks

#### Class C Networks

- **Binary Pattern**: 110xxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx
- **Range**: 192.0.0.0 to 223.255.255.255
- **Network Format**: N.N.N.H (Network.Network.Network.Host)
- **Default Subnet Mask**: 255.255.255.0 (/24)
- **Network Bits**: 24 bits
- **Host Bits**: 8 bits
- **Total Networks**: 2^21 = 2,097,152 networks
- **Hosts per Network**: 2^8 - 2 = 254 hosts
- **Reserved For**: Small networks

#### Class D Networks

- **Binary Pattern**: 1110xxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx
- **Range**: 224.0.0.0 to 239.255.255.255
- **Purpose**: Multicast addressing
- **Usage**: Group communication, streaming

#### Class E Networks

- **Binary Pattern**: 1111xxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx
- **Range**: 240.0.0.0 to 255.255.255.255
- **Purpose**: Experimental and research
- **Usage**: Reserved for future use

## Practical Section

### Binary to Decimal Conversion

```
Binary: 11000000.10101000.00000001.00000001
Decimal: 192.168.1.1

Calculation method:
- Add all bit values where bit = 1
- Or subtract from 255 where bit = 0
```

### Identifying Network Classes

```
IP Address: 10.0.0.1        → Class A
IP Address: 172.16.0.1      → Class B
IP Address: 192.168.1.1     → Class C
IP Address: 224.0.0.1       → Class D
IP Address: 240.0.0.1       → Class E
```

### Classless Addressing (CIDR)

- **CIDR**: Classless Inter-Domain Routing
- Uses variable-length subnet masks
- More efficient address allocation
- Notation: IP/prefix (e.g., 192.168.1.0/24)

## Study Questions

1. What are the advantages and disadvantages of classful addressing?
2. How do you identify the class of an IP address?
3. Why was CIDR introduced?
4. What is the difference between network and host portions?

## Next Class Preview

- IANA and IP address management
- Public vs Private IP addresses
- NAT and address translation
