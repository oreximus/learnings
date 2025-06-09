# Class 16-II: Linux DHCP and Basic Commands

## Overview
This class covers DHCP configuration on Linux and basic file manipulation commands.

## DHCP Configuration (Linux)
- **Tool**: `dhcpd` (ISC DHCP Server)
- **Steps**:
  1. Install: `sudo dnf install dhcp-server` (RHEL/CentOS).
  2. Configure Scope:
     - Edit `/etc/dhcp/dhcpd.conf`:
       ```conf
       subnet 192.168.1.0 netmask 255.255.255.0 {
           range 192.168.1.100 192.168.1.200;
           option routers 192.168.1.1;
           option domain-name-servers 8.8.8.8;
           option lease-duration 86400; # 24 hours
       }
       ```
  3. Start Service: `sudo systemctl start dhcpd`
  4. Enable on Boot: `sudo systemctl enable dhcpd`
- **DORA Process**:
  - **Discover**: Client broadcasts (UDP 67).
  - **Offer**: Server responds with IP offer.
  - **Request**: Client requests the IP.
  - **Acknowledge**: Server assigns the IP.
- **Verification**: Use Wireshark, filter `udp.port == 67`.

## Basic Commands
1. **touch**:
   ```bash
   touch filename
   touch "file with spaces"
   ```
2. **cat**:
   ```bash
   cat filename
   cat > filename  # Create/overwrite file
   ```
3. **mkdir**:
   ```bash
   mkdir dir
   mkdir -p dir1/dir2/dir3  # Recursive
   ```
4. **rmdir/rm**:
   ```bash
   rmdir dir  # Empty directories
   rm -f file  # Force delete
   rm -rf dir  # Recursive force delete
   rm -vf A*   # Delete with pattern
   ```

## Corrections
- Completed DHCP configuration section with Linux-specific steps.
- Added Wireshark usage for DORA process verification.