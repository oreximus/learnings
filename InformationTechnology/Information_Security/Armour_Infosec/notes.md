### Comprehensive Network & Information Security Notes

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

### Wireless Network Types

#### WLAN (Wireless LAN)

- **Device**: Wi-Fi Router
- **Range**: 20m - 50m
- **Use**: Home and small office wireless networks

#### WPAN (Wireless Personal Area Network)

- **Device**: Bluetooth, Zigbee
- **Range**: Up to 10 meters
- **Use**: Short-range connectivity for personal devices

#### WMAN (Wireless MAN)

- **Device**: WiMAX, Wi-Fi CPE (Customer Premises Equipment)
- **Range**: Up to 50 km
- **Use**: Wireless internet service providers

#### WWAN (Wireless WAN)

- **Device**: Cell towers, satellites
- **Range**: 15km - thousands of kilometers
- **Use**: Cellular networks, IoT devices, satellite internet

---

## IP Addressing

### What is an IP Address?

An **IP Address** (Internet Protocol Address) is a unique numerical identifier assigned to every device on a network. Think of it as a postal address for your device on the internet.

### IP Versions

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

#### Class A (1.0.0.0 to 126.255.255.255)

- **Binary Pattern**: 0XXXXXXX.XXXXXXXX.XXXXXXXX.XXXXXXXX
- **Format**: N.H.H.H (Network.Host.Host.Host)
- **Default Subnet Mask**: 255.0.0.0 (/8)
- **Networks**: 126 (2^7 - 2, excluding 0 and 127)
- **Hosts per Network**: 16,777,214 (2^24 - 2)
- **Use**: Large organizations, ISPs, governments
- **Example**: 10.0.0.0 (private), 8.8.8.8 (Google DNS)

#### Class B (128.0.0.0 to 191.255.255.255)

- **Binary Pattern**: 10XXXXXX.XXXXXXXX.XXXXXXXX.XXXXXXXX
- **Format**: N.N.H.H (Network.Network.Host.Host)
- **Default Subnet Mask**: 255.255.0.0 (/16)
- **Networks**: 16,384 (2^14)
- **Hosts per Network**: 65,534 (2^16 - 2)
- **Use**: Medium to large organizations
- **Example**: 172.16.0.0 (private), 128.0.0.1

#### Class C (192.0.0.0 to 223.255.255.255)

- **Binary Pattern**: 110XXXXX.XXXXXXXX.XXXXXXXX.XXXXXXXX
- **Format**: N.N.N.H (Network.Network.Network.Host)
- **Default Subnet Mask**: 255.255.255.0 (/24)
- **Networks**: 2,097,152 (2^21)
- **Hosts per Network**: 254 (2^8 - 2)
- **Use**: Small organizations, home networks
- **Example**: 192.168.1.0 (private), 8.8.4.4

#### Class D (224.0.0.0 to 239.255.255.255)

- **Binary Pattern**: 1110XXXX.XXXXXXXX.XXXXXXXX.XXXXXXXX
- **Use**: Multicast addressing
- **Note**: Not used for regular host addressing

#### Class E (240.0.0.0 to 255.255.255.255)

- **Binary Pattern**: 1111XXXX.XXXXXXXX.XXXXXXXX.XXXXXXXX
- **Use**: Reserved for experimental purposes
- **Note**: Not used for regular addressing

### Public vs Private IP Addresses

#### Public IP Addresses

- **Definition**: Globally unique addresses assigned by ISPs
- **Routable**: Can communicate directly over the internet
- **Assignment**: Managed by IANA → Regional Registries → ISPs
- **Cost**: Usually costs money from ISP
- **Example**: Your home's external IP address

#### Private IP Addresses

- **Definition**: Used within private networks, not routable on internet
- **Purpose**: Solve IPv4 address shortage
- **Reserved Ranges**:

- **Class A**: 10.0.0.0 to 10.255.255.255
- **Class B**: 172.16.0.0 to 172.31.255.255
- **Class C**: 192.168.0.0 to 192.168.255.255
- **Link-Local**: 169.254.0.0 to 169.254.255.255 (APIPA)
- **Carrier-Grade NAT**: 100.64.0.0 to 100.127.255.255

#### Special IP Addresses

- **Loopback**: 127.0.0.1 to 127.255.255.255 (localhost)
- **Broadcast**: Last address in any network (e.g., 192.168.1.255)
- **Network Address**: First address in any network (e.g., 192.168.1.0)

### IANA Hierarchy

```mermaid
IANA IP Address Distribution Hierarchy.download-icon {
            cursor: pointer;
            transform-origin: center;
        }
        .download-icon .arrow-part {
            transition: transform 0.35s cubic-bezier(0.35, 0.2, 0.14, 0.95);
             transform-origin: center;
        }
        button:has(.download-icon):hover .download-icon .arrow-part, button:has(.download-icon):focus-visible .download-icon .arrow-part {
          transform: translateY(-1.5px);
        }
        #mermaid-diagram-r1ql{font-family:var(--font-geist-sans);font-size:12px;fill:#000000;}#mermaid-diagram-r1ql .error-icon{fill:#552222;}#mermaid-diagram-r1ql .error-text{fill:#552222;stroke:#552222;}#mermaid-diagram-r1ql .edge-thickness-normal{stroke-width:1px;}#mermaid-diagram-r1ql .edge-thickness-thick{stroke-width:3.5px;}#mermaid-diagram-r1ql .edge-pattern-solid{stroke-dasharray:0;}#mermaid-diagram-r1ql .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-diagram-r1ql .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-diagram-r1ql .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-diagram-r1ql .marker{fill:#666;stroke:#666;}#mermaid-diagram-r1ql .marker.cross{stroke:#666;}#mermaid-diagram-r1ql svg{font-family:var(--font-geist-sans);font-size:12px;}#mermaid-diagram-r1ql p{margin:0;}#mermaid-diagram-r1ql .label{font-family:var(--font-geist-sans);color:#000000;}#mermaid-diagram-r1ql .cluster-label text{fill:#333;}#mermaid-diagram-r1ql .cluster-label span{color:#333;}#mermaid-diagram-r1ql .cluster-label span p{background-color:transparent;}#mermaid-diagram-r1ql .label text,#mermaid-diagram-r1ql span{fill:#000000;color:#000000;}#mermaid-diagram-r1ql .node rect,#mermaid-diagram-r1ql .node circle,#mermaid-diagram-r1ql .node ellipse,#mermaid-diagram-r1ql .node polygon,#mermaid-diagram-r1ql .node path{fill:#eee;stroke:#999;stroke-width:1px;}#mermaid-diagram-r1ql .rough-node .label text,#mermaid-diagram-r1ql .node .label text{text-anchor:middle;}#mermaid-diagram-r1ql .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-diagram-r1ql .node .label{text-align:center;}#mermaid-diagram-r1ql .node.clickable{cursor:pointer;}#mermaid-diagram-r1ql .arrowheadPath{fill:#333333;}#mermaid-diagram-r1ql .edgePath .path{stroke:#666;stroke-width:2.0px;}#mermaid-diagram-r1ql .flowchart-link{stroke:#666;fill:none;}#mermaid-diagram-r1ql .edgeLabel{background-color:white;text-align:center;}#mermaid-diagram-r1ql .edgeLabel p{background-color:white;}#mermaid-diagram-r1ql .edgeLabel rect{opacity:0.5;background-color:white;fill:white;}#mermaid-diagram-r1ql .labelBkg{background-color:rgba(255, 255, 255, 0.5);}#mermaid-diagram-r1ql .cluster rect{fill:hsl(0, 0%, 98.9215686275%);stroke:#707070;stroke-width:1px;}#mermaid-diagram-r1ql .cluster text{fill:#333;}#mermaid-diagram-r1ql .cluster span{color:#333;}#mermaid-diagram-r1ql div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:var(--font-geist-sans);font-size:12px;background:hsl(-160, 0%, 93.3333333333%);border:1px solid #707070;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-diagram-r1ql .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#000000;}#mermaid-diagram-r1ql .flowchart-link{stroke:hsl(var(--gray-400));stroke-width:1px;}#mermaid-diagram-r1ql .marker,#mermaid-diagram-r1ql marker,#mermaid-diagram-r1ql marker *{fill:hsl(var(--gray-400))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r1ql .label,#mermaid-diagram-r1ql text,#mermaid-diagram-r1ql text>tspan{fill:hsl(var(--black))!important;color:hsl(var(--black))!important;}#mermaid-diagram-r1ql .background,#mermaid-diagram-r1ql rect.relationshipLabelBox{fill:hsl(var(--white))!important;}#mermaid-diagram-r1ql .entityBox,#mermaid-diagram-r1ql .attributeBoxEven{fill:hsl(var(--gray-150))!important;}#mermaid-diagram-r1ql .attributeBoxOdd{fill:hsl(var(--white))!important;}#mermaid-diagram-r1ql .label-container,#mermaid-diagram-r1ql rect.actor{fill:hsl(var(--white))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r1ql line{stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r1ql :root{--mermaid-font-family:var(--font-geist-sans);}IANA(Internet Assigned NumbersAuthority)Global CoordinationRegional Internet Registries(RIRs)ARIN(North America)RIPE NCC(Europe, Middle East)APNIC(Asia Pacific)LACNIC(Latin America)AFRINIC(Africa)National Registries&amp; ISPsEnd Users(Organizations &amp; Individuals)
```

