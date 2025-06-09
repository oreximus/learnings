# Class 20: Windows DHCP Configuration and Linux Commands

## Overview
This class covers advanced DHCP configuration on Windows and basic Linux navigation commands.

## Windows DHCP Configuration
- **Backup Options**:
  - **Manual Backup**: Export DHCP database via Server Manager.
  - **Snapshots**: Periodic backups for recovery.
- **Policies**:
  - **Allow List**: Permit specific clients.
  - **Deny List**: Block specific clients.
  - **Ignore**: Assign IPs to clients ignoring certain conditions.
- **Exclusion Range**: Reserve IPs (e.g., 192.168.1.1–192.168.1.10) for static use.
- **Reservation**: Assign fixed IPs to devices via MAC address.
- **Lease Expiration**: Configurable lease duration (e.g., 24 hours).
- **Scope Options**: Provide gateway, DNS, etc., to clients.
- **Server Options**: Apply settings to multiple scopes.

## Linux Commands
### ls
- **Purpose**: List files/directories.
- **Options**:
  ```bash
  ls -h   # Human-readable sizes
  ls -l   # Long format
  ls -a   # Include hidden files
  ls -la  # Long format with hidden files
  ls -r   # Reverse sorting
  ls -t   # Sort by modification time
  ls -1   # One file per line
  ```

### cd
- **Purpose**: Change directory.
- **Usage**:
  ```bash
  cd          # Go to home directory
  cd ..       # Go up one directory
  cd ../..    # Go up two directories
  ```

## Corrections
- Clarified DHCP policies and backup options.
- Corrected `cd ..` description (does not go to root; `/` does).