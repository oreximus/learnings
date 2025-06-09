# Class 15-I: Linux Init Levels

## Overview
This class covers Linux runlevels (init levels) and how to manage them.

## Runlevels
- **Definition**: States defining system services and operational modes.
- **Systemd Targets** (modern equivalent of runlevels):
  - **0**: Poweroff (halt)
  - **1**: Single-user mode (rescue)
  - **2**: Multi-user mode without networking
  - **3**: Multi-user mode with networking (CLI)
  - **4**: Unused
  - **5**: Multi-user mode with GUI
  - **6**: Reboot

## Commands
- **Check Current Runlevel**:
  ```bash
  runlevel
  ```
  - Output: `N 5` (N = previous runlevel, 5 = current).
- **Change Runlevel** (Systemd):
  ```bash
  systemctl set-default graphical.target  # Sets runlevel 5
  ```
- **View Current Target**:
  ```bash
  systemctl get-default
  ```

## Corrections
- Completed the incomplete section with systemd details (modern Linux uses systemd, not SysV init).
- Added commands for runlevel management.