# Class 16-I: Linux Server Fundamentals

## Overview
This class covers basic Linux commands and terminal prompt information for server management.

## Basic Commands
- **Kernel Version**:
  ```bash
  uname -r
  ```
- **Disk Space**:
  ```bash
  df -h
  ```
- **Hostname**:
  ```bash
  hostname
  ```
- **Current Directory**:
  ```bash
  pwd
  ```
- **Help**:
  ```bash
  help
  ```
- **Manual**:
  ```bash
  man <command>
  ```

## Terminal Prompt
- **Format**: `user@hostname:directory$`
  - **user**: Current user (e.g., `root`).
  - **hostname**: System hostname (e.g., `localhost.localdomain`).
  - **directory**: Current directory (e.g., `~` for home).
  - **$**: Normal user; `#` for root.

## Link-Local Addressing
- **Definition**: Automatically assigned IPs (169.254.0.0/16) when DHCP fails.
- **Example**: `169.254.x.x`

## Corrections
- Added `df -h` for disk space and clarified link-local addressing.
- Completed the section with terminal prompt details.