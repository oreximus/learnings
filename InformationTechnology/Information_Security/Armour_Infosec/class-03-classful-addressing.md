# Class 3: Classful IP Addressing

## IP Address Classes

### Class A
- **Binary Pattern**: 0xxxxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx
- **Range**: 0.0.0.0 to 127.255.255.255
- **Format**: N.H.H.H (Network.Host.Host.Host)
- **Network Bits**: 8 bits
- **Host Bits**: 24 bits
- **Total Networks**: 2^7 - 2 = 126 networks
- **Hosts per Network**: 2^24 - 2 = 16,777,214 hosts
- **Reserved for**: Large networks (governments, ISPs, large organizations)
- **Default Subnet Mask**: 255.0.0.0 (/8)

### Class B
- **Binary Pattern**: 10xxxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx
- **Range**: 128.0.0.0 to 191.255.255.255
- **Format**: N.N.H.H (Network.Network.Host.Host)
- **Network Bits**: 16 bits
- **Host Bits**: 16 bits
- **Total Networks**: 2^14 = 16,384 networks
- **Hosts per Network**: 2^16 - 2 = 65,534 hosts
- **Reserved for**: Medium-sized networks
- **Default Subnet Mask**: 255.255.0.0 (/16)

### Class C
- **Binary Pattern**: 110xxxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx
- **Range**: 192.0.0.0 to 223.255.255.255
- **Format**: N.N.N.H (Network.Network.Network.Host)
- **Network Bits**: 24 bits
- **Host Bits**: 8 bits
- **Total Networks**: 2^21 = 2,097,152 networks
- **Hosts per Network**: 2^8 - 2 = 254 hosts
- **Reserved for**: Small networks
- **Default Subnet Mask**: 255.255.255.0 (/24)

### Class D (Multicast)
- **Binary Pattern**: 1110xxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx
- **Range**: 224.0.0.0 to 239.255.255.255
- **Purpose**: Multicast addressing
- **Usage**: One-to-many communication

### Class E (Experimental)
- **Binary Pattern**: 1111xxxx.xxxxxxxx.xxxxxxxx.xxxxxxxx
- **Range**: 240.0.0.0 to 255.255.255.255
- **Purpose**: Experimental use
- **Status**: Reserved for future use

## Calculation Methods
- **Adding bit values**: Sum the values of ON bits (128, 64, 32, 16, 8, 4, 2, 1)
- **Subtracting from 255**: 255 minus the sum of OFF bits
\`\`\`
