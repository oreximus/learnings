# Class 07: IP Address Assignment Rules

## Overview

This class outlines the essential rules and best practices for assigning IP addresses to devices within a network to ensure proper communication and avoid conflicts.

## Rules for Assigning IP Addresses

1.  **Uniqueness**: Every device within the same network must have a unique IP address. If an IP is assigned to more than one device, an IP conflict occurs, and one or both devices will fail to communicate on the network.

2.  **Correct Network Segment**: All devices on the same physical network or subnet must have IP addresses from the same network segment. For example, if the network is `192.168.1.0/24`, all devices should have IPs like `192.168.1.x`.

3.  **Valid IP Range**: The assigned IP address must be a valid host address. You cannot use the network address or the broadcast address for a device.
    * **Network Address**: The first IP in a subnet, where all host bits are `0`. For `192.168.1.0/24`, the network address is `192.168.1.0`.
    * **Broadcast Address**: The last IP in a subnet, where all host bits are `1`. For `192.168.1.0/24`, the broadcast address is `192.168.1.255`.

4.  **Avoiding Reserved IP Addresses**: Do not assign special-purpose reserved addresses to standard devices, such as the loopback range (127.x.x.x).

5.  **Consistent Subnet Mask**: All devices within the same subnet must be configured with the same subnet mask to correctly identify the network and host portions of IP addresses.

6.  **Consistent Gateway Address**: All devices that need to communicate with outside networks (like the internet) must be configured with the same gateway address. The gateway IP must be on the same network segment as the devices.

7.  **Avoid Conflicts with DHCP**: If a DHCP server is used to automatically assign IPs, you must configure a static IP address from a range that is *outside* the DHCP scope to avoid the server assigning that same IP to another device.

