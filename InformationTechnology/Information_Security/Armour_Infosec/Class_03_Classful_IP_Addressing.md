# Class 03: Classful IP Addressing

## Overview

This class explores the original system for classifying IPv4 addresses, known as Classful Addressing. This system divides the IPv4 address space into five classes: A, B, C, D, and E.

### Class A

* **Range**: 0.0.0.0 to 127.255.255.255.
* **Leading Bits**: The first bit is always `0`.
* **Structure**: `Network.Host.Host.Host`. The first 8 bits are for the network, and the last 24 bits are for hosts.
* **Total Networks**: $2^7 - 2$.
* **Hosts per Network**: $2^{24} - 2$.
* **Reserved For**: Large organizations, governments, and ISPs.

### Class B

* **Range**: 128.0.0.0 to 191.255.255.255.
* **Leading Bits**: The first two bits are always `10`.
* **Structure**: `Network.Network.Host.Host`. The first 16 bits are for the network, and the last 16 bits are for hosts.
* **Total Networks**: $2^{14}$.
* **Hosts per Network**: $2^{16} - 2$.
* **Reserved For**: Medium to large-sized networks, such as universities and large corporations.

### Class C

* **Range**: 192.0.0.0 to 223.255.255.255.
* **Leading Bits**: The first three bits are always `110`.
* **Structure**: `Network.Network.Network.Host`. The first 24 bits are for the network, and the last 8 bits are for hosts.
* **Total Networks**: $2^{21}$.
* **Hosts per Network**: $2^8 - 2$.
* **Reserved For**: Small networks.

### Class D

* **Range**: 224.0.0.0 to 239.255.255.255.
* **Leading Bits**: The first four bits are always `1110`.
* **Reserved For**: Multicast addressing. Not used for general host assignment.

### Class E

* **Range**: 240.0.0.0 to 255.255.255.255.
* **Leading Bits**: The first four bits are always `1111`.
* **Reserved For**: Experimental and research purposes. Not used in the public internet.

