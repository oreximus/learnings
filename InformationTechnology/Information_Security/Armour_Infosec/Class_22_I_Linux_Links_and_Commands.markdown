# Class 22-I: Linux Links and Commands

## Overview
This class covers file linking and additional Linux commands for system information.

## File Links
- **Hard Links**:
  ```bash
  ln /var/log/messages my_hard_link
  ```
  - Points to file content; persists if original file is deleted.
- **Soft Links (Symbolic)**:
  ```bash
  ln -s /var/log/messages my_soft_link
  ```
  - Points to file path; breaks if original file is deleted.

## Navigation Commands
- **less/more**:
  ```bash
  less filename
  more filename
  ```
  - Navigation: Space (next page), arrows (line-by-line), `q` (quit).

## System Identification
- **id**:
  ```bash
  id
  ```
  - Shows user ID, group ID, and context.
- **tty**:
  ```bash
  tty
  ```
  - Shows terminal device (e.g., `/dev/pts/1`).
- **whoami**:
  ```bash
  whoami
  ```
  - Shows current username.
- **who -a**:
  ```bash
  who -a
  ```
  - Lists all users and sessions.
- **w**:
  ```bash
  w
  ```
  - Shows user activity and system load.

## Host Information
- **hostname**:
  ```bash
  hostname
  hostname -a  # Aliases
  hostname -i  # IPs
  ```
- **uname**:
  ```bash
  uname -r     # Kernel release
  uname -mrs   # Machine, release, system
  ```

## Date and Time
- **cal**:
  ```bash
  cal 6 2025  # Calendar for June 2025
  ```
- **date**:
  ```bash
  date
  ```

## Corrections
- Completed incomplete sections (e.g., `uname` options).
- Clarified hard vs. soft link behavior.