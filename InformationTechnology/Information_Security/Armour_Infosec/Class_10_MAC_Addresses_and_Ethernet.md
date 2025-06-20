# Class 10: MAC Addresses and Ethernet

## Overview

This class covers the physical aspects of networking, including Ethernet cables, connectors like RJ45, and the role of the MAC address as a unique hardware identifier.

## Ethernet Cables and Connectors

* **Unshielded Twisted Pair (UTP) Cable**: The most common type of cable used in wired LANs.
    * **CAT5e**: Supports speeds up to 1 Gbps. (Note: The notes mention 5GB, which is incorrect for CAT5e).
    * **CAT6**: Supports higher performance with speeds up to 10 Gbps over shorter distances.
    * **CAT6a**: Improved performance over longer distances for 10 Gbps.

* **Connectors**:
    * **RJ45**: Used for Ethernet connections in PCs and networking devices.
    * **RJ11**: Used for telephone lines.

## MAC Address (Media Access Control)

A MAC address is a unique identifier assigned to a Network Interface Controller (NIC) for use as a network address in communications within a network segment.

### Characteristics

* **Uniqueness**: Assigned by the manufacturer and burned into the hardware.
* **Size**: A 48-bit address.
* **Representation**: Commonly written in hexadecimal, separated by colons or dashes (e.g., `00:A0:C9:FF:FF:FF` or `00-A0-C9-FF-FF-FF`).
* **Structure**:
    * **First 24 bits**: OUI (Organizationally Unique Identifier). This identifies the manufacturer.
    * **Last 24 bits**: A unique value assigned by the manufacturer to the specific device.

### Commands

* **Windows**: `getmac` or `ipconfig /all` to find the MAC address.
* **Linux**: `ip a` or `ifconfig` to find the MAC address.

### Types of MAC Addresses

* **Unicast**: Represents a single specific NIC.
* **Multicast**: Represents a group of NICs. A multicast MAC address always starts with `01-00-5E`.
* **Broadcast**: Represents all NICs on the network. The broadcast MAC address is `FF:FF:FF:FF:FF:FF`.

### Features

* **MAC Address Spoofing**: The process of changing a NIC's MAC address. This can be used for legitimate purposes like network testing or for malicious purposes.
* **Wake-on-LAN**: A feature that allows a computer to be turned on or awakened by a network message. The message is sent to the device's MAC address.

