# Class 11: Network Devices and Transmission Media

## Theory Section

### Network Transmission Media

#### Unshielded Twisted Pair (UTP) Cable Categories

##### CAT5e (Category 5 Enhanced)

- **Speed**: Up to 1 Gbps (1000 Mbps)
- **Frequency**: 100 MHz
- **Distance**: 100 meters maximum
- **Usage**: Most common for Gigabit Ethernet

##### CAT6 (Category 6)

- **Speed**: Up to 10 Gbps (short distances), 1 Gbps (full distance)
- **Frequency**: 250 MHz
- **Distance**: 55 meters for 10 Gbps, 100 meters for 1 Gbps
- **Usage**: High-performance networks

##### CAT6a (Category 6 Augmented)

- **Speed**: Up to 10 Gbps
- **Frequency**: 500 MHz
- **Distance**: 100 meters for 10 Gbps
- **Usage**: Future-proof installations

#### Cable Limitations and Considerations

- **Bending Radius**: Cannot be folded sharply (damages internal conductors)
- **Distance Limitations**: Signal degradation over long distances
- **Electromagnetic Interference**: Susceptible to EMI from power lines, motors
- **Installation**: Proper termination and testing required

### Ethernet Wiring Standards

#### 100BASE-TX (Fast Ethernet) Pinout

```
Pin 1: Orange/White (TX+)    - Transmit Data +
Pin 2: Orange (TX-)          - Transmit Data -
Pin 3: Green/White (RX+)     - Receive Data +
Pin 4: Blue                  - Unused in 100 Mbps
Pin 5: Blue/White            - Unused in 100 Mbps
Pin 6: Green (RX-)           - Receive Data -
Pin 7: Brown/White           - Unused in 100 Mbps
Pin 8: Brown                 - Unused in 100 Mbps
```

#### 1000BASE-T (Gigabit Ethernet) Pinout

```
Pin 1: Orange/White (BI_DA+) - Bidirectional Data A+
Pin 2: Orange (BI_DA-)       - Bidirectional Data A-
Pin 3: Green/White (BI_DB+)  - Bidirectional Data B+
Pin 4: Blue (BI_DC+)         - Bidirectional Data C+
Pin 5: Blue/White (BI_DC-)   - Bidirectional Data C-
Pin 6: Green (BI_DB-)        - Bidirectional Data B-
Pin 7: Brown/White (BI_DD+)  - Bidirectional Data D+
Pin 8: Brown (BI_DD-)        - Bidirectional Data D-
```

## Practical Section

### Cable Color Coding Standards

#### T568A Standard

```
Pin 1: Green/White
Pin 2: Green
Pin 3: Orange/White
Pin 4: Blue
Pin 5: Blue/White
Pin 6: Orange
Pin 7: Brown/White
Pin 8: Brown
```

#### T568B Standard (Most Common)

```
Pin 1: Orange/White
Pin 2: Orange
Pin 3: Green/White
Pin 4: Blue
Pin 5: Blue/White
Pin 6: Green
Pin 7: Brown/White
Pin 8: Brown
```

### Connector Types and Applications

#### RJ45 (8P8C - 8 Position 8 Contact)

- **Usage**: Ethernet networking
- **Devices**: Computers, switches, routers
- **Cable**: Cat5e, Cat6, Cat6a UTP
- **Wiring**: T568A or T568B standard

#### RJ11 (6P4C - 6 Position 4 Contact)

- **Usage**: Telephone systems
- **Devices**: Phones, modems, fax machines
- **Cable**: Telephone wire (typically 2 or 4 conductors)
- **Wiring**: Various standards depending on application

### Network Interface Card (NIC) Features

#### Basic Functions

- **Physical Connection**: Provides network connectivity
- **MAC Address**: Unique hardware identifier
- **Signal Processing**: Converts digital data to electrical signals
- **Protocol Handling**: Implements Ethernet protocols

#### Advanced Features

##### Wake on LAN (WoL)

- **Purpose**: Remote power-up of devices
- **Requirements**: BIOS support, network connection maintained
- **Usage**: Remote management, energy saving
- **Magic Packet**: Special network packet to trigger wake-up

##### Auto-Negotiation

- **Speed Detection**: Automatically determines optimal speed
- **Duplex Mode**: Full-duplex vs half-duplex selection
- **Standards**: IEEE 802.3u for Fast Ethernet, 802.3ab for Gigabit

##### Link Aggregation

- **Purpose**: Combine multiple network connections
- **Benefits**: Increased bandwidth, redundancy
- **Standards**: IEEE 802.3ad (LACP)

### Network Device Categories

#### Layer 1 Devices (Physical Layer)

- **Hubs**: Simple signal repeaters (largely obsolete)
- **Repeaters**: Extend cable distance
- **Media Converters**: Convert between media types

#### Layer 2 Devices (Data Link Layer)

- **Switches**: Intelligent frame forwarding
- **Bridges**: Connect network segments
- **Wireless Access Points**: Wireless to wired bridging

#### Layer 3 Devices (Network Layer)

- **Routers**: Route packets between networks
- **Layer 3 Switches**: Switching with routing capabilities
- **Firewalls**: Security and access control

### Practical Exercises

#### Exercise 1: Cable Testing

1. **Visual Inspection**: Check for physical damage
2. **Continuity Testing**: Verify all pins connected
3. **Wire Mapping**: Confirm correct pin assignments
4. **Performance Testing**: Measure speed and error rates

#### Exercise 2: NIC Configuration

```bash
# Linux - View NIC information
ethtool eth0                    # Detailed interface info
ip link show eth0               # Basic interface status
lspci | grep -i ethernet        # PCI Ethernet devices

# Windows - View NIC information
Device Manager → Network Adapters
ipconfig /all                   # Detailed network configuration
```

#### Exercise 3: Wake on LAN Setup

```bash
# Enable WoL on Linux
ethtool -s eth0 wol g

# Send WoL packet
wakeonlan 00:11:22:33:44:55

# Windows WoL configuration
Device Manager → Network Adapter → Properties → Power Management
```

### Troubleshooting Network Connectivity

#### Physical Layer Issues

- **Cable Problems**: Damaged, incorrect wiring, wrong category
- **Connector Issues**: Poor termination, corrosion, loose connections
- **Distance Limitations**: Exceeding maximum cable length

#### Common Diagnostic Steps

1. **Check Physical Connections**: Cables, connectors, ports
2. **Verify Link Status**: LED indicators, software status
3. **Test Cable Integrity**: Cable tester, continuity check
4. **Check Speed/Duplex**: Auto-negotiation issues
5. **Monitor Error Counters**: CRC errors, collisions, drops

#### Diagnostic Commands

```bash
# Linux
ethtool eth0                    # Interface statistics
ip -s link show eth0           # Interface statistics
dmesg | grep eth0              # Kernel messages

# Windows
ipconfig /all                   # Network configuration
netsh interface show interface # Interface status
```

## Study Questions

1. What are the differences between CAT5e, CAT6, and CAT6a cables?
2. How does Wake on LAN work and what are its requirements?
3. What is the difference between T568A and T568B wiring standards?
4. How do you troubleshoot physical network connectivity issues?

## Next Class Preview

- Linux operating system fundamentals
- Shell concepts and command line interface
- Linux distributions and package management
