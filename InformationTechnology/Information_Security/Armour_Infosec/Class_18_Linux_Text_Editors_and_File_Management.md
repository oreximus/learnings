# Class 18: Linux Text Editors and Basic File Management

## Overview

This class covers essential command-line tools for file and directory management, as well as an introduction to common text editors in Linux.

## 1. File and Directory Management

### `mkdir`: Create Directories

* **Create a single directory**: `mkdir my_directory`.
* **Create multiple directories**: `mkdir dir1 dir2 dir3`.
* **Create nested directories (recursively)**: `mkdir -p parent/child/grandchild`. The `-p` option creates parent directories if they don't exist.

### `touch`: Create Empty Files

* **Create a single empty file**: `touch filename.txt`.
* **Create a file with spaces in the name**: `touch "my new file.txt"`.
* `touch` can also be used to update the modification timestamp of an existing file.

### `rm` and `rmdir`: Remove Files and Directories

* **`rmdir`**: Removes **only empty** directories.
    * `rmdir empty_dir`.
    * `rmdir -p parent/child` removes the child and then the parent if it becomes empty.
* **`rm`**: Removes files and directories.
    * **Remove a file**: `rm filename.txt`.
    * **Remove a file without confirmation**: `rm -f filename.txt` (`-f` for force).
    * **Remove a directory and its contents recursively**: `rm -r my_directory`.
    * **Force remove recursively with verbose output**: `rm -rfv my_directory`.
    * **Remove using wildcards**: `rm -vf A*` removes all files starting with 'A'.

---

## 2. Viewing and Editing Files

### `cat`: Concatenate and Display Files

The `cat` command is primarily used to display the content of files.

* **View a file**: `cat filename.txt`.
* **View multiple files**: `cat file1 file2`.
* **Create a new file (overwrite)**: `cat > newfile.txt`. Type content, then press `Ctrl+D` to save and exit.
* **Append to a file**: `cat >> existingfile.txt`. Type content, then press `Ctrl+D`.
* **Combine files**: `cat file1 file2 > combined_file.txt`.
* **Display with line numbers**: `cat -n filename.txt`.
* **Squeeze multiple blank lines**: `cat -s filename.txt` removes repeated empty lines.

### `nano`: Simple Text Editor

`nano` is a beginner-friendly, modeless command-line text editor.

* **Open/Create a file**: `nano filename.txt`.
* **Key Commands** (displayed at the bottom of the screen):
    * `Ctrl + O`: Write Out (Save the file).
    * `Ctrl + X`: Exit `nano`.
    * `Ctrl + K`: Cut the current line.
    * `Ctrl + U`: Uncut (Paste the line).

### `vim`: Powerful Modal Text Editor

`vim` (Vi IMproved) is a highly powerful and efficient modal text editor. It has different modes for different operations.

* **Open/Create a file**: `vim filename.txt`.
* **Basic Modes**:
    * **Normal Mode**: Default mode for navigation and commands. Press `Esc` to enter this mode.
        * `h, j, k, l`: Left, down, up, right navigation.
        * `dd`: Delete a line.
        * `yy`: Yank (copy) a line.
        * `p`: Paste a line.
    * **Insert Mode**: For typing text. Press `i` to enter Insert Mode from Normal Mode.
    * **Command-Line Mode**: For saving, quitting, and other commands. From Normal Mode, type `:` to enter.
        * `:w`: Write (save) the file.
        * `:q`: Quit.
        * `:wq`: Write and quit (save and exit).
        * `:q!`: Quit without saving changes.

