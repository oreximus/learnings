# Introduction to Networking

## Networking Oeverview

- A network enables two computers to communicate with each other.

- There is a wide array of **topologies** (mesh/tree/star), **medium**(ethernet/fiber/wireless), and **protocols** (TCP/UDP/IPX) that can be used to facilitate the network.

**Be able to understand the network structure of any organization**

***Consider list of these as example:***
    - Server Gateway
    - Domain Controller
    - Client Gateway
    - Client Workstation
    - Pentester IP

### Basic Information

- The website address or **Uniform Resource Locator (URL)** which we enter into our browser is also known as **Fully Qualified Domain Name (FQDN)**.

The difference between **URLs** and **FQDN** is that:

    - an **FQDN** (**www.google.com**) only specifies the address of the "building" and

### Extra Points

- The Web Server should be in a DMZ (Demilitarized Zone) because clients on the internet can initiate communications with the website, making it more likely to become compromised. Placing it in a separate network allows the administrators to put networking protections between the web server and other devices.

- Workstations should be on their own network, and in a perfect world, each workstation should have a Host-Based Firewall rule preventing it from talking to other workstations. If a Workstation is on the same network as a Server, networking attacks like **spoofing** or **man in the middle** become much more of an issue.

- The Switch and Router should be on an "Administrator Network." This prevents workstations from snooping in on my communication between these devices. I hace often performed a Penetration Test and saw **OSPF** (Open Shortest Path First) advertisements. Since the router did not have a **trusted network**, anyone on the internel network could have sent a malicious advertisement and performed a **man in the middle** attack against any network.

- IP Phones should be on their own network. Security-wise this is to prevent computers from being able to eavesdrop on communication. In addition to security, phones are unique in the sense that latency/lag is significant. Placing them on their own network can allow network administrators to prioritize their traffic to prevent high latency more easily.

- Printers should be on their own network. This may sound weired, but it is next to impossible to secure a printer. Due to how Windows works, if a printer tells a computer authentication is required during a print job, that computer will attempt an **NTLMv2** authentication, which can lead to passwords being stolen. Additionally, these devices are great for persistence and, in general, have tons of sensitive information sent to them.

## Network Types

- Each network is structured differently and can be set up individually. For this reason, so-called **types** and **topologies** have been developed that can be used to categorize these networks.

### Common Technology

| **Network** | **Definition** |
|-------------|----------------|
| Wide Area Network | Internet |
| Local Arean Network (LAN) | Internal Networks (Ex: Home or Office) |
| Wireless Local Area Network (WLAN) | Internal Networks accessible over Wi-Fi |
| Wireless Local Area Network (WLAN) | Internal Networks accessible over Wi-Fi |
| Virtual Private Network (VPN) | Connects multiple network sites to one **LAN** |

### WAN

The WAN (Wide Area Network) is commonly reffered to as **The Internet**. When dealing with networking equipment, we'll often have a WAN Address and LAN Address. The WAN one is the address that is generally accessed by the internet.That being said, it is not inclusive to the Internet, a WAN is just a large number of LANs joined together. Many large companies or government agencies will have an "Internal WAN" (also called Intranet, Airgap Network, etc.). Generally speaking, the primary way we identify if the network is a WAN is to use a WAN Specific routing protocol such as BGP and if the IP Schema in use in not within RFC 1918 (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16)

### LAN/WLAN

- LANs (Local Area Network) and WLANs (Wireless Local Area Network) will typically assign IP Addresses designated for local use (RFC 1918, 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0./16). In some cases, like some colleges or hotels, you may be assigned a routable (internet) IP Address LAN or WLAN, other than WLAN's introduce the ability to transmit data without cables. It is mainly a security designation.

### VPN

- There are three main types **Virtual Private Networks (VPN)**, but all three have the same goal of making the user feel as if they were plugged into a different network.

### Site-To-Site VPN

- Both the client and server are Network Devices, typically either **Routers** and **Firewalls**, and share entire network ranges. This is most commonly used to join company networks together over the Internet, allowing multiple locations to communicate over the Internet as if they were local.
