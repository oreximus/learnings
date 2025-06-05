# Class 10: MAC Addresses and Network Interface Cards

## MAC Address Fundamentals

### Definition

- **MAC**: Media Access Control Address
- **Purpose**: Unique identifier assigned to network interface during manufacturing
- **Scope**: Physical layer addressing
- **Types**: Wired and wireless network interfaces

### Technical Specifications

- **Size**: 48-bit address (6 bytes)
- **Structure**: Two parts
  - **First 24 bits**: OUI (Organizationally Unique Identifier) - identifies manufacturer
  - **Last 24 bits**: Manufacturer-assigned unique identifier

### Common Representations

- **Colon Separated**: 00:A0:C9:14:C8:29
- **Dash Separated**: 00-A0-C9-14-C8-29
- **No Separation**: 00A0C914C829

## Network Interface Card (NIC) Features

### Capabilities

- **Speeds**: Range from 10 Mbps (older) to 10 Gbps (modern high-speed)
- **Wake on LAN**: Remote power-up capability for remote management
- **Duplex**: Full-duplex communication support

### Physical Characteristics

- **Wired**: Ethernet ports (RJ45 connectors)
- **Wireless**: Wi-Fi antennas and radio modules
- **Power**: Some support Power over Ethernet (PoE)

## MAC Address Types

### 1. Unicast MAC Address

- **Purpose**: Identifies a single network interface
- **Format**: Least significant bit of first byte is 0
- **Usage**: Point-to-point communication

### 2. Multicast MAC Address

- **Purpose**: Identifies a group of network interfaces
- **Format**: Least significant bit of first byte is 1
- **Usage**: One-to-many communication

### 3. Broadcast MAC Address

- **Value**: FF:FF:FF:FF:FF:FF
- **Purpose**: Reaches all devices on local network segment
- **Usage**: Network announcements, ARP requests

## OUI (Organizationally Unique Identifier)

### Structure

- **Size**: First 24 bits of MAC address
- **Assignment**: Allocated by IEEE Registration Authority
- **Purpose**: Identifies device manufacturer

### Example OUI Range

- **Smallest Address**: 00:A0:C9:00:00:00
- **Largest Address**: 00:A0:C9:FF:FF:FF
- **Total Addresses**: 16,777,216 (2^24) per OUI

## MAC Address Characteristics

### Static Assignment

- **Method**: "Burned into" NIC during manufacturing
- **Permanence**: Stored in firmware/hardware
- **Uniqueness**: Globally unique (in theory)

### Practical Considerations

- **Network Testing**: Used for device identification
- **MAC Address Spoofing**: Software can change apparent MAC address
- **Security**: Used in access control lists
- **Troubleshooting**: Helps identify specific devices on network

## Frame Processing

- **Layer 2**: MAC addresses operate at Data Link Layer
- **Switching**: Switches learn and store MAC addresses
- **Forwarding**: Frames forwarded based on destination MAC
- **Aging**: Switch MAC tables have aging timers
