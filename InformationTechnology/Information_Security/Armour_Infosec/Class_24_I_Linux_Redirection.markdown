# Class 24-I: Linux Redirection

## Overview
This class covers standard data streams and redirection in Linux.

## Standard Data Streams
1. **Standard Input (stdin)**:
   - **File Descriptor**: 0
   - **Default**: Keyboard
   - **Example**:
     ```bash
     cat /dev/stdin
     bc  # Interactive input
     ```
2. **Standard Output (stdout)**:
   - **File Descriptor**: 1
   - **Example**:
     ```bash
     ls -l > list_output.txt
     ```
3. **Standard Error (stderr)**:
   - **File Descriptor**: 2
   - **Example**:
     ```bash
     ls nonexistentfile 2> error.txt
     ```

## Redirection Examples
- **Separate stdout and stderr**:
  ```bash
  cat /etc/passwd /etc/shadow 1> output.txt 2> error.txt
  ```
- **Combine stdout and stderr**:
  ```bash
  cat /etc/passwd /etc/shadow &> both_error.txt
  cat /etc/passwd /etc/shadow > both_error.txt 2>&1
  ```

## Exit Code
- **Check Exit Code**:
  ```bash
  echo $?
  ```
  - 0 = Success, non-zero = Failure.

## Corrections
- Corrected `wl -n` to `wc -l` in previous notes.
- Added `bc` example for stdin.