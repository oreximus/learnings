# Class 21-I: Linux File Operations

## Overview
This class covers Linux commands for file and directory operations.

## cp Command
- **Purpose**: Copy files/directories.
- **Examples**:
  ```bash
  cp /etc/passwd ~/Desktop
  cp /etc/passwd /etc/hosts ~/Desktop
  cp -vr /var/log/* /root/Desktop/d1
  cp -rv /var/log/*.log /root/Desktop/d1
  cp ca* /root/Desktop/
  cp hel? /root/Desktop/d1
  cp file[0-8] /root/Desktop/d1
  cp [hd]ello /root/Desktop/d1
  cp file[!1] /root/Desktop/d1
  cp {*.txt,*.pdf} /root/Desktop/d1
  cp -rv /etc/*.conf /root/Desktop/d1
  ```

## mv Command
- **Purpose**: Move or rename files/directories.
- **Options**: Same as `cp` (e.g., `-v`, `-r`, wildcards).

## Corrections
- Clarified `mv` command usage, which was mentioned but not detailed.
- Added examples for consistency.