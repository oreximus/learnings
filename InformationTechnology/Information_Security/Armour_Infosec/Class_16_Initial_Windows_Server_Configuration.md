# Class 16: Initial Windows Server Configuration

## Overview

This class covers the first steps to take after installing Windows Server, using the Server Manager dashboard to perform initial configuration tasks like setting a static IP, changing the server name, and enabling remote management.

## Using Server Manager

**Server Manager** is the primary tool for managing a Windows Server. The **Local Server** properties pane in the dashboard provides a central place to view and modify essential server settings.

### Initial Configuration Steps

#### 1. Change the Server Name

* **Why**: The default computer name is randomly generated and not descriptive. Changing it to something memorable (e.g., `DC01`, `FILESRV`) is a critical first step for identification on the network.
* **How**: In Server Manager > Local Server, click the existing computer name to open System Properties and change it. A restart is required.

#### 2. Configure a Static IP Address

* **Why**: Servers provide services and must have a predictable, unchanging IP address. Dynamic IPs assigned by DHCP can change, which would break connections for clients trying to reach the server.
* **How**:
    1.  In Server Manager > Local Server, click the value next to "Ethernet" (which will likely show "IPv4 address assigned by DHCP"). This opens the Network Connections window (`ncpa.cpl`).
    2.  Right-click the network adapter, choose `Properties`, select `Internet Protocol Version 4 (TCP/IPv4)`, and click `Properties`.
    3.  Select "Use the following IP address" and enter a static IP, subnet mask, and gateway address appropriate for your network (e.g., `192.168.1.51`, `255.255.255.0`, `192.168.1.1`).
    4.  Also, configure the Preferred DNS server, which is often the server itself if it's a domain controller, or the gateway/router.

#### 3. Enable Remote Management and Remote Desktop

* **Why**: Managing servers remotely is standard practice. You should not need to be physically at the server console for most tasks.
* **How**:
    * **Windows Remote Management (WinRM)**: This is enabled by default and allows for management via tools like PowerShell Remoting and Server Manager from another machine.
    * **Remote Desktop**: In Server Manager > Local Server, click "Disabled" next to Remote Desktop to enable it. This allows you to connect to the server's full desktop experience using a Remote Desktop client.

#### 4. Configure Windows Firewall

* **Why**: The firewall is crucial for security, but for initial testing in a controlled lab environment, you might temporarily turn it off to ensure connectivity is not being blocked while you set up services.
* **How**: In Server Manager > Local Server, click the link next to "Windows Firewall" to configure its settings. For production, you should create specific rules to allow traffic for your services rather than turning it off completely.

#### 5. Configure WORKGROUP

* By default, a server is in a `WORKGROUP`. This represents a peer-to-peer network for a specific department or group. Later, the server will typically be joined to a domain.

