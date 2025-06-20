# Class 22: Linux Pattern Matching with grep and Pipes

## Overview

This class focuses on two powerful command-line concepts: command chaining with pipes and logical operators, and text processing with `grep` (Global Regular Expression Print).

## 1. Command Chaining and Background Processes

You can run multiple commands in sequence from a single line.

* **Semicolon (`;`)**: Runs commands sequentially, regardless of whether the previous command succeeded or failed.
    * `ifconfig; date; ls`
* **Logical AND (`&&`)**: Runs the next command **only if** the previous command was successful (exited with a code of 0).
    * `ifconfig && date && id`
* **Logical OR (`||`)**: Runs the next command **only if** the previous command failed.
    * `ifconfig || date || id`

### Background Processes

* **Ampersand (`&`)**: Runs a command in the background, freeing up your terminal.
    * `ping 8.8.8.8 &`
* **`jobs`**: Lists all background processes running in the current shell.
* **`fg`**: Brings the most recently backgrounded job to the foreground.

## 2. Pipes (`|`)

A pipe takes the standard output (stdout) of one command and uses it as the standard input (stdin) for the next command. This is fundamental for building powerful command-line workflows.

#### Pipe Examples:

* **Paging through output**: `ls -l /etc/ | less`
* **Sorting output**: `ls -l /etc/ | sort`
* **Counting lines**: `cat /etc/passwd | wc -l` (Note: `wl -n` in notes is likely a typo for `wc -l`).
* **Chaining multiple pipes**: `cat /etc/passwd | grep "root" | sort | uniq`

---

## 3. Practical: Text Processing with `grep`

`grep` searches for patterns in text. It can search within files or within the output of other commands (via pipes).

#### Basic Syntax

`grep [options] pattern [file...]`

#### Key `grep` Options

* `-i`: Case-insensitive search.
* `-v`: Invert match (show lines that *do not* match the pattern).
* `-r` or `-R`: Recursive search through directories.
* `-n`: Show the line number of each match.
* `-w`: Match only whole words.
* `-c`: Count the number of matching lines.
* `-l`: List only the names of files that contain the pattern.
* `-E`: Use extended regular expressions (same as `egrep`).
* `-A <num>`, `-B <num>`, `-C <num>`: Show lines After, Before, or around (Context) the match.

#### `grep` Exercises

1.  **Basic search in a file**:
    ```bash
    grep root /etc/passwd
    ```
   

2.  **Using `grep` with a pipe**:
    ```bash
    cat /etc/passwd | grep root
    ```
   

3.  **Search in multiple files**:
    ```bash
    grep root /etc/passwd /etc/shadow
    ```
   

4.  **Case-insensitive search**:
    ```bash
    grep -i RooT /etc/passwd
    ```
   

5.  **Search for a pattern with spaces** (use quotes):
    ```bash
    grep "Session Started" /var/log/auth.log
    ```
   

6.  **Find lines that *do not* contain a pattern**:
    ```bash
    grep -v "failed" /var/log/auth.log
    ```
   

7.  **Search for multiple patterns** (using extended grep):
    ```bash
    grep -E "(root|daemon)" /etc/passwd
    ```
   

8.  **Match start of line (`^`)**: Find all commented-out lines.
    ```bash
    grep "^#" /etc/ssh/sshd_config
    ```
   

9.  **Match end of line (`$`)**: Find all users with the `/bin/bash` shell.
    ```bash
    grep "/bin/bash$" /etc/passwd
    ```

