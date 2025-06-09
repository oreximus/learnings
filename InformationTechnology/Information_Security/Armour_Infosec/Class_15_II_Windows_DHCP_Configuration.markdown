# Class 15-II: Windows DHCP Configuration

## Overview
This class covers configuring a DHCP server on Windows Server and the DORA process.

## DHCP Server Configuration
- **Purpose**: Dynamically assigns IP addresses to clients.
- **Steps**:
  1. Open Server Manager.
  2. Add Role: Select “DHCP Server.”
  3. Configure Scope:
     - Name: e.g., “LAN_Scope”
     - IP Range: e.g., 192.168.1.100–192.168.1.200
     - Subnet Mask: 255.255.255.0
     - Gateway: 192.168.1.1
     - DNS Server: e.g., 8.8.8.8
  4. Activate Scope.
- **Files Location**: `C:\Windows\System32\dhcp`
- **Port**: UDP 67 (server), UDP 68 (client).
- **Note**: Only one DHCP server per LAN to avoid conflicts.

## DORA Process
- **Discover**: Client broadcasts a request to find a DHCP server.
- **Offer**: Server responds with an available IP.
- **Request**: Client requests the offered IP.
- **Acknowledge**: Server confirms the IP assignment.

## Verification
- **Check DHCP Presence**: Set client to “Obtain IP automatically” in network settings.
- **Disable Router DHCP**: Ensure no conflicting DHCP servers.

## Corrections
- Clarified DORA process and port usage.
- Added steps for scope configuration.