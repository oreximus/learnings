# Class 9: Network Topologies and Transmission Media

## Network Topologies by Generation

### 1. Line Topology

- **Structure**: Devices connected in a straight line series
- **Data Transfer**: Data flows through every device between source and destination
- **Security**: Low - every intermediate device can see the data
- **Current Use**: Not in practical use nowadays
- **Example**: Decorative lighting systems

### 2. Bus Topology

- **Structure**: All devices connected to a common network line (backbone)
- **Data Transfer**: Data flows along the main line, accessible to all devices
- **Advantages**: Simple, cost-effective
- **Disadvantages**: Single point of failure (main line)
- **Failure Impact**: If main network line breaks, entire network fails

### 3. Ring Topology

- **Structure**: All devices connected in a circular/ring manner
- **Data Transfer**: Data travels in one direction around the ring
- **Advantages**: Equal access for all devices
- **Disadvantages**: Single device failure can break the ring

### 4. Mesh Topology

- **Structure**: Devices connected in any random manner
- **Types**: Full mesh (every device connected to every other) or partial mesh
- **Advantages**: High redundancy, multiple paths
- **Disadvantages**: Complex, expensive

### 5. Star Topology

- **Structure**: All devices connected to a central hub/switch
- **Data Transfer**: All communication goes through central device
- **Advantages**: Easy to manage, failure isolation
- **Disadvantages**: Central device is single point of failure
- **Common Use**: Most modern networks

## Networking Devices and Transmission Media

### Unshielded Twisted Pair (UTP) Cable

#### Cable Categories

- **CAT5e**: Supports speeds up to 1 Gbps (1000 Mbps)
- **CAT6**: Higher performance, speeds up to 10 Gbps
- **CAT6a**: Improved performance for longer distances

#### Cable Limitations

- Cannot be folded excessively
- Not suitable for very long distances without repeaters
- Susceptible to electromagnetic interference

## Ethernet Wiring Standards

### 100 Mbps Ethernet (Fast Ethernet) - T568B Standard

#### Transmit Pairs

- **Pin 1**: Orange/White
- **Pin 2**: Orange

#### Receive Pairs

- **Pin 3**: Green/White
- **Pin 6**: Green

#### Full Pinout (T568B)

1. Orange/White
2. Orange
3. Green/White
4. Blue
5. Blue/White
6. Green
7. Brown/White
8. Brown

### Connector Types

- **RJ45**: Used for Ethernet connections in PCs
- **RJ11**: Used for telephone connections
