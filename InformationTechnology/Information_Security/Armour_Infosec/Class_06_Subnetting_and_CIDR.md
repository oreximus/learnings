# Class 06: Subnetting and CIDR

## Overview

This class introduces subnetting, a technique to divide a large IP network into smaller, more manageable sub-networks (or subnets). It also covers Subnet Masks and Classless Inter-Domain Routing (CIDR).

## Subnet Mask

A Subnet Mask is a 32-bit address used to distinguish the network portion of an IP address from the host portion.
* In a subnet mask, all network bits are set to `1` (ON), and all host bits are set to `0` (OFF).

#### Default Subnet Masks (Classful)

* **Class A**: 255.0.0.0 (Binary: `11111111.00000000.00000000.00000000`). Has 8 network bits.
* **Class B**: 255.255.0.0 (Binary: `11111111.11111111.00000000.00000000`). Has 16 network bits.
* **Class C**: 255.255.255.0 (Binary: `11111111.11111111.11111111.00000000`). Has 24 network bits.

## Subnetting

Subnetting is the logical subdivision of an IP network. It is achieved by "borrowing" bits from the host portion of the IP address and using them as network bits for the subnet.

#### Subnetting Example

* Consider a Class C network with the default mask `255.255.255.0`.
* If we use the subnet mask `255.255.255.192` (Binary: `...11000000`), we have borrowed 2 bits from the host portion.
* **Network Bits**: 24 (default) + 2 (borrowed) = 26 bits.
* **Host Bits**: 8 (default) - 2 (borrowed) = 6 bits.
* **Number of Subnets**: $2^{\text{borrowed bits}} = 2^2 = 4$ subnets.
* **Hosts per Subnet**: $2^{\text{host bits}} - 2 = 2^6 - 2 = 62$ hosts.

## Classless Inter-Domain Routing (CIDR)

CIDR was introduced to replace the classful system and slow IPv4 address exhaustion. It allows for more flexible allocation of IP addresses.

* **CIDR Notation**: An IP address is written with a suffix indicating the number of network bits, e.g., `192.168.1.0/24`.
    * `/24` means the first 24 bits are the network portion.
    * This is equivalent to the subnet mask `255.255.255.0`.

* **Classless Addressing**: When an IP address from one class is used with a subnet mask from another class (or any non-default mask), it is called Classless addressing. For example, a Class A IP with a `/24` mask.