### Network Communication Process

```mermaid
Network Communication Flow.download-icon {
            cursor: pointer;
            transform-origin: center;
        }
        .download-icon .arrow-part {
            transition: transform 0.35s cubic-bezier(0.35, 0.2, 0.14, 0.95);
             transform-origin: center;
        }
        button:has(.download-icon):hover .download-icon .arrow-part, button:has(.download-icon):focus-visible .download-icon .arrow-part {
          transform: translateY(-1.5px);
        }
        Device B(Different Network)InternetRouter/Gateway(192.168.1.1)SwitchDevice A(192.168.1.10)Device B(Different Network)InternetRouter/Gateway(192.168.1.1)SwitchDevice A(192.168.1.10)#mermaid-diagram-r1qr{font-family:var(--font-geist-sans);font-size:12px;fill:#000000;}#mermaid-diagram-r1qr .error-icon{fill:#552222;}#mermaid-diagram-r1qr .error-text{fill:#552222;stroke:#552222;}#mermaid-diagram-r1qr .edge-thickness-normal{stroke-width:1px;}#mermaid-diagram-r1qr .edge-thickness-thick{stroke-width:3.5px;}#mermaid-diagram-r1qr .edge-pattern-solid{stroke-dasharray:0;}#mermaid-diagram-r1qr .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-diagram-r1qr .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-diagram-r1qr .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-diagram-r1qr .marker{fill:#666;stroke:#666;}#mermaid-diagram-r1qr .marker.cross{stroke:#666;}#mermaid-diagram-r1qr svg{font-family:var(--font-geist-sans);font-size:12px;}#mermaid-diagram-r1qr p{margin:0;}#mermaid-diagram-r1qr .actor{stroke:hsl(0, 0%, 83%);fill:#eee;}#mermaid-diagram-r1qr text.actor>tspan{fill:#333;stroke:none;}#mermaid-diagram-r1qr .actor-line{stroke:hsl(0, 0%, 83%);}#mermaid-diagram-r1qr .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-diagram-r1qr .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-diagram-r1qr #arrowhead path{fill:#333;stroke:#333;}#mermaid-diagram-r1qr .sequenceNumber{fill:white;}#mermaid-diagram-r1qr #sequencenumber{fill:#333;}#mermaid-diagram-r1qr #crosshead path{fill:#333;stroke:#333;}#mermaid-diagram-r1qr .messageText{fill:#333;stroke:none;}#mermaid-diagram-r1qr .labelBox{stroke:hsl(0, 0%, 83%);fill:#eee;}#mermaid-diagram-r1qr .labelText,#mermaid-diagram-r1qr .labelText>tspan{fill:#333;stroke:none;}#mermaid-diagram-r1qr .loopText,#mermaid-diagram-r1qr .loopText>tspan{fill:#333;stroke:none;}#mermaid-diagram-r1qr .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(0, 0%, 83%);fill:hsl(0, 0%, 83%);}#mermaid-diagram-r1qr .note{stroke:#999;fill:#666;}#mermaid-diagram-r1qr .noteText,#mermaid-diagram-r1qr .noteText>tspan{fill:#fff;stroke:none;}#mermaid-diagram-r1qr .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-diagram-r1qr .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-diagram-r1qr .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-diagram-r1qr .actorPopupMenu{position:absolute;}#mermaid-diagram-r1qr .actorPopupMenuPanel{position:absolute;fill:#eee;box-shadow:0px 8px 16px 0px rgba(0,0,0,0.2);filter:drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));}#mermaid-diagram-r1qr .actor-man line{stroke:hsl(0, 0%, 83%);fill:#eee;}#mermaid-diagram-r1qr .actor-man circle,#mermaid-diagram-r1qr line{stroke:hsl(0, 0%, 83%);fill:#eee;stroke-width:2px;}#mermaid-diagram-r1qr .flowchart-link{stroke:hsl(var(--gray-400));stroke-width:1px;}#mermaid-diagram-r1qr .marker,#mermaid-diagram-r1qr marker,#mermaid-diagram-r1qr marker *{fill:hsl(var(--gray-400))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r1qr .label,#mermaid-diagram-r1qr text,#mermaid-diagram-r1qr text>tspan{fill:hsl(var(--black))!important;color:hsl(var(--black))!important;}#mermaid-diagram-r1qr .background,#mermaid-diagram-r1qr rect.relationshipLabelBox{fill:hsl(var(--white))!important;}#mermaid-diagram-r1qr .entityBox,#mermaid-diagram-r1qr .attributeBoxEven{fill:hsl(var(--gray-150))!important;}#mermaid-diagram-r1qr .attributeBoxOdd{fill:hsl(var(--white))!important;}#mermaid-diagram-r1qr .label-container,#mermaid-diagram-r1qr rect.actor{fill:hsl(var(--white))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r1qr line{stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r1qr :root{--mermaid-font-family:var(--font-geist-sans);}Same Network CommunicationDifferent Network CommunicationPacket to 192.168.1.20Direct delivery (same subnet)Packet to 8.8.8.8Forward packet (NAT applied)Response packetDeliver response (NAT reversed)
```

---

## Subnetting & CIDR

### Subnet Mask

A **subnet mask** determines which portion of an IP address represents the network and which represents the host.

#### Structure

- **32-bit address** like IP address
- **Network bits**: Set to 1 (binary)
- **Host bits**: Set to 0 (binary)
- **Representation**: Dotted decimal or CIDR notation

#### Examples

- **Class A**: 255.0.0.0 = /8
- **Class B**: 255.255.0.0 = /16
- **Class C**: 255.255.255.0 = /24

### Subnetting Process

#### Why Subnet?

- **Efficient IP usage**: Divide large networks into smaller ones
- **Improved performance**: Reduce broadcast domains
- **Better security**: Isolate network segments
- **Easier management**: Organize by department/function

#### Subnetting Example

**Original Network**: 192.168.1.0/24 (254 hosts)
**Requirement**: 4 subnets with ~60 hosts each

**Solution**: Use /26 (255.255.255.192)

- **Subnet 1**: 192.168.1.0/26 (192.168.1.1 - 192.168.1.62)
- **Subnet 2**: 192.168.1.64/26 (192.168.1.65 - 192.168.1.126)
- **Subnet 3**: 192.168.1.128/26 (192.168.1.129 - 192.168.1.190)
- **Subnet 4**: 192.168.1.192/26 (192.168.1.193 - 192.168.1.254)

### CIDR (Classless Inter-Domain Routing)

