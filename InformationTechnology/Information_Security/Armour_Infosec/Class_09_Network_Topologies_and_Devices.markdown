# Class 09: Network Topologies and Devices

## Overview
This class discusses network topologies and transmission media used in networking.

## Network Topologies

### Line Topology
- **Description**: Devices connected in a series.
- **Data Transfer**: Data passes through each device between source and destination.
- **Data Security**: Each device can see the data, posing security risks.
- **Use Case**: Rarely used today; seen in decorative lighting.
- **Disadvantage**: Failure of one device disrupts the chain.

### Bus Topology
- **Description**: Devices connect to a single backbone cable.
- **Data Transfer**: Data travels along the backbone, accessible to all devices.
- **Failure**: Network functions unless the backbone fails.
- **Disadvantage**: Collisions and limited scalability.

### Ring Topology
- **Description**: Devices form a closed loop, each connected to the next.
- **Data Transfer**: Data circulates in one direction.
- **Disadvantage**: A single device failure can disrupt the network.

### Mesh Topology
- **Description**: Devices connect to multiple other devices, forming a complex network.
- **Data Transfer**: Multiple paths ensure redundancy.
- **Advantage**: High reliability; failure of one link doesn’t disrupt the network.
- **Disadvantage**: Expensive due to extensive cabling.

### Fully Connected Topology
- **Description**: Every device connects directly to every other device.
- **Data Transfer**: Direct communication between all devices.
- **Disadvantage**: Impractical for large networks due to cost and complexity.

### Star Topology
- **Description**: Devices connect to a central hub or switch.
- **Data Transfer**: All communication passes through the hub.
- **Advantage**: Easy to manage; failure of one device doesn’t affect others.
- **Disadvantage**: Hub failure disrupts the entire network.

## Transmission Media

### Unshielded Twisted Pair (UTP) Cable
- **Types**:
  - **CAT5e**: Supports up to 1 Gbps, 100m distance.
  - **CAT6**: Supports up to 10 Gbps, 55m distance.
  - **CAT6a**: Improved performance for 10 Gbps over longer distances (100m).
- **Limitations**: Cannot be folded tightly; limited range for high speeds.
- **Pin Assignments for 100 Mbps Ethernet (T568-B)**:
  - **Transmit**: Pin 1 (White/Orange), Pin 2 (Orange)
  - **Receive**: Pin 3 (White/Green), Pin 6 (Green)
- **Note**: Pins 4, 5, 7, and 8 are unused in Fast Ethernet.

## Corrections
- Corrected the pin assignments (original listed Pin 4 as Blue, which is incorrect).
- Added details on topology advantages and disadvantages.