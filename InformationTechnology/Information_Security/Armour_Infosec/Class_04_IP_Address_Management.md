# Class 04: IP Address Management and Reserved IPs

## Overview

This class covers how IP addresses are managed globally by organizations like IANA and introduces the concept of public vs. private IP addressing as a solution to IPv4 address exhaustion.

## IANA (Internet Assigned Numbers Authority)

IANA is responsible for the global coordination of key internet resources, including:
* **IP Address Management**: Allocating blocks of IP addresses to Regional Internet Registries (RIRs).
* **DNS Management**: Managing the DNS root zone.
* **Protocol Assignment**: Maintaining assignments for internet protocols.

The distribution of IP addresses follows a hierarchy:
1.  **IANA** allocates to RIRs.
2.  RIRs allocate to country-level registries or ISPs (e.g., BSNL/JIO in India). This is known as a **T2** connection.
3.  ISPs allocate to their customers, such as businesses or cities. This is a **T3** connection.

## Public vs. Private IP Addresses

To overcome the shortage of IPv4 addresses, a system of public and private IPs was developed.

* **Public IP**: An IP address assigned by an ISP that is directly accessible over the internet.
* **Private IP**: An IP address used within a private network (intranet) that is not directly accessible from the internet.

### Reserved Private IP Ranges

Certain ranges are reserved for use in private networks and are not routable on the public internet.

* **Class A**: 10.0.0.0 to 10.255.255.255.
* **Class B**: 172.16.0.0 to 172.31.255.255. (Note: The provided notes incorrectly list this range, this is the correct range).
* **Class C**: 192.168.0.0 to 192.168.255.255. (Note: The provided notes incorrectly list this range, this is the correct range).
* **Carrier-Grade NAT**: 100.64.0.0 to 100.127.255.255.

### Special Purpose Addresses

* **Loopback Address**: 127.0.0.0 to 127.255.255.255, with 127.0.0.1 being the most common. Used by a host to send a message to itself for testing purposes.
* **Link-Local Address**: 169.254.0.0 to 169.254.255.255. Automatically assigned when a device cannot get an IP from a DHCP server.

