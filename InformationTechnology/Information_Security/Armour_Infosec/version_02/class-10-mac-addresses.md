# Class 10: MAC Addresses and Network Interface Cards

## Theory Section

### MAC Address (Media Access Control Address)

- **Definition**: Unique hardware identifier assigned to network interface cards during manufacturing
- **Purpose**: Physical addressing at the Data Link Layer (Layer 2)
- **Uniqueness**: Globally unique identifier for network devices
- **Assignment**: Burned into NIC during manufacturing (also called "burned-in address")

### MAC Address Characteristics

#### Structure

- **Length**: 48-bit address (6 bytes)
- **Format**: Usually displayed as 6 pairs of hexadecimal digits
- **Representation Formats**:
  - Colon Separated: 00:A0:C9:14:C8:29
  - Dash Separated: 00-A0-C9-14-C8-29
  - No Separation: 00A0C914C829

#### Address Components

```
MAC Address: 00:A0:C9:14:C8:29
             |----| |-------|
             OUI    Unique ID

First 24 bits (OUI): Organizationally Unique Identifier
- Identifies the manufacturer
- Assigned by IEEE Registration Authority

Last 24 bits: Manufacturer-assigned unique identifier
- Unique serial number from manufacturer
- Ensures global uniqueness
```

### Network Interface Card (NIC)

#### Types

- **Wired NICs**: Ethernet connections (RJ45)
- **Wireless NICs**: Wi-Fi connections (802.11 standards)
- **Integrated**: Built into motherboard
- **Add-on Cards**: PCIe, USB adapters

#### Speeds and Standards

```
10 Mbps:    Legacy Ethernet
100 Mbps:   Fast Ethernet (most common legacy)
1 Gbps:     Gigabit Ethernet (current standard)
10 Gbps:    10 Gigabit Ethernet (high-performance)
```

#### Advanced Features

- **Wake on LAN**: Remote power-up capability
- **Auto-negotiation**: Automatic speed/duplex detection
- **VLAN Support**: Virtual LAN tagging
- **Jumbo Frames**: Large packet support for performance

## Practical Section

### OUI (Organizationally Unique Identifier) Examples

#### Common Manufacturer OUIs

```
00:A0:C9 - Intel Corporation
00:50:56 - VMware
08:00:27 - Oracle VirtualBox
00:0C:29 - VMware
00:1B:21 - Intel Corporation
3C:97:0E - Wistron Corporation
```

#### OUI Range Example

```
Manufacturer: Intel (00:A0:C9)
Smallest Address: 00:A0:C9:00:00:00
Largest Address:  00:A0:C9:FF:FF:FF
Total Addresses:  16,777,216 (2^24)
```

### MAC Address Types

#### Unicast MAC Address

- **Definition**: Identifies a single network interface
- **First Bit**: 0 (even first octet)
- **Example**: 00:A0:C9:14:C8:29
- **Usage**: Normal device-to-device communication

#### Multicast MAC Address

- **Definition**: Identifies a group of network interfaces
- **First Bit**: 1 (odd first octet)
- **Example**: 01:00:5E:xx:xx:xx (IPv4 multicast)
- **Usage**: Group communication, streaming

#### Broadcast MAC Address

- **Definition**: Targets all devices in network segment
- **Address**: FF:FF:FF:FF:FF:FF
- **Usage**: ARP requests, DHCP discovery

### MAC Address Spoofing

- **Definition**: Changing the MAC address reported by network interface
- **Uses**:
  - Network testing and troubleshooting
  - Bypassing MAC-based access controls
  - Privacy protection
- **Limitation**: Only changes locally reported MAC, not burned-in address

### Network Troubleshooting with MAC Addresses

#### Common Scenarios

1. **Duplicate MAC**: Two devices with same MAC (rare, usually virtualization)
2. **ARP Poisoning**: Malicious MAC address mapping
3. **Switch MAC Table**: Learning and aging of MAC addresses
4. **DHCP Reservations**: Binding IP addresses to specific MAC addresses

## Study Questions

1. What is the difference between MAC address and IP address?
2. How does the OUI system ensure global MAC address uniqueness?
3. When would you use MAC address spoofing?
4. How do switches use MAC addresses for forwarding decisions?

## Next Class Preview

- Network transmission media and cabling
- Ethernet standards and wiring
- Connector types and applications
