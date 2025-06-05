# Class 5: Network Communication Principles

## IP Assignment Rules
- **Network Gateway**: First IP in a network is typically assigned to the gateway
- **Same Network**: All devices must have the same network portion for direct communication
- **Unique Host**: Each device must have a unique host portion within the network

## Inter-Network Communication Process

### Same Network Communication
1. Source device checks if destination is on same network
2. Direct communication through switch/hub
3. No routing required

### Different Network Communication
1. Source device determines destination is on different network
2. Packet sent to default gateway (router)
3. Router forwards packet toward destination network
4. Process continues until destination is reached
5. Response follows reverse path

## Key Networking Concepts

### Port Forwarding
- **Purpose**: Transfer public incoming requests to private network hosts
- **Usage**: Allows external access to internal services
- **Example**: Accessing internal web server from internet

### NAT (Network Address Translation)
- **Function**: Translates private IP addresses to public IP addresses
- **Purpose**: Enables multiple devices to share single public IP
- **Types**: Static NAT, Dynamic NAT, PAT (Port Address Translation)

## Network Types by Access

### Internet
- **Definition**: Public network available to everyone
- **Access**: Global connectivity
- **Protocols**: TCP/IP suite

### Intranet
- **Definition**: Private network (also known as internal network)
- **Access**: Restricted to organization members
- **Security**: Higher security due to controlled access

## Communication Examples

### IPv4 to Different Network IPv4
- Requires routing through gateways
- May involve multiple hops
- Response path: Source becomes destination and vice versa

### Public-Private IP Communication
- Works through NAT and Port Forwarding
- Router maintains translation tables
- Enables internal network protection
\`\`\`
