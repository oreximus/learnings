# Class 24: Linux I/O Redirection

## Overview

This class explains the three standard data streams in Unix-like operating systems and how to redirect them to control the input and output of commands.

## Standard Data Streams

In Linux, every process gets three standard data streams when it starts.

### 1. Standard Input (stdin)

* **Description**: The default source of input for a command.
* **File Descriptor**: `0`.
* **Default**: Keyboard input.
* **Example**: When you run `cat` without a filename, it waits for input from `stdin` (your keyboard).

### 2. Standard Output (stdout)

* **Description**: The default destination for a command's normal output.
* **File Descriptor**: `1`.
* **Default**: The terminal screen.
* **Example**: The `ls` command sends its list of files to `stdout`.

### 3. Standard Error (stderr)

* **Description**: The default destination for a command's error messages.
* **File Descriptor**: `2`.
* **Default**: The terminal screen.
* **Example**: `ls nonexistentfile` will send an error message like "cannot access 'nonexistentfile': No such file or directory" to `stderr`.

## Redirection Operators

Redirection allows you to change where the standard streams go.

#### Redirecting `stdout`

* **`>` (Overwrite)**: Redirects `stdout` to a file, overwriting the file if it exists.
    ```bash
    # Save the output of ls to a file
    ls -l > file_list.txt
    ```
   

* **`>>` (Append)**: Redirects `stdout` to a file, appending the output to the end of the file.
    ```bash
    date >> log.txt
    ```

#### Redirecting `stderr`

You must specify the file descriptor `2` to redirect standard error.

* **`2>` (Overwrite)**: Redirects `stderr` to a file.
    ```bash
    # Save only the error messages to a file
    ls nonexistentfile 2> error.log
    ```
   

* **`2>>` (Append)**: Appends `stderr` to a file.

#### Redirecting Both `stdout` and `stderr`

* **Method 1 (Modern Bash)**: `&>`
    ```bash
    # Redirect both stdout and stderr to the same file
    cat /etc/passwd /etc/shadow &> command_output.txt
    ```
   

* **Method 2 (Traditional)**: `> ... 2>&1`
    This redirects `stdout` to a file (`>`) and then redirects `stderr` (`2`) to the same place as `stdout` (`&1`). The order is important.
    ```bash
    cat /etc/passwd /etc/shadow > command_output.txt 2>&1
    ```
   

#### Redirecting to `/dev/null`

`/dev/null` is a special file that discards all data written to it. It's useful for suppressing unwanted output.

```bash
# Run a command and throw away all its output (both stdout and stderr)
ping 8.8.8.8 > /dev/null 2>&1 &
```


#### Redirecting `stdin`

* **`<`**: Takes input from a file instead of the keyboard.
    ```bash
    # Use data.txt as input for the sort command
    sort < data.txt
    ```

