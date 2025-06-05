# Class 13: Linux Distributions and Windows Server

## Linux Distributions and Package Managers

### 1. Debian-Based Distribution
- **Origin**: Free open-source Linux distribution
- **Developed**: 1993
- **Package Format**: .deb files
- **Package Manager**: APT (Advanced Package Tool)
- **Availability**: Compact form with core packages

#### Ubuntu
- **Based On**: Debian
- **Developed**: 2004
- **First Version**: Desktop version
- **Target**: Replace Windows XP
- **Popularity**: Most popular desktop Linux distribution

### 2. Red Hat Enterprise Linux (RHEL)
- **Developed**: 1993
- **Package Format**: .rpm files
- **Package Manager**: YUM/DNF
- **Target**: Enterprise environments

#### Related Distributions
- **Fedora**: Beta/testing version of RHEL
- **CentOS**: Free version of RHEL (discontinued)
- **Rocky Linux**: CentOS replacement
- **AlmaLinux**: Another CentOS replacement

## Windows Server Roles and Features

### Server Roles
- **Definition**: Primary functions that a server performs
- **Purpose**: Provide specific services to client computers
- **Examples**: 
  - Web Server (IIS)
  - DNS Server
  - DHCP Server
  - File Server
  - Print Server

### Server Features
- **Definition**: Additional functionality for the server
- **Purpose**: Enhance server capabilities
- **Examples**:
  - .NET Framework
  - PowerShell
  - Backup Features
  - Remote Management Tools

### Benefits
- **Client Advantages**: Clients can utilize server services
- **Centralized Management**: Single point of administration
- **Resource Sharing**: Efficient resource utilization
- **Scalability**: Can add roles as needed

### Installation Process
1. Open Server Manager
2. Select "Add Roles and Features"
3. Choose installation type
4. Select server
5. Choose roles/features
6. Configure settings
7. Install and restart if required

### Common Role Combinations
- **Domain Controller**: Active Directory Domain Services
- **File and Print Server**: File Services + Print Services
- **Web Server**: IIS + .NET Framework
- **Infrastructure Server**: DNS + DHCP + NTP
\`\`\`
