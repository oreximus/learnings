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

- **Purpose**: Connect networks across a city
- **Device**: Router (organization-owned)
- **Range**: 4m - citywide
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

#### WCAN (Wireless CAN)

- **Device**: Wi-Fi Access Point (AP)
- **Range**: 20m - 1km
- **Devices**: Up to 250 PCs
- **Use**: Large campus wireless coverage

#### WMAN (Wireless MAN)

- **Device**: Wi-Fi CPE (Customer Premises Equipment)
- **Range**: 20m - 15km
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

#### Class A (0.0.0.0 to 127.255.255.255)

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

1. **IANA** (Internet Assigned Numbers Authority) - Global coordination
2. **Regional Registries** - Continental distribution
3. **National Registries/ISPs** - Country/provider level
4. **End Users** - Individual/organization assignment

### Network Communication Process

1. **Same Network**: Direct communication through switch
2. **Different Network**: Packet sent to gateway/router
3. **Internet**: Multiple routers forward packet to destination
4. **Return Path**: Response follows reverse route

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

- **Structure**: All devices connect to central hub/switch
- **Advantages**: Easy troubleshooting, centralized management
- **Disadvantages**: Single point of failure (central device)
- **Use**: Most common in modern LANs

#### Bus Topology

- **Structure**: All devices share common communication line
- **Advantages**: Simple, cost-effective for small networks
- **Disadvantages**: Difficult troubleshooting, single point of failure
- **Use**: Legacy networks, some industrial applications

#### Ring Topology

- **Structure**: Devices connected in circular fashion
- **Advantages**: Predictable performance, no collisions
- **Disadvantages**: Failure of one device affects entire network
- **Use**: Token Ring networks (legacy)

#### Mesh Topology

- **Structure**: Multiple connections between devices
- **Types**: Full mesh (all-to-all) or partial mesh
- **Advantages**: High redundancy, excellent fault tolerance
- **Disadvantages**: Expensive, complex configuration
- **Use**: Critical infrastructure, WAN connections

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

1. **Discover**: Client broadcasts DHCP Discover message
2. **Offer**: Server responds with IP offer
3. **Request**: Client requests specific IP from server
4. **Acknowledge**: Server confirms assignment

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

1. **Root Servers**: Top-level (.)
2. **TLD Servers**: Top-Level Domains (.com, .org, .net)
3. **Authoritative Servers**: Domain-specific
4. **Local DNS**: ISP or organization DNS

#### DNS Record Types

- **A**: IPv4 address mapping
- **AAAA**: IPv6 address mapping
- **CNAME**: Canonical name (alias)
- **MX**: Mail exchange servers
- **NS**: Name server records
- **PTR**: Reverse DNS lookup
- **TXT**: Text records (verification, SPF)

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

   - Configure static IPs on same network
   - Test connectivity with ping
   - Use traceroute/tracert to trace paths

2. **Subnetting Practice**:

   - Use subnet calculators
   - Practice VLSM scenarios
   - Calculate network/broadcast addresses

3. **Server Configuration**:

   - Set up DHCP server
   - Configure DNS forwarding
   - Practice domain joining

4. **Troubleshooting**:
   - Identify network connectivity issues
   - Use network diagnostic tools
   - Analyze network traffic

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
