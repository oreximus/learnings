# Class 08: IP Address Configuration - Practical

## Overview

This class covers practical aspects of IP address configuration, including common gateway addresses and troubleshooting network errors related to IP settings.

## Practical Configuration

### Assigning a Class C IP

* For a typical small network using the `192.168.1.0/24` range, you can assign host IPs from `192.168.1.1` to `192.168.1.254`.
* The first IP address of the network (`192.168.1.0`) is the Network Address and cannot be used.
* The last IP address (`192.168.1.255`) is the Broadcast Address and cannot be used.
* The first usable IP (`192.168.1.1`) is typically assigned to the gateway (router).

### Common Default Gateways

Different ISPs and router manufacturers use common default IPs for their gateways:
* **Jio**: 192.168.29.1
* **Airtel**: 192.168.0.1

### Windows IP Configuration

You can access the network adapter settings in Windows quickly by:
* Opening the Run dialog (`Win + R`).
* Typing `ncpa.cpl` and pressing Enter.

## Common Network Errors

When troubleshooting with tools like `ping`, you might encounter these errors:

* **Host Unreachable**: This error occurs when your device can't find a path to the destination host. This often happens if the device is on the same network segment but is turned off, disconnected, or blocked by a firewall.

* **Transmit Failed / Destination Host Unreachable**: This can occur if your device's IP is on a different network segment from the destination and there is no correctly configured gateway to route the traffic.

* **Request Timed Out**: This means your device sent the packets, but it did not receive a reply from the destination host within a specific time limit. This could be due to network congestion, firewall issues on the destination, or the destination being down.

