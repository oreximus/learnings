# Class 9: Network Topologies

## Theory Section

### Network Topologies by Generation

#### 1. Line Topology (Bus Topology - Linear)

- **Structure**: Devices connected in a straight line series
- **Data Transfer**: Data flows through every device between source and destination
- **Data Security**: Every intermediate device can see the data (security concern)
- **Current Use**: Not in practical use nowadays
- **Examples**: Decorative lights, some legacy systems

**Advantages:**

- Simple to implement
- Requires minimal cable

**Disadvantages:**

- Poor security (data visible to all devices)
- Single point of failure
- Performance degrades with more devices

#### 2. Bus Topology

- **Structure**: All devices connected to a common network line (backbone)
- **Data Transfer**: Data flows along the backbone, devices listen for their data
- **Failure Resilience**: Individual device failure doesn't affect network
- **Critical Failure**: Main network line (backbone) failure brings down entire network

**Advantages:**

- Easy to install and extend
- Requires less cable than star topology
- Individual device failures don't affect network

**Disadvantages:**

- Backbone failure affects entire network
- Difficult to troubleshoot
- Performance degrades with more devices

#### 3. Ring Topology

- **Structure**: Devices connected in a circular manner
- **Data Flow**: Data travels in one direction around the ring
- **Token Passing**: Often uses token-based access control

**Advantages:**

- Equal access for all devices
- No collisions with token passing
- Predictable performance

**Disadvantages:**

- Single device failure can break the ring
- Difficult to troubleshoot
- Adding/removing devices affects network

#### 4. Mesh Topology

- **Structure**: Devices connected in random manner, any device to any device
- **Flexibility**: Combination of multiple topologies
- **Redundancy**: Multiple paths between devices

**Types:**

- **Full Mesh**: Every device connected to every other device
- **Partial Mesh**: Some devices have multiple connections

**Advantages:**

- High redundancy and reliability
- Multiple paths for data
- Excellent fault tolerance

**Disadvantages:**

- Expensive (many cables/connections needed)
- Complex to install and maintain
- Difficult to troubleshoot

#### 5. Star Topology

- **Structure**: All devices connected to a central hub/switch
- **Data Flow**: All communication goes through central device
- **Centralized Control**: Hub/switch manages all network traffic

**Advantages:**

- Easy to install and manage
- Individual device failure doesn't affect others
- Easy to troubleshoot
- Good performance

**Disadvantages:**

- Central device failure brings down entire network
- Requires more cable than bus topology
- Hub/switch can become bottleneck

#### 6. Full Connected Topology

- **Structure**: All devices connected to a single central device
- **Similar to**: Star topology but with emphasis on complete connectivity
- **Usage**: Small networks with centralized control

## Practical Section

### Modern Network Implementation

#### Typical Office Network (Star Topology)

```
Internet → Router → Switch → Workstations
                 → Wireless Access Point → Mobile Devices
                 → Servers
                 → Printers
```

#### Home Network (Star Topology)

```
Internet → ISP Modem → Wireless Router → Devices
                                     → Wired Devices
                                     → Wireless Devices
```

### Topology Selection Criteria

#### Factors to Consider

1. **Network Size**: Number of devices to connect
2. **Budget**: Cost of equipment and installation
3. **Reliability Requirements**: Acceptable downtime
4. **Performance Needs**: Bandwidth and latency requirements
5. **Scalability**: Future expansion plans
6. **Management Complexity**: Available technical expertise

#### Topology Comparison Table

| Topology | Cost   | Reliability | Performance | Scalability | Management |
| -------- | ------ | ----------- | ----------- | ----------- | ---------- |
| Bus      | Low    | Poor        | Poor        | Limited     | Difficult  |
| Ring     | Medium | Medium      | Good        | Medium      | Medium     |
| Star     | Medium | Good        | Good        | Good        | Easy       |
| Mesh     | High   | Excellent   | Excellent   | Excellent   | Complex    |

## Study Questions

1. What are the advantages and disadvantages of each topology?
2. Why is star topology most commonly used in modern networks?
3. How do you choose the appropriate topology for a given scenario?
4. What role do network devices play in different topologies?

## Next Class Preview

- MAC addresses and network interface cards
- Physical addressing vs logical addressing
- Network device identification
