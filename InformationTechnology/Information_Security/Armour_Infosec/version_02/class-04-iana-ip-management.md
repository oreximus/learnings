# Class 4: IANA and IP Address Management

## Theory Section

### IANA (Internet Assigned Numbers Authority)

- **Primary Functions**:
  - IP Address Management
  - DNS Management
  - Protocol Assignment

### IP Address Distribution Hierarchy

#### Tier 1 (T1): IANA to Country

- **From**: IANA (Global Authority)
- **To**: GOI (Gateway of India) - approximately 80-90% allocation
- **Connection**: Physical submarine cables
- **Purpose**: International connectivity

#### Tier 2 (T2): Country to ISP

- **From**: GOI (Gateway of India)
- **To**: ISPs (BSNL, JIO, Airtel, etc.)
- **Purpose**: National distribution

#### Tier 3 (T3): ISP to City

- **From**: ISPs
- **To**: Local distribution points (e.g., Indore)
- **Purpose**: Regional connectivity

## Public vs Private IP Addresses

### Public IP Addresses

- **Source**: Provided by ISPs
- **Uniqueness**: Globally unique
- **Accessibility**: Reachable from internet
- **Cost**: Usually charged by ISP
- **Examples**: 8.8.8.8, 1.1.1.1

### Private IP Addresses

- **Source**: Assigned internally within private networks
- **Uniqueness**: Unique within local network only
- **Accessibility**: Not directly reachable from internet
- **Cost**: Free to use internally

### Reserved Private IP Ranges

#### Class A Private Range

- **Range**: 10.0.0.0 to 10.255.255.255
- **Subnet Mask**: 255.0.0.0 (/8)
- **Usage**: Large private networks

#### Class B Private Range

- **Range**: 172.16.0.0 to 172.31.255.255
- **Subnet Mask**: 255.255.0.0 (/16)
- **Usage**: Medium private networks

#### Class C Private Range

- **Range**: 192.168.0.0 to 192.168.255.255
- **Subnet Mask**: 255.255.255.0 (/24)
- **Usage**: Small private networks (most common)

#### Special Ranges

- **Carrier-Grade NAT**: 100.64.0.0 to 100.127.255.255
- **Loopback**: 127.0.0.0 to 127.255.255.255 (127.0.0.1 most common)

## Practical Section

### Network Communication Rules

- **Same Network IP**: Devices can communicate within the network
- **Different Network IP**: Traffic must go through gateway
- **IP Conflicts**: Same IP on multiple devices causes connectivity issues

### Communication Examples

```
Scenario 1: Same Network
Device A: 192.168.1.10
Device B: 192.168.1.20
Result: Direct communication possible

Scenario 2: Different Networks
Device A: 192.168.1.10
Device B: 192.168.2.10
Result: Must route through gateway
```

### Gateway Concepts

- **First IP**: Usually allocated to gateway (e.g., 192.168.1.1)
- **Gateway Role**: Routes traffic between networks
- **Default Route**: Where packets go when destination is unknown

## Study Questions

1. What is the role of IANA in internet governance?
2. Why do we need both public and private IP addresses?
3. How does the IP address distribution hierarchy work?
4. What happens when devices have conflicting IP addresses?

## Next Class Preview

- Network communication principles
- Port forwarding and NAT
- Internet vs Intranet concepts