- **Purpose**: More flexible IP allocation than classful addressing
- **Notation**: IP/prefix (e.g., 192.168.1.0/24)
- **Benefits**: Reduces routing table size, more efficient IP usage

---

## Network Devices & Topologies

### Network Devices

#### Hub (Legacy)

- **Layer**: Physical (Layer 1)
- **Function**: Simple signal repeater
- **Collision Domain**: Single collision domain
- **Duplex**: Half-duplex only
- **Status**: Largely obsolete

#### Switch

- **Layer**: Data Link (Layer 2)
- **Function**: Frame switching based on MAC addresses
- **Collision Domain**: Each port = separate collision domain
- **Duplex**: Full-duplex capable
- **Features**: MAC address learning, VLAN support

#### Router

- **Layer**: Network (Layer 3)
- **Function**: Packet routing between different networks
- **Features**: NAT, DHCP, firewall capabilities
- **Use**: Connect different network segments

#### Access Point (AP)

- **Function**: Provides wireless connectivity
- **Modes**: Autonomous or controller-based
- **Standards**: 802.11a/b/g/n/ac/ax (Wi-Fi 6)

### Network Topologies

#### Star Topology

```mermaid
Star Topology - Central Hub/Switch.download-icon {
            cursor: pointer;
            transform-origin: center;
        }
        .download-icon .arrow-part {
            transition: transform 0.35s cubic-bezier(0.35, 0.2, 0.14, 0.95);
             transform-origin: center;
        }
        button:has(.download-icon):hover .download-icon .arrow-part, button:has(.download-icon):focus-visible .download-icon .arrow-part {
          transform: translateY(-1.5px);
        }
        #mermaid-diagram-r255{font-family:var(--font-geist-sans);font-size:12px;fill:#000000;}#mermaid-diagram-r255 .error-icon{fill:#552222;}#mermaid-diagram-r255 .error-text{fill:#552222;stroke:#552222;}#mermaid-diagram-r255 .edge-thickness-normal{stroke-width:1px;}#mermaid-diagram-r255 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-diagram-r255 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-diagram-r255 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-diagram-r255 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-diagram-r255 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-diagram-r255 .marker{fill:#666;stroke:#666;}#mermaid-diagram-r255 .marker.cross{stroke:#666;}#mermaid-diagram-r255 svg{font-family:var(--font-geist-sans);font-size:12px;}#mermaid-diagram-r255 p{margin:0;}#mermaid-diagram-r255 .label{font-family:var(--font-geist-sans);color:#000000;}#mermaid-diagram-r255 .cluster-label text{fill:#333;}#mermaid-diagram-r255 .cluster-label span{color:#333;}#mermaid-diagram-r255 .cluster-label span p{background-color:transparent;}#mermaid-diagram-r255 .label text,#mermaid-diagram-r255 span{fill:#000000;color:#000000;}#mermaid-diagram-r255 .node rect,#mermaid-diagram-r255 .node circle,#mermaid-diagram-r255 .node ellipse,#mermaid-diagram-r255 .node polygon,#mermaid-diagram-r255 .node path{fill:#eee;stroke:#999;stroke-width:1px;}#mermaid-diagram-r255 .rough-node .label text,#mermaid-diagram-r255 .node .label text{text-anchor:middle;}#mermaid-diagram-r255 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-diagram-r255 .node .label{text-align:center;}#mermaid-diagram-r255 .node.clickable{cursor:pointer;}#mermaid-diagram-r255 .arrowheadPath{fill:#333333;}#mermaid-diagram-r255 .edgePath .path{stroke:#666;stroke-width:2.0px;}#mermaid-diagram-r255 .flowchart-link{stroke:#666;fill:none;}#mermaid-diagram-r255 .edgeLabel{background-color:white;text-align:center;}#mermaid-diagram-r255 .edgeLabel p{background-color:white;}#mermaid-diagram-r255 .edgeLabel rect{opacity:0.5;background-color:white;fill:white;}#mermaid-diagram-r255 .labelBkg{background-color:rgba(255, 255, 255, 0.5);}#mermaid-diagram-r255 .cluster rect{fill:hsl(0, 0%, 98.9215686275%);stroke:#707070;stroke-width:1px;}#mermaid-diagram-r255 .cluster text{fill:#333;}#mermaid-diagram-r255 .cluster span{color:#333;}#mermaid-diagram-r255 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:var(--font-geist-sans);font-size:12px;background:hsl(-160, 0%, 93.3333333333%);border:1px solid #707070;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-diagram-r255 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#000000;}#mermaid-diagram-r255 .flowchart-link{stroke:hsl(var(--gray-400));stroke-width:1px;}#mermaid-diagram-r255 .marker,#mermaid-diagram-r255 marker,#mermaid-diagram-r255 marker *{fill:hsl(var(--gray-400))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r255 .label,#mermaid-diagram-r255 text,#mermaid-diagram-r255 text>tspan{fill:hsl(var(--black))!important;color:hsl(var(--black))!important;}#mermaid-diagram-r255 .background,#mermaid-diagram-r255 rect.relationshipLabelBox{fill:hsl(var(--white))!important;}#mermaid-diagram-r255 .entityBox,#mermaid-diagram-r255 .attributeBoxEven{fill:hsl(var(--gray-150))!important;}#mermaid-diagram-r255 .attributeBoxOdd{fill:hsl(var(--white))!important;}#mermaid-diagram-r255 .label-container,#mermaid-diagram-r255 rect.actor{fill:hsl(var(--white))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r255 line{stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r255 :root{--mermaid-font-family:var(--font-geist-sans);}Central Switch192.168.1.1PC1192.168.1.10PC2192.168.1.11PC3192.168.1.12PC4192.168.1.13Server192.168.1.100Printer192.168.1.200
```

**Advantages**: Easy troubleshooting, centralized management, failure isolation
**Disadvantages**: Single point of failure (central device), requires more cable
**Use**: Most common in modern LANs

#### Bus Topology

