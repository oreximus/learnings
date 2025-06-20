# Class 15: Windows Server Management and Services

## Theory Section

### Server Manager

- **Purpose**: Central management tool for Windows Server
- **Functions**:
  - Server configuration
  - Role and feature installation
  - Remote server management
  - Performance monitoring

### Windows Services Management

#### Service Control Manager

- **Access**: services.msc
- **Purpose**: Start, stop, and configure Windows services
- **Service States**: Running, Stopped, Paused

#### Service Startup Types

##### Automatic

- **Behavior**: Starts automatically when system boots
- **Usage**: Critical system services
- **Examples**: Windows Audio, DHCP Client

##### Automatic (Delayed Start)

- **Behavior**: Starts automatically but after other automatic services
- **Purpose**: Reduces boot time by staggering service startup
- **Usage**: Non-critical services that can wait

##### Manual

- **Behavior**: Starts only when explicitly started or when needed
- **Usage**: Services used occasionally
- **Examples**: Windows Update, Print Spooler (if no printer)

##### Disabled

- **Behavior**: Cannot be started
- **Purpose**: Security or resource conservation
- **Usage**: Unused or potentially dangerous services

### Server Roles and Features

#### Server Roles

- **Definition**: Primary functions that a server performs
- **Purpose**: Provide services to clients on the network
- **Installation**: Through Server Manager → Add Roles and Features

#### Common Server Roles

- **Active Directory Domain Services**: Directory services and authentication
- **DNS Server**: Domain name resolution
- **DHCP Server**: IP address assignment
- **Web Server (IIS)**: Web hosting and applications
- **File and Storage Services**: File sharing and storage management
- **Print and Document Services**: Print server functionality

#### Features

- **Definition**: Additional functionality that enhances server capabilities
- **Purpose**: Support roles or provide additional tools
- **Examples**: PowerShell, Remote Server Administration Tools

### Local Server Configuration

#### Server Name Management

- **Purpose**: Provide memorable and meaningful server names
- **Best Practices**: Use descriptive names (DC01, WEB01, FILE01)
- **Change Method**: Server Manager → Local Server → Computer name

#### Workgroup vs Domain

- **Workgroup**: Peer-to-peer network model
- **Domain**: Centralized authentication and management
- **Department Representation**: Workgroups often represent departments

#### Windows Remote Management (WinRM)

- **Purpose**: Enable remote management of Windows servers
- **Protocol**: WS-Management protocol
- **Usage**: PowerShell remoting, remote administration
- **Security**: Encrypted communication

#### Network Configuration

- **Static IP Assignment**: Recommended for servers
- **Example Configuration**:
  - IP Address: 192.168.1.51
  - Subnet Mask: 255.255.255.0
  - Default Gateway: 192.168.1.1
  - DNS Servers: 192.168.1.1, 8.8.8.8

#### Windows Firewall

- **Recommendation**: Disable for lab environments
- **Production**: Configure appropriate rules
- **Profiles**: Domain, Private, Public

## Practical Section

### DHCP Server Configuration

#### Installation Steps

1. **Server Manager** → Add Roles and Features
2. **Server Selection**: Choose local server
3. **Server Roles**: Select DHCP Server
4. **Features**: Accept defaults
5. **Confirmation**: Review and install
6. **Restart**: If required

#### DHCP Server Requirements

- **Unique Server**: Only one DHCP server per network segment
- **Lease Time**: Configure appropriate lease duration
- **Firewall**: Port 67 (DHCP server) must be allowed
- **Gateway and DNS**: Must be configured for clients
- **File Location**: C:\Windows\System32\dhcp\

#### DHCP Configuration Process

1. **Create Scope**:

   - Scope name and description
   - IP address range (start and end)
   - Subnet mask
   - Lease duration

2. **Configure Options**:

   - Default gateway (router)
   - DNS servers
   - Domain name
   - Other options as needed

3. **Activate Scope**: Enable the scope to start serving clients

#### DHCP Testing

- **Client Configuration**: Set network adapter to "Obtain IP address automatically"
- **Verification**: Check if client receives IP, gateway, and DNS
- **Conflict Prevention**: Disable other DHCP servers on network

### DHCP DORA Process

#### DORA Explained

- **D**iscover: Client broadcasts to find DHCP servers
- **O**ffer: DHCP server offers IP address and configuration
- **R**equest: Client requests the offered configuration
- **A**cknowledge: Server acknowledges and finalizes lease

#### DORA Process Details

1. **DHCP Discover**:

   - Client broadcasts on 255.255.255.255
   - Contains client MAC address
   - Requests IP configuration

2. **DHCP Offer**:

   - Server responds with available IP
   - Includes lease time and options
   - May include gateway, DNS, etc.

3. **DHCP Request**:

   - Client accepts offered configuration
   - May reject other offers
   - Confirms selection

4. **DHCP Acknowledge**:
   - Server confirms lease
   - Client configures network interface
   - Lease timer starts

## Study Questions

1. What are the different Windows service startup types and when would you use each?
2. What is the DORA process and why is it important?
3. What are the key considerations when configuring a DHCP server?
4. How do server roles differ from server features?

## Next Class Preview

- Linux basic commands and file operations
- Text editors and file manipulation
- System information and networking commands
- Process management and system control
