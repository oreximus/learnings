# Class 17: Windows DHCP Server Configuration

## Overview

This class covers the installation and configuration of the Dynamic Host Configuration Protocol (DHCP) server role on Windows Server. DHCP automates the assignment of IP addresses and other network settings to clients.

## 1. Theory: DHCP and the DORA Process

### DHCP (Dynamic Host Configuration Protocol)

* **Purpose**: A network management protocol used on IP networks whereby a DHCP server automatically assigns an IP address and other network configuration parameters to each device on a network.
* **Firewall Ports**: The DHCP server uses UDP port 67 (for server) and UDP port 68 (for client).
* **Uniqueness**: There should only be one active DHCP server in a single LAN segment to avoid conflicts.

### The DORA Process

The process a client follows to get an IP address from a DHCP server is called DORA:

1.  **D**iscover: The client, having no IP address, sends a broadcast message (`DHCPDISCOVER`) to the entire network to find any available DHCP servers.
2.  **O**ffer: Any DHCP server that receives the discover message can respond with a `DHCPOFFER` message. This message contains a potential IP address and other network settings for the client.
3.  **R**equest: The client receives one or more offers and chooses one. It then sends a `DHCPREQUEST` message back, broadcasting its choice to all servers to inform them which offer it has accepted.
4.  **A**cknowledgment (ACK): The server whose offer was chosen finalizes the lease and sends a `DHCPACK` message to the client, confirming the IP address and lease duration. The other servers rescind their offers.

---

## 2. Practical: DHCP Configuration in Windows Server

### Step 1: Installation

1.  Open **Server Manager** and go to `Manage > Add Roles and Features`.
2.  Select the **DHCP Server** role.
3.  Follow the wizard to complete the installation. A restart may be required.
4.  After installation, click the notification flag in Server Manager and select **Complete DHCP configuration** to authorize the DHCP server in Active Directory (if applicable).

### Step 2: Create a Scope

A **scope** is a range of IP addresses that the server can lease to clients.

1.  Open the DHCP management console (`dhcpmgmt.msc`).
2.  Right-click on your server name (or IPv4) and select **New Scope...**.
3.  **Name**: Give the scope a descriptive name.
4.  **IP Address Range**: Define the starting and ending IP addresses for the lease pool (e.g., `192.168.1.100` to `192.168.1.200`).
5.  **Exclusions**: You can specify any IPs within the range that you want to *exclude* from being assigned (e.g., for devices that need a static IP within that range).
6.  **Lease Duration**: Set how long a client can keep an IP address before it needs to be renewed. The default is 8 days.
7.  **Configure DHCP Options**: You will be prompted to configure common options now.
    * **Gateway (Router)**: Enter the IP address of your network's gateway.
    * **Domain Name and DNS Servers**: Enter your domain name and the IP addresses of your DNS servers.
8.  **Activate Scope**: Choose to activate the scope now.

### DHCP Features

* **Reservations**: To permanently assign a specific IP address to a specific device, you can create a reservation. This links an IP to a device's MAC address, ensuring it always gets the same IP. Useful for printers or servers.
* **Scope Options**: Network settings (like Gateway, DNS) that are applied to all clients getting an IP from this specific scope.
* **Server Options**: Global settings that apply to all scopes configured on the server.
* **Policies**: Create rules to assign different settings based on the client type (e.g., give different DNS servers to specific devices). You can create `Allow` or `Deny` lists based on MAC address.