```mermaid
Bus Topology - Shared Communication Line.download-icon {
            cursor: pointer;
            transform-origin: center;
        }
        .download-icon .arrow-part {
            transition: transform 0.35s cubic-bezier(0.35, 0.2, 0.14, 0.95);
             transform-origin: center;
        }
        button:has(.download-icon):hover .download-icon .arrow-part, button:has(.download-icon):focus-visible .download-icon .arrow-part {
          transform: translateY(-1.5px);
        }
        #mermaid-diagram-r25r{font-family:var(--font-geist-sans);font-size:12px;fill:#000000;}#mermaid-diagram-r25r .error-icon{fill:#552222;}#mermaid-diagram-r25r .error-text{fill:#552222;stroke:#552222;}#mermaid-diagram-r25r .edge-thickness-normal{stroke-width:1px;}#mermaid-diagram-r25r .edge-thickness-thick{stroke-width:3.5px;}#mermaid-diagram-r25r .edge-pattern-solid{stroke-dasharray:0;}#mermaid-diagram-r25r .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-diagram-r25r .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-diagram-r25r .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-diagram-r25r .marker{fill:#666;stroke:#666;}#mermaid-diagram-r25r .marker.cross{stroke:#666;}#mermaid-diagram-r25r svg{font-family:var(--font-geist-sans);font-size:12px;}#mermaid-diagram-r25r p{margin:0;}#mermaid-diagram-r25r .label{font-family:var(--font-geist-sans);color:#000000;}#mermaid-diagram-r25r .cluster-label text{fill:#333;}#mermaid-diagram-r25r .cluster-label span{color:#333;}#mermaid-diagram-r25r .cluster-label span p{background-color:transparent;}#mermaid-diagram-r25r .label text,#mermaid-diagram-r25r span{fill:#000000;color:#000000;}#mermaid-diagram-r25r .node rect,#mermaid-diagram-r25r .node circle,#mermaid-diagram-r25r .node ellipse,#mermaid-diagram-r25r .node polygon,#mermaid-diagram-r25r .node path{fill:#eee;stroke:#999;stroke-width:1px;}#mermaid-diagram-r25r .rough-node .label text,#mermaid-diagram-r25r .node .label text{text-anchor:middle;}#mermaid-diagram-r25r .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-diagram-r25r .node .label{text-align:center;}#mermaid-diagram-r25r .node.clickable{cursor:pointer;}#mermaid-diagram-r25r .arrowheadPath{fill:#333333;}#mermaid-diagram-r25r .edgePath .path{stroke:#666;stroke-width:2.0px;}#mermaid-diagram-r25r .flowchart-link{stroke:#666;fill:none;}#mermaid-diagram-r25r .edgeLabel{background-color:white;text-align:center;}#mermaid-diagram-r25r .edgeLabel p{background-color:white;}#mermaid-diagram-r25r .edgeLabel rect{opacity:0.5;background-color:white;fill:white;}#mermaid-diagram-r25r .labelBkg{background-color:rgba(255, 255, 255, 0.5);}#mermaid-diagram-r25r .cluster rect{fill:hsl(0, 0%, 98.9215686275%);stroke:#707070;stroke-width:1px;}#mermaid-diagram-r25r .cluster text{fill:#333;}#mermaid-diagram-r25r .cluster span{color:#333;}#mermaid-diagram-r25r div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:var(--font-geist-sans);font-size:12px;background:hsl(-160, 0%, 93.3333333333%);border:1px solid #707070;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-diagram-r25r .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#000000;}#mermaid-diagram-r25r .flowchart-link{stroke:hsl(var(--gray-400));stroke-width:1px;}#mermaid-diagram-r25r .marker,#mermaid-diagram-r25r marker,#mermaid-diagram-r25r marker *{fill:hsl(var(--gray-400))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r25r .label,#mermaid-diagram-r25r text,#mermaid-diagram-r25r text>tspan{fill:hsl(var(--black))!important;color:hsl(var(--black))!important;}#mermaid-diagram-r25r .background,#mermaid-diagram-r25r rect.relationshipLabelBox{fill:hsl(var(--white))!important;}#mermaid-diagram-r25r .entityBox,#mermaid-diagram-r25r .attributeBoxEven{fill:hsl(var(--gray-150))!important;}#mermaid-diagram-r25r .attributeBoxOdd{fill:hsl(var(--white))!important;}#mermaid-diagram-r25r .label-container,#mermaid-diagram-r25r rect.actor{fill:hsl(var(--white))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r25r line{stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r25r :root{--mermaid-font-family:var(--font-geist-sans);}TerminatorPC1PC2PC3PC4Terminator
```

**Advantages**: Simple, cost-effective for small networks, minimal cable required
**Disadvantages**: Difficult troubleshooting, single point of failure, collision domain
**Use**: Legacy networks, some industrial applications

#### Ring Topology

```mermaid
Ring Topology - Circular Data Flow.download-icon {
            cursor: pointer;
            transform-origin: center;
        }
        .download-icon .arrow-part {
            transition: transform 0.35s cubic-bezier(0.35, 0.2, 0.14, 0.95);
             transform-origin: center;
        }
        button:has(.download-icon):hover .download-icon .arrow-part, button:has(.download-icon):focus-visible .download-icon .arrow-part {
          transform: translateY(-1.5px);
        }
        #mermaid-diagram-r26h{font-family:var(--font-geist-sans);font-size:12px;fill:#000000;}#mermaid-diagram-r26h .error-icon{fill:#552222;}#mermaid-diagram-r26h .error-text{fill:#552222;stroke:#552222;}#mermaid-diagram-r26h .edge-thickness-normal{stroke-width:1px;}#mermaid-diagram-r26h .edge-thickness-thick{stroke-width:3.5px;}#mermaid-diagram-r26h .edge-pattern-solid{stroke-dasharray:0;}#mermaid-diagram-r26h .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-diagram-r26h .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-diagram-r26h .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-diagram-r26h .marker{fill:#666;stroke:#666;}#mermaid-diagram-r26h .marker.cross{stroke:#666;}#mermaid-diagram-r26h svg{font-family:var(--font-geist-sans);font-size:12px;}#mermaid-diagram-r26h p{margin:0;}#mermaid-diagram-r26h .label{font-family:var(--font-geist-sans);color:#000000;}#mermaid-diagram-r26h .cluster-label text{fill:#333;}#mermaid-diagram-r26h .cluster-label span{color:#333;}#mermaid-diagram-r26h .cluster-label span p{background-color:transparent;}#mermaid-diagram-r26h .label text,#mermaid-diagram-r26h span{fill:#000000;color:#000000;}#mermaid-diagram-r26h .node rect,#mermaid-diagram-r26h .node circle,#mermaid-diagram-r26h .node ellipse,#mermaid-diagram-r26h .node polygon,#mermaid-diagram-r26h .node path{fill:#eee;stroke:#999;stroke-width:1px;}#mermaid-diagram-r26h .rough-node .label text,#mermaid-diagram-r26h .node .label text{text-anchor:middle;}#mermaid-diagram-r26h .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-diagram-r26h .node .label{text-align:center;}#mermaid-diagram-r26h .node.clickable{cursor:pointer;}#mermaid-diagram-r26h .arrowheadPath{fill:#333333;}#mermaid-diagram-r26h .edgePath .path{stroke:#666;stroke-width:2.0px;}#mermaid-diagram-r26h .flowchart-link{stroke:#666;fill:none;}#mermaid-diagram-r26h .edgeLabel{background-color:white;text-align:center;}#mermaid-diagram-r26h .edgeLabel p{background-color:white;}#mermaid-diagram-r26h .edgeLabel rect{opacity:0.5;background-color:white;fill:white;}#mermaid-diagram-r26h .labelBkg{background-color:rgba(255, 255, 255, 0.5);}#mermaid-diagram-r26h .cluster rect{fill:hsl(0, 0%, 98.9215686275%);stroke:#707070;stroke-width:1px;}#mermaid-diagram-r26h .cluster text{fill:#333;}#mermaid-diagram-r26h .cluster span{color:#333;}#mermaid-diagram-r26h div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:var(--font-geist-sans);font-size:12px;background:hsl(-160, 0%, 93.3333333333%);border:1px solid #707070;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-diagram-r26h .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#000000;}#mermaid-diagram-r26h .flowchart-link{stroke:hsl(var(--gray-400));stroke-width:1px;}#mermaid-diagram-r26h .marker,#mermaid-diagram-r26h marker,#mermaid-diagram-r26h marker *{fill:hsl(var(--gray-400))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r26h .label,#mermaid-diagram-r26h text,#mermaid-diagram-r26h text>tspan{fill:hsl(var(--black))!important;color:hsl(var(--black))!important;}#mermaid-diagram-r26h .background,#mermaid-diagram-r26h rect.relationshipLabelBox{fill:hsl(var(--white))!important;}#mermaid-diagram-r26h .entityBox,#mermaid-diagram-r26h .attributeBoxEven{fill:hsl(var(--gray-150))!important;}#mermaid-diagram-r26h .attributeBoxOdd{fill:hsl(var(--white))!important;}#mermaid-diagram-r26h .label-container,#mermaid-diagram-r26h rect.actor{fill:hsl(var(--white))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r26h line{stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r26h :root{--mermaid-font-family:var(--font-geist-sans);}PC1PC2PC3PC4PC5
```

**Advantages**: Predictable performance, no collisions, equal access
**Disadvantages**: Failure of one device affects entire network, difficult to troubleshoot
**Use**: Token Ring networks (legacy), some fiber optic networks

#### Mesh Topology

