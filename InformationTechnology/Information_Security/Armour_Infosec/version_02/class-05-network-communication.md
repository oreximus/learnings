# Class 5: Network Communication Principles

## Theory Section

### Network Communication Rules

1. **Network First IP**: Always allocated to the Gateway
2. **IP Uniqueness**: IPs must be unique within the same network
3. **Same Network**: Devices can communicate directly
4. **Different Network**: Traffic routes through gateway
5. **Bidirectional Communication**: Source becomes destination and vice versa

### Communication Scenarios

#### Same Network Communication

```
Device A: 192.168.1.10/24
Device B: 192.168.1.20/24
Gateway: 192.168.1.1

Process:
1. Device A checks if Device B is on same network
2. Direct communication established
3. No gateway involvement needed
```

#### Different Network Communication

```
Device A: 192.168.1.10/24 (Private Network)
Device B: 8.8.8.8 (Public Network)
Gateway: 192.168.1.1

Process:
1. Device A recognizes different network
2. Sends packet to gateway (192.168.1.1)
3. Gateway routes to ISP
4. ISP routes to destination
5. Response follows reverse path
```

## Practical Section

### Port Forwarding

- **Definition**: Process of transferring public requests to private network hosts
- **Purpose**: Allows external access to internal services
- **Common Use**: Web servers, game servers, remote access

### NAT (Network Address Translation)

- **Function**: Translates private IPs to public IPs
- **Types**:
  - Static NAT (1:1 mapping)
  - Dynamic NAT (pool of public IPs)
  - PAT (Port Address Translation) - most common

### Network Types

#### Internet

- **Definition**: Public network available to everyone
- **Characteristics**: Global, public addressing, unrestricted access
- **Examples**: Websites, email servers, public services

#### Intranet

- **Definition**: Private network (also known as internal network)
- **Characteristics**: Private addressing, restricted access, internal use
- **Examples**: Company networks, home networks

### Communication Examples

#### IPv4 to Different Network IPv4

```
Private Device: 192.168.1.100
Public Server: 203.0.113.10

Steps:
1. Private device sends to gateway
2. NAT translates private IP to public IP
3. Packet routed through internet
4. Response translated back to private IP
5. Delivered to original device
```

#### Public to Private Communication

```
External Request: 203.0.113.50 → 203.0.113.10:80
Internal Server: 192.168.1.100:80

Port Forwarding Rule:
External Port 80 → Internal 192.168.1.100:80
```

## Key Concepts

### Gateway Functions

- **Routing**: Directs traffic between networks
- **NAT**: Translates addresses
- **Firewall**: Controls traffic flow
- **DHCP**: May assign IP addresses

### Address Resolution

- **ARP**: Maps IP addresses to MAC addresses
- **DNS**: Resolves domain names to IP addresses
- **DHCP**: Assigns IP addresses automatically

## Study Questions

1. How does communication differ between same and different networks?
2. What is the role of a gateway in network communication?
3. How does NAT enable private networks to access the internet?
4. What is port forwarding and when is it used?

## Next Class Preview

- Subnetting concepts
- Subnet masks and CIDR notation
- Network and broadcast addresses
