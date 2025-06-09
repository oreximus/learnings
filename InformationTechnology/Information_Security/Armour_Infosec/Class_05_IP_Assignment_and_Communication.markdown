# Class 05: IP Assignment and Communication

## Overview
This class covers rules for IP assignment and how devices communicate across networks.

## IP Assignment Rules
1. **Gateway Allocation**: The first IP in a network is reserved for the gateway (e.g., 192.168.1.1).
2. **Same Network**: Devices in the same network must share the same network ID.
3. **Unique IPs**: Each device must have a unique IP within the network to avoid conflicts.
4. **Routing to Gateway**: IPs outside the current network are sent to the gateway for routing.
5. **Reverse Communication**: Source and destination IPs swap during response (e.g., server to client).

## Communication Between IPs
- **Same Network**: Direct communication between devices.
- **Different Networks**: Traffic is routed through the gateway to the ISP or another network.
- **Port Forwarding**: Maps public IP requests to private IPs using NAT (Network Address Translation).
- **NAT and Port Forwarding**: Translates private IPs to public IPs for internet access.

## Internet vs. Intranet
- **Internet**: Public network accessible to everyone.
- **Intranet**: Private network restricted to an organization.

## Corrections
- Clarified the role of NAT in public-to-private IP communication.
- Added details on how gateways handle inter-network communication.