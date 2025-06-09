# Class 06: Subnetting and CIDR

## Overview
This class explains subnetting, subnet masks, and Classless Inter-Domain Routing (CIDR).

## Subnet Mask
- **Definition**: A 32-bit address that separates the network and host portions of an IP address.
- **Structure**: Four octets, with 1s for network bits and 0s for host bits.
- **Classful Subnet Masks**:
  - **Class A**: 255.0.0.0 (/8, 8 network bits, 24 host bits)
  - **Class B**: 255.255.0.0 (/16, 16 network bits, 16 host bits)
  - **Class C**: 255.255.255.0 (/24, 24 network bits, 8 host bits)

## Subnetting
- **Definition**: Divides a network into smaller subnetworks (subnets) for efficient IP allocation.
- **Example**:
  - **IP**: 192.168.1.0
  - **Subnet Mask**: 255.255.255.128 (/25)
  - **Network Bits**: 25
  - **Host Bits**: 7
  - **Subnets**: 2¹ = 2 subnets
  - **Hosts per Subnet**: 2⁷ - 2 = 126 hosts
  - **Ranges**:
    - Subnet 1: 192.168.1.0–192.168.1.127
    - Subnet 2: 192.168.1.128–192.168.1.255

## Classless Inter-Domain Routing (CIDR)
- **Definition**: Uses variable-length subnet masks (VLSM) to allocate IPs efficiently, replacing classful addressing.
- **Notation**: e.g., 192.168.1.0/25 indicates a 25-bit network portion.
- **Benefits**: Reduces IP waste and supports hierarchical routing.

## Corrections
- Corrected the subnetting example (original had an incorrect mask and calculation).
- Added clarity on CIDR benefits and notation.