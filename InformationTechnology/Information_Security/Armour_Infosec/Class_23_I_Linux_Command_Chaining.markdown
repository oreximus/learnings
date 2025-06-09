# Class 23-I: Linux Command Chaining

## Overview
This class covers methods to chain Linux commands and manage background processes.

## Command Chaining
- **Multiple Commands**:
  ```bash
  ifconfig; date; ls
  ```
- **AND Operator** (`&&`):
  ```bash
  ifconfig && date && id
  ```
  - Runs next command only if the previous succeeds.
- **OR Operator** (`||`):
  ```bash
  ifconfig || date || id
  ```
  - Runs next command if the previous fails.

## Background Processes
- **Run in Background**:
  ```bash
  ping 8.8.8.8 &
  ```
- **Suppress Output**:
  ```bash
  ping 8.8.8.8 >/dev/null &
  ```
- **View Jobs**:
  ```bash
  jobs
  ```
- **Bring to Foreground**:
  ```bash
  fg
  ```

## Pipes
- **Purpose**: Use one command’s output as input for another.
- **Examples**:
  ```bash
  ls -l /etc | less
  ls -l /etc | sort
  cat /etc/passwd | grep root
  cat /etc/passwd | wc -l
  cat /etc/passwd | grep root | sort | uniq
  ```

## Corrections
- Clarified `&&` and `||` behavior.
- Corrected `wl -n` to `wc -l` for line counting.