```mermaid
Full Mesh Topology - All-to-All Connections.download-icon {
            cursor: pointer;
            transform-origin: center;
        }
        .download-icon .arrow-part {
            transition: transform 0.35s cubic-bezier(0.35, 0.2, 0.14, 0.95);
             transform-origin: center;
        }
        button:has(.download-icon):hover .download-icon .arrow-part, button:has(.download-icon):focus-visible .download-icon .arrow-part {
          transform: translateY(-1.5px);
        }
        #mermaid-diagram-r277{font-family:var(--font-geist-sans);font-size:12px;fill:#000000;}#mermaid-diagram-r277 .error-icon{fill:#552222;}#mermaid-diagram-r277 .error-text{fill:#552222;stroke:#552222;}#mermaid-diagram-r277 .edge-thickness-normal{stroke-width:1px;}#mermaid-diagram-r277 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-diagram-r277 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-diagram-r277 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-diagram-r277 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-diagram-r277 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-diagram-r277 .marker{fill:#666;stroke:#666;}#mermaid-diagram-r277 .marker.cross{stroke:#666;}#mermaid-diagram-r277 svg{font-family:var(--font-geist-sans);font-size:12px;}#mermaid-diagram-r277 p{margin:0;}#mermaid-diagram-r277 .label{font-family:var(--font-geist-sans);color:#000000;}#mermaid-diagram-r277 .cluster-label text{fill:#333;}#mermaid-diagram-r277 .cluster-label span{color:#333;}#mermaid-diagram-r277 .cluster-label span p{background-color:transparent;}#mermaid-diagram-r277 .label text,#mermaid-diagram-r277 span{fill:#000000;color:#000000;}#mermaid-diagram-r277 .node rect,#mermaid-diagram-r277 .node circle,#mermaid-diagram-r277 .node ellipse,#mermaid-diagram-r277 .node polygon,#mermaid-diagram-r277 .node path{fill:#eee;stroke:#999;stroke-width:1px;}#mermaid-diagram-r277 .rough-node .label text,#mermaid-diagram-r277 .node .label text{text-anchor:middle;}#mermaid-diagram-r277 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-diagram-r277 .node .label{text-align:center;}#mermaid-diagram-r277 .node.clickable{cursor:pointer;}#mermaid-diagram-r277 .arrowheadPath{fill:#333333;}#mermaid-diagram-r277 .edgePath .path{stroke:#666;stroke-width:2.0px;}#mermaid-diagram-r277 .flowchart-link{stroke:#666;fill:none;}#mermaid-diagram-r277 .edgeLabel{background-color:white;text-align:center;}#mermaid-diagram-r277 .edgeLabel p{background-color:white;}#mermaid-diagram-r277 .edgeLabel rect{opacity:0.5;background-color:white;fill:white;}#mermaid-diagram-r277 .labelBkg{background-color:rgba(255, 255, 255, 0.5);}#mermaid-diagram-r277 .cluster rect{fill:hsl(0, 0%, 98.9215686275%);stroke:#707070;stroke-width:1px;}#mermaid-diagram-r277 .cluster text{fill:#333;}#mermaid-diagram-r277 .cluster span{color:#333;}#mermaid-diagram-r277 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:var(--font-geist-sans);font-size:12px;background:hsl(-160, 0%, 93.3333333333%);border:1px solid #707070;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-diagram-r277 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#000000;}#mermaid-diagram-r277 .flowchart-link{stroke:hsl(var(--gray-400));stroke-width:1px;}#mermaid-diagram-r277 .marker,#mermaid-diagram-r277 marker,#mermaid-diagram-r277 marker *{fill:hsl(var(--gray-400))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r277 .label,#mermaid-diagram-r277 text,#mermaid-diagram-r277 text>tspan{fill:hsl(var(--black))!important;color:hsl(var(--black))!important;}#mermaid-diagram-r277 .background,#mermaid-diagram-r277 rect.relationshipLabelBox{fill:hsl(var(--white))!important;}#mermaid-diagram-r277 .entityBox,#mermaid-diagram-r277 .attributeBoxEven{fill:hsl(var(--gray-150))!important;}#mermaid-diagram-r277 .attributeBoxOdd{fill:hsl(var(--white))!important;}#mermaid-diagram-r277 .label-container,#mermaid-diagram-r277 rect.actor{fill:hsl(var(--white))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r277 line{stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r277 :root{--mermaid-font-family:var(--font-geist-sans);}Router ASite 1Router BSite 2Router CSite 3Router DSite 4
```

**Advantages**: High redundancy, excellent fault tolerance, multiple paths
**Disadvantages**: Expensive, complex configuration, many connections required
**Use**: Critical infrastructure, WAN connections, data centers

### MAC Addresses

#### Structure

- **Size**: 48-bit (6 bytes) address
- **Format**: XX:XX:XX:XX:XX:XX (hexadecimal)
- **Parts**:

- **OUI** (First 24 bits): Organizationally Unique Identifier (manufacturer)
- **NIC** (Last 24 bits): Network Interface Controller specific

#### Characteristics

- **Uniqueness**: Burned into network interface during manufacturing
- **Scope**: Unique within Layer 2 broadcast domain
- **Types**: Unicast, Multicast, Broadcast
- **Spoofing**: Can be changed via software

---

## DHCP & Network Services

### DHCP (Dynamic Host Configuration Protocol)

#### Purpose

Automatically assigns IP configuration to network devices, eliminating manual configuration.

#### DORA Process

```mermaid
DHCP DORA Process.download-icon {
            cursor: pointer;
            transform-origin: center;
        }
        .download-icon .arrow-part {
            transition: transform 0.35s cubic-bezier(0.35, 0.2, 0.14, 0.95);
             transform-origin: center;
        }
        button:has(.download-icon):hover .download-icon .arrow-part, button:has(.download-icon):focus-visible .download-icon .arrow-part {
          transform: translateY(-1.5px);
        }
        DHCP Server(192.168.1.1)DHCP Client(New Device)DHCP Server(192.168.1.1)DHCP Client(New Device)#mermaid-diagram-r2aj{font-family:var(--font-geist-sans);font-size:12px;fill:#000000;}#mermaid-diagram-r2aj .error-icon{fill:#552222;}#mermaid-diagram-r2aj .error-text{fill:#552222;stroke:#552222;}#mermaid-diagram-r2aj .edge-thickness-normal{stroke-width:1px;}#mermaid-diagram-r2aj .edge-thickness-thick{stroke-width:3.5px;}#mermaid-diagram-r2aj .edge-pattern-solid{stroke-dasharray:0;}#mermaid-diagram-r2aj .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-diagram-r2aj .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-diagram-r2aj .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-diagram-r2aj .marker{fill:#666;stroke:#666;}#mermaid-diagram-r2aj .marker.cross{stroke:#666;}#mermaid-diagram-r2aj svg{font-family:var(--font-geist-sans);font-size:12px;}#mermaid-diagram-r2aj p{margin:0;}#mermaid-diagram-r2aj .actor{stroke:hsl(0, 0%, 83%);fill:#eee;}#mermaid-diagram-r2aj text.actor>tspan{fill:#333;stroke:none;}#mermaid-diagram-r2aj .actor-line{stroke:hsl(0, 0%, 83%);}#mermaid-diagram-r2aj .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-diagram-r2aj .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-diagram-r2aj #arrowhead path{fill:#333;stroke:#333;}#mermaid-diagram-r2aj .sequenceNumber{fill:white;}#mermaid-diagram-r2aj #sequencenumber{fill:#333;}#mermaid-diagram-r2aj #crosshead path{fill:#333;stroke:#333;}#mermaid-diagram-r2aj .messageText{fill:#333;stroke:none;}#mermaid-diagram-r2aj .labelBox{stroke:hsl(0, 0%, 83%);fill:#eee;}#mermaid-diagram-r2aj .labelText,#mermaid-diagram-r2aj .labelText>tspan{fill:#333;stroke:none;}#mermaid-diagram-r2aj .loopText,#mermaid-diagram-r2aj .loopText>tspan{fill:#333;stroke:none;}#mermaid-diagram-r2aj .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(0, 0%, 83%);fill:hsl(0, 0%, 83%);}#mermaid-diagram-r2aj .note{stroke:#999;fill:#666;}#mermaid-diagram-r2aj .noteText,#mermaid-diagram-r2aj .noteText>tspan{fill:#fff;stroke:none;}#mermaid-diagram-r2aj .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-diagram-r2aj .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-diagram-r2aj .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-diagram-r2aj .actorPopupMenu{position:absolute;}#mermaid-diagram-r2aj .actorPopupMenuPanel{position:absolute;fill:#eee;box-shadow:0px 8px 16px 0px rgba(0,0,0,0.2);filter:drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));}#mermaid-diagram-r2aj .actor-man line{stroke:hsl(0, 0%, 83%);fill:#eee;}#mermaid-diagram-r2aj .actor-man circle,#mermaid-diagram-r2aj line{stroke:hsl(0, 0%, 83%);fill:#eee;stroke-width:2px;}#mermaid-diagram-r2aj .flowchart-link{stroke:hsl(var(--gray-400));stroke-width:1px;}#mermaid-diagram-r2aj .marker,#mermaid-diagram-r2aj marker,#mermaid-diagram-r2aj marker *{fill:hsl(var(--gray-400))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r2aj .label,#mermaid-diagram-r2aj text,#mermaid-diagram-r2aj text>tspan{fill:hsl(var(--black))!important;color:hsl(var(--black))!important;}#mermaid-diagram-r2aj .background,#mermaid-diagram-r2aj rect.relationshipLabelBox{fill:hsl(var(--white))!important;}#mermaid-diagram-r2aj .entityBox,#mermaid-diagram-r2aj .attributeBoxEven{fill:hsl(var(--gray-150))!important;}#mermaid-diagram-r2aj .attributeBoxOdd{fill:hsl(var(--white))!important;}#mermaid-diagram-r2aj .label-container,#mermaid-diagram-r2aj rect.actor{fill:hsl(var(--white))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r2aj line{stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r2aj :root{--mermaid-font-family:var(--font-geist-sans);}1. DISCOVER Phase2. OFFER Phase3. REQUEST Phase4. ACKNOWLEDGE PhaseDHCP Discover (Broadcast)Source: 0.0.0.0Destination: 255.255.255.255DHCP OfferOffered IP: 192.168.1.100Lease Time: 24 hoursDHCP RequestRequesting: 192.168.1.100Server ID: 192.168.1.1DHCP ACKConfirmed: 192.168.1.100Gateway: 192.168.1.1DNS: 8.8.8.8
```

