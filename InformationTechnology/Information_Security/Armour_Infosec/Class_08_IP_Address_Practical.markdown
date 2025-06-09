# Class 08: IP Address Practical

## Overview
This class covers practical aspects of IP address assignment and common errors.

## IP Assignment Guidelines
- **First Octet Restrictions**: Cannot start with 0 (reserved for default route) or 127 (loopback).
- **Host Bits**: Cannot be all 0s (network address) or all 1s (broadcast address).
- **Common Gateway IPs**:
  - Jio: 192.168.29.1
  - Airtel: 192.168.0.1
- **Class C Example**:
  - Range: 192.168.1.2 to 192.168.1.254
  - Subnet Mask: 255.255.255.0 (/24)
  - Gateway: 192.168.1.1

## Common Errors
- **Host Unreachable**: IP is in the same network but the device is not present.
- **Transmit Failed**: IP is in a different network, and the gateway cannot route to it.

## Practical Exercise
- Assign IPs in the same network (e.g., 192.168.1.2 to 192.168.1.10) and test communication using `ping`.
- Use both classful (e.g., /24) and classless (e.g., /25) subnet masks.

## Corrections
- Clarified that the first octet cannot be 0 or 127 due to reserved uses.
- Added practical exercise details for clarity.