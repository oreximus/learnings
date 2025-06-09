# Class 14-II: Windows Server Basics

## Overview
This class covers basic Windows Server configuration and management.

## Server Manager
- **Purpose**: Centralized tool for managing server roles, features, and settings.
- **Access**: Available in the Start menu or via `servermanager.msc`.

## Services
- **Purpose**: Manage background processes (e.g., DHCP, DNS).
- **Startup Types**:
  - **Automatic**: Starts at boot.
  - **Automatic (Delayed Start)**: Starts after boot to reduce load.
  - **Manual**: Starts when needed.
  - **Disabled**: Does not start.
- **Example**: `LanmanServer` (file and printer sharing).

## Configuration
- **Server Name**: Set a memorable name (e.g., SRV01).
- **Workgroup**: Represents a department or group (default: WORKGROUP).
- **WinRM**: Enables remote management (Windows Remote Management).
- **IP Configuration**:
  - Example: Static IP 192.168.1.51, Subnet 255.255.255.0, Gateway 192.168.1.1.
- **Firewall**: Disable for experiments (not recommended for production).

## Corrections
- Clarified the purpose of `LanmanServer` and WinRM.
- Added details on firewall considerations.