#### DHCP Configuration Elements

- **IP Address Pool**: Range of available IP addresses
- **Lease Time**: How long client can use IP address
- **Gateway**: Default route for clients
- **DNS Servers**: Name resolution servers
- **Subnet Mask**: Network configuration

#### DHCP Server Setup (Windows Server)

1. Install DHCP role via Server Manager
2. Configure scope (IP range)
3. Set lease duration
4. Configure options (gateway, DNS)
5. Activate scope

### NAT (Network Address Translation)

#### Purpose

Allows private IP addresses to communicate with public internet using public IP addresses.

#### Types

- **Static NAT**: One-to-one mapping
- **Dynamic NAT**: Pool of public IPs
- **PAT/NAPT**: Port Address Translation (most common)

#### Port Forwarding

Process of redirecting external requests to internal private network hosts.

---

## Operating Systems

### Linux

#### History & Philosophy

- **Created**: 1991 by Linus Torvalds
- **License**: GPL (General Public License)
- **Philosophy**: Open source, community-driven development

#### Key Features

- **Open Source**: Source code freely available
- **Multitasking**: Multiple processes simultaneously
- **Multiuser**: Multiple users can use system concurrently
- **Portability**: Runs on various hardware platforms
- **Security**: Robust permission system, frequent security updates
- **Stability**: High uptime, reliable performance
- **Performance**: Efficient resource utilization

#### Shell

The **shell** is the interface between user and kernel:

- **Purpose**: Interpret user commands and execute them
- **Types**: Bash, Zsh, Fish, etc.
- **Function**: Command interpreter and programming environment

#### Linux Distributions & Package Managers

##### Debian-Based Distributions

- **Base**: Debian (1993)
- **Package Format**: .deb
- **Package Manager**: apt, dpkg
- **Popular Derivatives**:

- **Ubuntu**: User-friendly, desktop-focused
- **Linux Mint**: Beginner-friendly
- **Kali Linux**: Security/penetration testing

##### Red Hat-Based Distributions

- **Base**: Red Hat Enterprise Linux (RHEL)
- **Package Format**: .rpm
- **Package Manager**: yum, dnf, rpm
- **Popular Derivatives**:

- **Fedora**: Testing ground for RHEL features
- **CentOS**: Free RHEL clone (now CentOS Stream)
- **Rocky Linux**: RHEL alternative

### Linux File System Structure

#### Root Directory (/)

The top-level directory containing all other directories.

#### Essential Directories

- **/bin**: Essential user commands (ls, cp, mv, cat)
- **/sbin**: System administration commands (init, fsck, reboot)
- **/lib**: Libraries for /bin and /sbin programs
- **/lib64**: 64-bit specific libraries
- **/etc**: System-wide configuration files
- **/dev**: Device files (hardware interfaces)
- **/proc**: Virtual filesystem (kernel/process information)
- **/var**: Variable data (logs, databases, mail)
- **/tmp**: Temporary files (cleared on reboot)
- **/usr**: User programs and data
- **/boot**: Boot loader files and kernel
- **/opt**: Optional software packages
- **/srv**: Service-related data
- **/home**: User home directories
- **/root**: Root user's home directory
- **/mnt**: Mount points for temporary filesystems

### Linux Run Levels

#### Traditional Run Levels (SysV)

- **0**: Halt/Shutdown
- **1**: Single-user mode (maintenance)
- **2**: Multi-user without networking
- **3**: Multi-user with networking (text mode)
- **4**: Unused (custom)
- **5**: Multi-user with GUI
- **6**: Reboot

#### Systemd Targets (Modern)

- **poweroff.target**: Shutdown
- **rescue.target**: Single-user mode
- **multi-user.target**: Text mode
- **graphical.target**: GUI mode
- **reboot.target**: Restart

---

## Windows Server Administration

### Windows File System Structure

#### System Directories

- \*\*C:\*\*: Root drive containing Windows system files
- **Program Files**: 64-bit applications
- **Program Files (x86)**: 32-bit applications
- **ProgramData**: Shared application data
- **Users**: User profiles and data
- **Windows**: Core Windows system files

- **System32**: Essential system files and utilities
- **WinSxS**: Side-by-side component store
- **Temp**: Temporary system files

#### Hidden System Files

- **pagefile.sys**: Virtual memory file
- **swapfile.sys**: Modern apps virtual memory
- **hiberfil.sys**: Hibernation data
- **Recovery**: System recovery tools

### Windows Server Roles

#### Common Server Roles

- **DHCP Server**: Automatic IP configuration
- **DNS Server**: Name resolution services
- **File and Storage Services**: File sharing
- **Active Directory Domain Services**: Domain controller
- **Web Server (IIS)**: Web hosting
- **Print Services**: Printer sharing

### Windows Management Tools

#### Computer Management (compmgmt.msc)

- **System Tools**:

- **Task Scheduler**: Automated task execution
- **Event Viewer**: System logs and monitoring
- **Device Manager**: Hardware management
- **Services**: System service management

#### Service Management

**Startup Types**:

- **Automatic**: Starts with Windows
- **Automatic (Delayed)**: Starts after other services
- **Manual**: Starts when needed
- **Disabled**: Cannot start

### Windows Server Configuration

#### Initial Setup

1. **Server Name**: Change to descriptive name
2. **Workgroup/Domain**: Join appropriate group
3. **IP Configuration**: Set static IP address
4. **Windows Update**: Configure update settings
5. **Firewall**: Configure for services
6. **Remote Management**: Enable WinRM if needed

---

## Domain & DNS Concepts

### Domain Name System (DNS)

#### Purpose

Translates human-readable domain names to IP addresses and vice versa.

#### DNS Hierarchy

