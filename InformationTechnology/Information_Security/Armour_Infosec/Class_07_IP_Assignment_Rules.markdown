# Class 07: Rules for Assigning IP Addresses

## Overview
This class outlines the rules for assigning IP addresses to devices to ensure proper network functionality.

## IP Assignment Rules
1. **Uniqueness**: Each device in a network must have a unique IP to avoid conflicts.
2. **Correct Network**: IPs must belong to the same network segment (same network ID).
3. **Valid IP Range**: IPs must be within the network’s usable range, excluding network and broadcast addresses.
4. **Avoid Reserved IPs**: Do not use reserved IPs (e.g., private ranges, loopback).
5. **Consistent Subnet Mask**: All devices in the same network must use the same subnet mask.
6. **Avoid DHCP Conflicts**: Ensure manually assigned IPs do not overlap with DHCP ranges.
7. **Consistent Gateway**: Devices must use the correct gateway IP for routing.

## Network and Broadcast Addresses
- **Network Address**: All host bits are 0 (e.g., 192.168.1.0 in a /24 network).
- **Broadcast Address**: All host bits are 1 (e.g., 192.168.1.255 in a /24 network).
- **Note**: These addresses are reserved and cannot be assigned to devices.

## Corrections
- Clarified that network and broadcast addresses are reserved and cannot be used for hosts.
- Added details on DHCP conflict prevention.