# Comprehensive Network & Information Security Notes

## Table of Contents

1. [Network Fundamentals](#network-fundamentals)
2. [IP Addressing](#ip-addressing)
3. [Subnetting & CIDR](#subnetting--cidr)
4. [Network Devices & Topologies](#network-devices--topologies)
5. [DHCP & Network Services](#dhcp--network-services)
6. [Operating Systems](#operating-systems)
7. [Windows Server Administration](#windows-server-administration)
8. [Linux Administration](#linux-administration)
9. [Domain & DNS Concepts](#domain--dns-concepts)

---

## Network Fundamentals

### What is a Network?

A **network** is a collection of interconnected devices that can communicate and share resources. The term comes from "Net + Work" - devices working together through a network infrastructure.

### Types of Networks

![Network Types Overview](/placeholder.svg?height=400&width=600)
_Network types from PAN to WAN with their respective ranges and devices_

#### 1. PAN (Personal Area Network)

- **Purpose**: Connect personal devices around an individual
- **Device**: Bluetooth, USB, or personal hotspot
- **Range**: Up to 10 meters
- **Devices**: 1-10 devices (smartphones, tablets, laptops, smartwatches)
- **Example**: Connecting your phone to wireless earbuds

#### 2. LAN (Local Area Network)

- **Purpose**: Connect devices within a building or small area
- **Device**: Switch (Layer 2 device)
- **Range**: 4m - 100m
- **Devices**: 2-100+ PCs
- **Example**: Office network, home network

#### 3. CAN (Campus Area Network)

- **Purpose**: Connect multiple buildings within a campus
- **Device**: L3 Switch (operates at Network Layer)
- **Range**: 4m - 1km
- **Devices**: 100-1000+ devices
- **Example**: University campus, corporate campus

#### 4. MAN (Metropolitan Area Network)

- **Purpose**: Connect networks across a metropolitan area
- **Device**: Router (organization-owned)
- **Range**: Up to 50 km
- **Devices**: Multiple locations
- **Example**: City government network, cable TV network

#### 5. WAN (Wide Area Network)

- **Purpose**: Connect networks across large geographical areas
- **Device**: Router (ISP-managed)
- **Range**: 4m - worldwide
- **Devices**: Unlimited locations
- **Example**: Internet, corporate networks across countries

---

## IP Addressing

### What is an IP Address?

An **IP Address** (Internet Protocol Address) is a unique numerical identifier assigned to every device on a network. Think of it as a postal address for your device on the internet.

### IP Versions

![IPv4 vs IPv6 Comparison](/placeholder.svg?height=300&width=500)
_Visual comparison of IPv4 and IPv6 address formats and capacity_

#### IPv4 (Internet Protocol Version 4)

- **Size**: 32-bit address
- **Structure**: Four octets (8 bits each), separated by dots
- **Format**: X.X.X.X (where X ranges from 0-255)
- **Example**: 192.168.1.100
- **Total Addresses**: 4,294,967,296 (≈4.3 billion)
- **Problem**: Not enough addresses for all devices globally

#### IPv6 (Internet Protocol Version 6)

- **Size**: 128-bit address
- **Structure**: Eight groups of 16 bits, separated by colons
- **Format**: XXXX:XXXX:XXXX:XXXX:XXXX:XXXX:XXXX:XXXX
- **Example**: 2001:0db8:85a3:0000:0000:8a2e:0370:7334
- **Total Addresses**: 340,282,366,920,938,463,463,374,607,431,768,211,456
- **Solution**: Solves IPv4 address shortage

### IPv4 Address Classes

![IPv4 Address Classes](/placeholder.svg?height=400&width=700)
_Visual representation of Class A, B, C, D, and E with their ranges and uses_

```
IPv4 Address Classes (Simple View):

Class A: 1.0.0.0    to 126.255.255.255  (/8)  - Large Organizations
         [N][H][H][H] - 126 networks, 16M+ hosts each

Class B: 128.0.0.0  to 191.255.255.255  (/16) - Medium Organizations
         [N][N][H][H] - 16K networks, 65K hosts each

Class C: 192.0.0.0  to 223.255.255.255  (/24) - Small Organizations
         [N][N][N][H] - 2M networks, 254 hosts each

Class D: 224.0.0.0  to 239.255.255.255        - Multicast
Class E: 240.0.0.0  to 255.255.255.255        - Experimental
```

### Public vs Private IP Addresses

![Public vs Private IP Ranges](/placeholder.svg?height=350&width=600)
_Diagram showing public internet and private network ranges_

```
Private IP Address Ranges:

Class A Private: 10.0.0.0      to 10.255.255.255
Class B Private: 172.16.0.0    to 172.31.255.255
Class C Private: 192.168.0.0   to 192.168.255.255

Special Ranges:
Loopback:       127.0.0.0      to 127.255.255.255
Link-Local:     169.254.0.0    to 169.254.255.255 (APIPA)
Carrier NAT:    100.64.0.0     to 100.127.255.255
```

### IANA Hierarchy

![IANA Hierarchy Structure](/placeholder.svg?height=400&width=600)
_Hierarchical structure from IANA to end users_

```
IANA IP Address Distribution Hierarchy:

                    IANA (Global)
                         |
              Regional Internet Registries
                         |
        +--------+--------+--------+--------+
        |        |        |        |        |
      ARIN    RIPE NCC   APNIC   LACNIC  AFRINIC
   (N.America) (Europe) (Asia)  (Latin)  (Africa)
        |        |        |        |        |
                National Registries & ISPs
                         |
                    End Users
```

### Network Communication Process

![Network Communication Flow](/placeholder.svg?height=300&width=700)
_Step-by-step communication between devices on same and different networks_

```
Network Communication Process:

Same Network:
Device A → Switch → Device B (Direct)

Different Network:
Device A → Router/Gateway → Internet → Router → Device B

Example:
PC (192.168.1.10) → Router (192.168.1.1) → Internet → Google (8.8.8.8)
```

---

## Network Devices & Topologies

### Network Devices

![Network Devices Comparison](/placeholder.svg?height=350&width=600)
_Hub, Switch, Router, and Access Point with their OSI layers_

```
Network Device Layers:

Hub (Layer 1 - Physical)
├── Simple signal repeater
├── Single collision domain
└── Half-duplex only (OBSOLETE)

Switch (Layer 2 - Data Link)
├── MAC address learning
├── Each port = separate collision domain
└── Full-duplex capable

Router (Layer 3 - Network)
├── IP packet routing
├── Connects different networks
└── NAT, DHCP, Firewall features

Access Point (Layer 2 - Wireless)
├── Wireless connectivity
├── 802.11 standards
└── Bridge to wired network
```

### Network Topologies

#### Star Topology

![Star Topology Diagram](/placeholder.svg?height=300&width=400)
_Central switch connected to multiple devices_

```
Star Topology:

        PC1
         |
PC4 --- Switch --- PC2
         |
        PC3

✓ Easy troubleshooting
✓ Centralized management
✗ Single point of failure
```

#### Bus Topology

![Bus Topology Diagram](/placeholder.svg?height=200&width=500)
_Devices connected along a single cable_

```
Bus Topology:

[T] --- PC1 --- PC2 --- PC3 --- PC4 --- [T]
        (Shared Communication Line)

✓ Simple and cost-effective
✓ Minimal cable required
✗ Difficult troubleshooting
✗ Single point of failure
```

#### Ring Topology

![Ring Topology Diagram](/placeholder.svg?height=300&width=300)
_Devices connected in a circular fashion_

```
Ring Topology:

    PC1 → PC2
     ↑     ↓
    PC4 ← PC3

✓ Predictable performance
✓ No collisions
✗ One failure affects all
✗ Difficult to troubleshoot
```

#### Mesh Topology

![Mesh Topology Diagram](/placeholder.svg?height=300&width=400)
_Multiple connections between all devices_

```
Full Mesh Topology:

    A ←→ B
    ↕ ✗ ↕
    D ←→ C

✓ High redundancy
✓ Multiple paths
✗ Expensive
✗ Complex configuration
```

---

## DHCP & Network Services

### DHCP (Dynamic Host Configuration Protocol)

![DHCP DORA Process](/placeholder.svg?height=400&width=600)
_Four-step DHCP process visualization_

```
DHCP DORA Process:

Client                    DHCP Server
  |                           |
  |------ DISCOVER ---------->| (Broadcast: "I need an IP")
  |                           |
  |<------ OFFER -------------| (Unicast: "Here's 192.168.1.100")
  |                           |
  |------ REQUEST ----------->| (Broadcast: "I want 192.168.1.100")
  |                           |
  |<------ ACK ---------------| (Unicast: "Confirmed + Gateway/DNS")

Result: Client gets IP: 192.168.1.100
                Gateway: 192.168.1.1
                DNS: 8.8.8.8
```

### NAT (Network Address Translation)

![NAT Process Diagram](/placeholder.svg?height=300&width=600)
_How private IPs are translated to public IPs_

```
NAT Translation Process:

Private Network          Router (NAT)         Internet
192.168.1.10:1234  →  203.0.113.1:5678  →  8.8.8.8:53
                   ←                     ←
                   Translation Table:
                   Internal → External
                   192.168.1.10:1234 ↔ 203.0.113.1:5678
```

---

## Domain & DNS Concepts

### DNS Hierarchy

![DNS Hierarchy Structure](/placeholder.svg?height=400&width=600)
_Complete DNS hierarchy from root to subdomains_

```
DNS Hierarchy Structure:

                Root Servers (.)
                      |
        +-------------+-------------+
        |             |             |
    .com TLD      .org TLD      .net TLD
        |             |             |
   example.com   nonprofit.org  network.net
        |
   www.example.com

Query Flow:
1. Client → Local DNS
2. Local DNS → Root Server
3. Root → TLD Server (.com)
4. TLD → Authoritative Server (example.com)
5. Authoritative → Local DNS (IP Address)
6. Local DNS → Client (Final Answer)
```

### DNS Query Process

![DNS Resolution Process](/placeholder.svg?height=350&width=700)
_Step-by-step DNS query resolution_

```
DNS Resolution Process for www.example.com:

Client Device → Local DNS Resolver → Root Server
     ↑                                    ↓
     |                              "Ask .com server"
     |                                    ↓
     |              Local DNS → .com TLD Server
     |                   ↑              ↓
     |                   |        "Ask example.com NS"
     |                   |              ↓
     |              Local DNS → example.com Server
     |                   ↑              ↓
     |                   |         "192.168.1.100"
     |                   ↓
     ←── "192.168.1.100" ←──────────────
```

---

## Alternative Simple Visualization Methods

### 1. ASCII Art Diagrams

Perfect for text-only environments and simple understanding:

```
Network Topology Comparison:

STAR:           BUS:            RING:           MESH:
  PC1           PC1-PC2-PC3      PC1→PC2         PC1↔PC2
   |             (shared)         ↑  ↓           ↕ ✗ ↕
Switch                           PC4←PC3         PC4↔PC3
   |
  PC2
```

### 2. Simple Tables

For structured information:

| Network Type | Range  | Device     | Example Use       |
| ------------ | ------ | ---------- | ----------------- |
| PAN          | 10m    | Bluetooth  | Phone to earbuds  |
| LAN          | 100m   | Switch     | Office network    |
| CAN          | 1km    | L3 Switch  | University campus |
| MAN          | 50km   | Router     | City network      |
| WAN          | Global | ISP Router | Internet          |

### 3. Process Flows

For step-by-step procedures:

```
DHCP Configuration Steps:
1. Install DHCP Role → 2. Create Scope → 3. Set Options → 4. Activate

Subnetting Process:
Original Network → Determine Requirements → Calculate Subnets → Assign Ranges
```

### 4. Hierarchical Lists

For organizational structures:

```
Linux File System:
/
├── bin/ (essential commands)
├── etc/ (configuration files)
├── home/ (user directories)
├── var/ (variable data)
└── usr/ (user programs)
```

### 5. Comparison Charts

For feature comparisons:

```
IPv4 vs IPv6:
Feature     | IPv4          | IPv6
------------|---------------|------------------
Address Size| 32-bit        | 128-bit
Format      | 192.168.1.1   | 2001:db8::1
Addresses   | 4.3 billion   | 340 undecillion
Header      | Variable      | Fixed
Security    | Optional      | Built-in
```

---

## Tools for Creating Simple Images

### Free Online Tools:

1. **Draw.io** (now diagrams.net) - Free online diagramming
2. **Canva** - Simple graphic design with network templates
3. **Google Drawings** - Basic shapes and diagrams
4. **Lucidchart** - Professional network diagrams (free tier)
5. **Creately** - Collaborative diagramming

### Desktop Tools:

1. **Microsoft Visio** - Professional network diagrams
2. **LibreOffice Draw** - Free alternative to Visio
3. **Inkscape** - Free vector graphics editor
4. **GIMP** - Free image editor for simple diagrams

### Quick Creation Tips:

- Use basic shapes (rectangles, circles, lines)
- Keep colors simple (2-3 colors max)
- Use consistent fonts and sizes
- Label everything clearly
- Save as PNG or SVG for web use