```mermaid
DNS Hierarchy Structure.download-icon {
            cursor: pointer;
            transform-origin: center;
        }
        .download-icon .arrow-part {
            transition: transform 0.35s cubic-bezier(0.35, 0.2, 0.14, 0.95);
             transform-origin: center;
        }
        button:has(.download-icon):hover .download-icon .arrow-part, button:has(.download-icon):focus-visible .download-icon .arrow-part {
          transform: translateY(-1.5px);
        }
        #mermaid-diagram-r338{font-family:var(--font-geist-sans);font-size:12px;fill:#000000;}#mermaid-diagram-r338 .error-icon{fill:#552222;}#mermaid-diagram-r338 .error-text{fill:#552222;stroke:#552222;}#mermaid-diagram-r338 .edge-thickness-normal{stroke-width:1px;}#mermaid-diagram-r338 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-diagram-r338 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-diagram-r338 .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-diagram-r338 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-diagram-r338 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-diagram-r338 .marker{fill:#666;stroke:#666;}#mermaid-diagram-r338 .marker.cross{stroke:#666;}#mermaid-diagram-r338 svg{font-family:var(--font-geist-sans);font-size:12px;}#mermaid-diagram-r338 p{margin:0;}#mermaid-diagram-r338 .label{font-family:var(--font-geist-sans);color:#000000;}#mermaid-diagram-r338 .cluster-label text{fill:#333;}#mermaid-diagram-r338 .cluster-label span{color:#333;}#mermaid-diagram-r338 .cluster-label span p{background-color:transparent;}#mermaid-diagram-r338 .label text,#mermaid-diagram-r338 span{fill:#000000;color:#000000;}#mermaid-diagram-r338 .node rect,#mermaid-diagram-r338 .node circle,#mermaid-diagram-r338 .node ellipse,#mermaid-diagram-r338 .node polygon,#mermaid-diagram-r338 .node path{fill:#eee;stroke:#999;stroke-width:1px;}#mermaid-diagram-r338 .rough-node .label text,#mermaid-diagram-r338 .node .label text{text-anchor:middle;}#mermaid-diagram-r338 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-diagram-r338 .node .label{text-align:center;}#mermaid-diagram-r338 .node.clickable{cursor:pointer;}#mermaid-diagram-r338 .arrowheadPath{fill:#333333;}#mermaid-diagram-r338 .edgePath .path{stroke:#666;stroke-width:2.0px;}#mermaid-diagram-r338 .flowchart-link{stroke:#666;fill:none;}#mermaid-diagram-r338 .edgeLabel{background-color:white;text-align:center;}#mermaid-diagram-r338 .edgeLabel p{background-color:white;}#mermaid-diagram-r338 .edgeLabel rect{opacity:0.5;background-color:white;fill:white;}#mermaid-diagram-r338 .labelBkg{background-color:rgba(255, 255, 255, 0.5);}#mermaid-diagram-r338 .cluster rect{fill:hsl(0, 0%, 98.9215686275%);stroke:#707070;stroke-width:1px;}#mermaid-diagram-r338 .cluster text{fill:#333;}#mermaid-diagram-r338 .cluster span{color:#333;}#mermaid-diagram-r338 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:var(--font-geist-sans);font-size:12px;background:hsl(-160, 0%, 93.3333333333%);border:1px solid #707070;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-diagram-r338 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#000000;}#mermaid-diagram-r338 .flowchart-link{stroke:hsl(var(--gray-400));stroke-width:1px;}#mermaid-diagram-r338 .marker,#mermaid-diagram-r338 marker,#mermaid-diagram-r338 marker *{fill:hsl(var(--gray-400))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r338 .label,#mermaid-diagram-r338 text,#mermaid-diagram-r338 text>tspan{fill:hsl(var(--black))!important;color:hsl(var(--black))!important;}#mermaid-diagram-r338 .background,#mermaid-diagram-r338 rect.relationshipLabelBox{fill:hsl(var(--white))!important;}#mermaid-diagram-r338 .entityBox,#mermaid-diagram-r338 .attributeBoxEven{fill:hsl(var(--gray-150))!important;}#mermaid-diagram-r338 .attributeBoxOdd{fill:hsl(var(--white))!important;}#mermaid-diagram-r338 .label-container,#mermaid-diagram-r338 rect.actor{fill:hsl(var(--white))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r338 line{stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r338 :root{--mermaid-font-family:var(--font-geist-sans);}Root Servers(.)13 Root Servers WorldwideTop-Level Domain Servers(.com, .org, .net, .edu, .gov)Country Code TLD(.uk, .de, .jp, .ca)Authoritative Name Servers(example.com zone)Country-specific Domains(example.co.uk)Subdomains( )(mail.example.com)Local DNS Resolver(ISP or Organization)8.8.8.8, 1.1.1.1Client Device(Your Computer)
```

#### DNS Query Process

```mermaid
DNS Resolution Process.download-icon {
            cursor: pointer;
            transform-origin: center;
        }
        .download-icon .arrow-part {
            transition: transform 0.35s cubic-bezier(0.35, 0.2, 0.14, 0.95);
             transform-origin: center;
        }
        button:has(.download-icon):hover .download-icon .arrow-part, button:has(.download-icon):focus-visible .download-icon .arrow-part {
          transform: translateY(-1.5px);
        }
        Authoritative Server(example.com).com TLD ServerRoot ServerLocal DNS Resolver(ISP)Client DeviceAuthoritative Server(example.com).com TLD ServerRoot ServerLocal DNS Resolver(ISP)Client Device#mermaid-diagram-r33d{font-family:var(--font-geist-sans);font-size:12px;fill:#000000;}#mermaid-diagram-r33d .error-icon{fill:#552222;}#mermaid-diagram-r33d .error-text{fill:#552222;stroke:#552222;}#mermaid-diagram-r33d .edge-thickness-normal{stroke-width:1px;}#mermaid-diagram-r33d .edge-thickness-thick{stroke-width:3.5px;}#mermaid-diagram-r33d .edge-pattern-solid{stroke-dasharray:0;}#mermaid-diagram-r33d .edge-thickness-invisible{stroke-width:0;fill:none;}#mermaid-diagram-r33d .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-diagram-r33d .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-diagram-r33d .marker{fill:#666;stroke:#666;}#mermaid-diagram-r33d .marker.cross{stroke:#666;}#mermaid-diagram-r33d svg{font-family:var(--font-geist-sans);font-size:12px;}#mermaid-diagram-r33d p{margin:0;}#mermaid-diagram-r33d .actor{stroke:hsl(0, 0%, 83%);fill:#eee;}#mermaid-diagram-r33d text.actor>tspan{fill:#333;stroke:none;}#mermaid-diagram-r33d .actor-line{stroke:hsl(0, 0%, 83%);}#mermaid-diagram-r33d .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-diagram-r33d .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-diagram-r33d #arrowhead path{fill:#333;stroke:#333;}#mermaid-diagram-r33d .sequenceNumber{fill:white;}#mermaid-diagram-r33d #sequencenumber{fill:#333;}#mermaid-diagram-r33d #crosshead path{fill:#333;stroke:#333;}#mermaid-diagram-r33d .messageText{fill:#333;stroke:none;}#mermaid-diagram-r33d .labelBox{stroke:hsl(0, 0%, 83%);fill:#eee;}#mermaid-diagram-r33d .labelText,#mermaid-diagram-r33d .labelText>tspan{fill:#333;stroke:none;}#mermaid-diagram-r33d .loopText,#mermaid-diagram-r33d .loopText>tspan{fill:#333;stroke:none;}#mermaid-diagram-r33d .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(0, 0%, 83%);fill:hsl(0, 0%, 83%);}#mermaid-diagram-r33d .note{stroke:#999;fill:#666;}#mermaid-diagram-r33d .noteText,#mermaid-diagram-r33d .noteText>tspan{fill:#fff;stroke:none;}#mermaid-diagram-r33d .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-diagram-r33d .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-diagram-r33d .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-diagram-r33d .actorPopupMenu{position:absolute;}#mermaid-diagram-r33d .actorPopupMenuPanel{position:absolute;fill:#eee;box-shadow:0px 8px 16px 0px rgba(0,0,0,0.2);filter:drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));}#mermaid-diagram-r33d .actor-man line{stroke:hsl(0, 0%, 83%);fill:#eee;}#mermaid-diagram-r33d .actor-man circle,#mermaid-diagram-r33d line{stroke:hsl(0, 0%, 83%);fill:#eee;stroke-width:2px;}#mermaid-diagram-r33d .flowchart-link{stroke:hsl(var(--gray-400));stroke-width:1px;}#mermaid-diagram-r33d .marker,#mermaid-diagram-r33d marker,#mermaid-diagram-r33d marker *{fill:hsl(var(--gray-400))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r33d .label,#mermaid-diagram-r33d text,#mermaid-diagram-r33d text>tspan{fill:hsl(var(--black))!important;color:hsl(var(--black))!important;}#mermaid-diagram-r33d .background,#mermaid-diagram-r33d rect.relationshipLabelBox{fill:hsl(var(--white))!important;}#mermaid-diagram-r33d .entityBox,#mermaid-diagram-r33d .attributeBoxEven{fill:hsl(var(--gray-150))!important;}#mermaid-diagram-r33d .attributeBoxOdd{fill:hsl(var(--white))!important;}#mermaid-diagram-r33d .label-container,#mermaid-diagram-r33d rect.actor{fill:hsl(var(--white))!important;stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r33d line{stroke:hsl(var(--gray-400))!important;}#mermaid-diagram-r33d :root{--mermaid-font-family:var(--font-geist-sans);}Query: www.example.comQuery: www.example.comReferral: .com TLD serversQuery: www.example.comReferral: example.com NSQuery: www.example.comAnswer: 192.168.1.100Answer: 192.168.1.100
```

