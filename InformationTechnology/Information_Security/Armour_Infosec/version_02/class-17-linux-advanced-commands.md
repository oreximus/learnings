# Class 17: Advanced Linux Commands and File Linking

## Theory Section

### File Linking in Linux

#### Hard Links

- **Definition**: Direct pointer to file content (inode)
- **Characteristics**:
  - Points directly to file data on disk
  - Survives original file deletion
  - Same inode number as original file
  - Cannot cross filesystem boundaries
  - Cannot link to directories

```bash
ln /var/log/messages my_hard_link
```

#### Soft Links (Symbolic Links)

- **Definition**: Pointer to file path/name
- **Characteristics**:
  - Points to file path, not content
  - Breaks if original file is deleted
  - Can cross filesystem boundaries
  - Can link to directories
  - Different inode number

```bash
ln -s /var/log/messages my_soft_link
```

#### Link Comparison

| Feature           | Hard Link            | Soft Link |
| ----------------- | -------------------- | --------- |
| Points to         | File content (inode) | File path |
| Survives deletion | Yes                  | No        |
| Cross filesystems | No                   | Yes       |
| Link directories  | No                   | Yes       |
| Disk space        | None                 | Minimal   |

### Text Viewing Commands

#### less Command

- **Purpose**: View file content page by page
- **Navigation**:
  - Space bar: Next page
  - Page Up/Page Down: Navigate pages
  - Arrow keys: Line by line navigation
  - q: Quit
  - /pattern: Search forward
  - ?pattern: Search backward

#### more Command

- **Purpose**: View file content page by page (older, less featured)
- **Navigation**:
  - Space bar: Next page
  - Enter: Next line
  - q: Quit

## Practical Section

### Advanced Command Chaining

#### Multiple Command Execution

```bash
# Sequential execution (regardless of success/failure)
ifconfig; date; ls

# Conditional AND execution (stop on failure)
ifconfig && date && id

# Conditional OR execution (continue until success)
command1 || command2 || command3
```

#### Background Process Management

```bash
# Run command in background
ping 8.8.8.8 &

# Run without terminal output
ping 8.8.8.8 >/dev/null &

# Manage background jobs
jobs                        # List background jobs
fg                          # Bring last job to foreground
bg                          # Send stopped job to background
kill %1                     # Kill job number 1
```

### Pipe Operations

#### Basic Pipe Usage

```bash
# Directory listing with pagination
ls -l /etc/ | less

# Sort directory contents
ls -l /etc/ | sort

# Search in command output
ps aux | grep apache

# Count lines in file
cat /etc/passwd | wc -l
```

#### Advanced Pipe Chains

```bash
# Complex text processing
cat /etc/passwd | grep "root" | sort | uniq

# Process analysis
ps aux | sort -nrk 3 | head -10

# Log analysis
cat /var/log/syslog | grep error | tail -20 | less

# Network analysis
netstat -tuln | grep LISTEN | sort
```

### System Monitoring Commands

#### Process Information

```bash
ps aux                  # Show all running processes
top                     # Real-time process viewer
htop                    # Enhanced process viewer (if installed)
```

#### System Load

```bash
uptime                  # System uptime and load average
w                       # Users and system load
```

#### Disk Usage

```bash
df -h                   # Filesystem disk usage
du -sh /path/*          # Directory sizes
iostat                  # I/O statistics (if installed)
```

### File Operations Examples

#### Creating and Viewing Files

```bash
# Create file with content
cat > example.txt << EOF
This is line 1
This is line 2
This is line 3
EOF

# View file with line numbers
cat -n example.txt

# View file with line numbers and end-of-line markers
cat -ne example.txt

# Remove multiple blank lines
cat -s file_with_blanks.txt
```

#### File Linking Examples

```bash
# Create original file
echo "Original content" > original.txt

# Create hard link
ln original.txt hard_link.txt

# Create soft link
ln -s original.txt soft_link.txt

# Check link information
ls -li original.txt hard_link.txt soft_link.txt

# Test link behavior
rm original.txt
cat hard_link.txt    # Still works
cat soft_link.txt    # Broken link
```

### Text Processing Examples

#### Pattern Matching with rm

```bash
rm A*                   # Remove files starting with 'A'
rm -vf file[!1]        # Remove all files except 'file1'
rm *.{txt,pdf}         # Remove all .txt and .pdf files
```

#### File Listing with Patterns

```bash
ls {*.txt,*.pdf}       # List .txt and .pdf files
ls file[1-3]*          # List files starting with file1, file2, file3
ls *.{doc,docx}        # List Word documents
```

### System Information Gathering

#### Comprehensive System Information

```bash
# System details
echo "Hostname: $(hostname)"
echo "OS: $(cat /etc/os-release | grep PRETTY_NAME | cut -d'"' -f2)"
echo "Kernel: $(uname -r)"
echo "Uptime: $(uptime -p)"
echo "Memory: $(free -h | grep Mem | awk '{print $3"/"$2}')"
echo "Disk Usage: $(df -h / | tail -1 | awk '{print $3"/"$2" ("$5")"}')"
```

#### Hardware Information

```bash
# CPU information
echo "CPU: $(lscpu | grep 'Model name' | cut -d':' -f2 | xargs)"

# Memory information
echo "Total Memory: $(free -h | grep Mem | awk '{print $2}')"

# Storage information
echo "Root Disk: $(df -h / | tail -1 | awk '{print $2}')"
```

## Study Questions

1. What are the practical differences between hard links and soft links?
2. How do command chaining operators (;, &&, ||) differ in behavior?
3. What are the advantages of using command pipes for text processing?
4. How can background processes improve system administration efficiency?

## Next Class Preview

- Domain Name System (DNS) fundamentals
- DNS record types and their purposes
- DNS server hierarchy and resolution process