#### DNS Record Types

- **A**: IPv4 address mapping
- **AAAA**: IPv6 address mapping
- **CNAME**: Canonical name (alias)
- **MX**: Mail exchange servers
- **NS**: Name server records
- **PTR**: Reverse DNS lookup
- **TXT**: Text records (verification, SPF)
- **SRV**: Service locator records
- **SOA**: Start of Authority (zone information)

### Domain Valuation Factors

#### Technical Factors

- **TLD Importance**: .com > .org > .net > others
- **Domain Length**: Shorter is generally better
- **Memorability**: Easy to remember and spell
- **Brandability**: Suitable for business use

#### Market Factors

- **Keyword Value**: Search volume and relevance
- **Market Trends**: Industry popularity
- **Historical Sales**: Comparable domain sales
- **Traffic/SEO**: Existing visitors and search ranking

### WHOIS Information

- **Domain Status**: Registration status
- **Registrant**: Domain owner information
- **Registration Dates**: Created, updated, expires
- **Name Servers**: DNS servers for domain
- **Contact Information**: Administrative and technical contacts

---

## IP Configuration Rules & Best Practices

### IP Assignment Rules

1. **Uniqueness**: Each IP must be unique within network
2. **Correct Network**: IP must belong to proper network segment
3. **Valid Range**: Avoid network and broadcast addresses
4. **Reserved Addresses**: Don't use gateway, DHCP server IPs
5. **Subnet Consistency**: Match subnet mask across network
6. **DHCP Coordination**: Avoid conflicts with DHCP pools
7. **Gateway Network**: Gateway must be in same network

### Network Troubleshooting

#### Common Error Messages

- **Host Unreachable**: Device not responding (same network)
- **Transmit Failed**: Different network, routing issue
- **Request Timeout**: Network congestion or firewall

#### Troubleshooting Commands

- **Windows**: ipconfig, ping, tracert, nslookup
- **Linux**: ifconfig/ip, ping, traceroute, dig

### Cable Standards & Pinouts

#### Ethernet Cable Categories

- **CAT5e**: Up to 1 Gbps (100 MHz)
- **CAT6**: Up to 10 Gbps over short distances (250 MHz)
- **CAT6a**: Up to 10 Gbps at full distance (500 MHz)

#### T568B Wiring Standard

1. **Orange/White**
2. **Orange**
3. **Green/White**
4. **Blue**
5. **Blue/White**
6. **Green**
7. **Brown/White**
8. **Brown**

#### Connector Types

- **RJ45**: Ethernet (8-pin)
- **RJ11**: Telephone (6-pin)

---

## Alternative Visualization Methods

### 1. ASCII Art Diagrams

For simple text-based representations that work in any environment:

```plaintext
DNS Hierarchy (ASCII):
                    [Root Servers (.)]
                           |
        +------------------+------------------+
        |                  |                  |
    [.com TLD]         [.org TLD]         [.net TLD]
        |                  |                  |
   [example.com]      [nonprofit.org]   [network.net]
        |
   [www.example.com]
```

### 2. Table-Based Representations

For structured data that's easy to read:

| DNS Level     | Example                                   | Responsibility      |
| ------------- | ----------------------------------------- | ------------------- |
| Root          | .                                         | Global coordination |
| TLD           | .com                                      | Top-level domains   |
| Authoritative | example.com                               | Domain-specific     |
| Subdomain     | [www.example.com](http://www.example.com) | Host-specific       |

### 3. Flowchart Alternatives

Using simple text-based flowcharts:

```plaintext
DHCP Process Flow:
Client Boot → DISCOVER → Server OFFER → Client REQUEST → Server ACK → IP Assigned
```

### 4. Mind Map Style

For conceptual understanding:

```plaintext
Network Topologies
├── Star
│   ├── Advantages: Easy troubleshooting
│   └── Disadvantages: Single point of failure
├── Bus
│   ├── Advantages: Cost-effective
│   └── Disadvantages: Difficult troubleshooting
├── Ring
│   ├── Advantages: Predictable performance
│   └── Disadvantages: One failure affects all
└── Mesh
    ├── Advantages: High redundancy
    └── Disadvantages: Expensive
```

### 5. Interactive Learning Tools

Recommended external tools for better visualization:

- **Packet Tracer**: Cisco's network simulation tool
- **GNS3**: Advanced network emulator
- **Draw.io**: Free online diagramming tool
- **Lucidchart**: Professional network diagrams
- **Visio**: Microsoft's diagramming software

---

## Study Resources & Practical Exercises

### Key Topics for Review

1. **Internet vs Intranet vs VPN**
2. **Classful vs Classless addressing**
3. **Public vs Private IP ranges**
4. **DHCP configuration and DORA process**
5. **NAT and Port Forwarding**
6. **Network devices and topologies**
7. **OSI and TCP/IP models**
8. **Linux distributions and package management**
9. **Host files and NetBIOS**
10. **Link-local addressing (APIPA)**

### Practical Exercises

1. **Network Testing**:

1. Configure static IPs on same network
1. Test connectivity with ping
1. Use traceroute/tracert to trace paths

1. **Subnetting Practice**:

1. Use subnet calculators
1. Practice VLSM scenarios
1. Calculate network/broadcast addresses

1. **Server Configuration**:

1. Set up DHCP server
1. Configure DNS forwarding
1. Practice domain joining

1. **Troubleshooting**:

1. Identify network connectivity issues
1. Use network diagnostic tools
1. Analyze network traffic

### Useful Tools & Utilities

- **Windows**: ncpa.cpl, compmgmt.msc, services.msc
- **Network Tools**: Wireshark, Nmap, PuTTY
- **Online Resources**: Subnet calculators, WHOIS lookup
- **Documentation**: RFC standards, vendor documentation

---

## Glossary

**APIPA**: Automatic Private IP Addressing (169.254.x.x)
**CIDR**: Classless Inter-Domain Routing
**DHCP**: Dynamic Host Configuration Protocol
**DNS**: Domain Name System
**FQDN**: Fully Qualified Domain Name
**IANA**: Internet Assigned Numbers Authority
**NAT**: Network Address Translation
**OSI**: Open Systems Interconnection
**PoE**: Power over Ethernet
**TCP/IP**: Transmission Control Protocol/Internet Protocol
**VLAN**: Virtual Local Area Network
**VPN**: Virtual Private Network
