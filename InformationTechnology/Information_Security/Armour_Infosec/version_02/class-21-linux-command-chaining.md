# Class 21: Linux Command Chaining and Process Management

## Theory Section

### Command Execution Methods

#### Sequential Execution (;)

```bash
ifconfig; date; ls
# Executes commands one after another regardless of success/failure
```

#### Conditional AND Execution (&&)

```bash
ifconfig && date && id
# Executes next command only if previous command succeeds
```

#### Conditional OR Execution (||)

```bash
ifconfig || date || id
# Executes next command only if previous command fails
```

### Background Process Management

#### Running Commands in Background

```bash
ping 8.8.8.8 &
# Runs command in background, returns control to shell
```

#### Background Process Control

```bash
jobs                    # Show background jobs
fg                      # Bring last background job to foreground
bg                      # Send stopped job to background
kill %1                 # Kill job number 1
```

#### Suppressing Output

```bash
ping 8.8.8.8 >/dev/null &
# Run in background without showing output on terminal
```

### Pipe Operations

#### Basic Pipe Concept

- **Purpose**: Take output of one command as input to another
- **Symbol**: | (pipe character)
- **Data Flow**: Command1 | Command2 | Command3

#### Pipe Examples

```bash
# Directory listing with pagination
ls -l /etc/ | less

# Sorting directory contents
ls -l /etc/ | sort

# Searching in file contents
cat /etc/passwd | grep root

# Counting lines in file
cat /etc/passwd | wc -l

# Process sorting by CPU usage
ps aux | sort -nrk 3

# Command chaining with pipes
cat /etc/passwd | grep "root" | sort | uniq
```

## Practical Section

### Advanced Command Chaining

#### System Information Gathering

```bash
# Comprehensive system info
uname -a && cat /etc/os-release && free -h && df -h

# Network information chain
ifconfig && route -n && cat /etc/resolv.conf

# Process monitoring chain
ps aux | grep -v grep | sort -nrk 3 | head -10
```

#### File Processing Chains

```bash
# Find and process log files
find /var/log -name "*.log" | head -5

# User account analysis
cat /etc/passwd | cut -d: -f1,3,6 | sort -t: -k2 -n

# Disk usage analysis
du -h /var/log/* 2>/dev/null | sort -hr | head -10
```

### Background Process Management

#### Long-Running Tasks

```bash
# Start backup in background
tar -czf backup.tar.gz /home/user/ &

# Monitor system resources
top &

# Network monitoring
ping -c 1000 8.8.8.8 > ping_results.txt &
```

#### Process Control Examples

```bash
# Start multiple background jobs
ping google.com &
ping yahoo.com &
ping microsoft.com &

# List all jobs
jobs

# Bring specific job to foreground
fg %2

# Kill specific background job
kill %1
```

### Text Processing with Pipes

#### Log Analysis

```bash
# Analyze system logs
grep -i error /var/log/syslog | tail -20

# Count occurrences of a pattern
grep -c 'pattern' filename

# Show context around matches
grep -A 3 -B 3 'pattern' filename  # 3 lines after and before
```

#### System Monitoring

```bash
# Memory usage by process
ps aux | sort -nrk 4 | head -10

# Network connections
netstat -tuln | grep LISTEN | sort

# Disk usage summary
df -h | grep -v tmpfs | sort -k5 -nr
```

### Standard Data Streams

#### Standard Input (stdin) - File Descriptor 0

```bash
# Reading from stdin
cat                     # Read from keyboard input
cat < file.txt          # Read from file
echo "data" | command   # Pipe data to command
```

#### Standard Output (stdout) - File Descriptor 1

```bash
# Redirecting stdout
ls > file.txt           # Redirect output to file
ls >> file.txt          # Append output to file
ls | less               # Pipe output to another command
```

#### Standard Error (stderr) - File Descriptor 2

```bash
# Redirecting stderr
ls nonexistent 2>error.txt              # Redirect errors to file
command 2>/dev/null                     # Discard error messages
command >output.txt 2>error.txt         # Separate output and errors
command &>combined.txt                  # Combine output and errors
command >output.txt 2>&1                # Redirect errors to same file as output
```

### Practical Redirection Examples

```bash
# Separate normal output and errors
cat /etc/passwd /etc/shadow 1>output.txt 2>error.txt

# Combine both streams
cat /etc/passwd /etc/shadow &>combined.txt

# Alternative syntax for combining
cat /etc/passwd /etc/shadow >combined.txt 2>&1
```

### Exit Code Checking

```bash
echo $?                 # Check exit code of last command
# 0 = success, non-zero = failure
```

### Advanced Text Processing

#### Complex Processing Chains

```bash
# Find most common words in a file
cat file.txt | tr ' ' '\n' | sort | uniq -c | sort -nr | head -10

# Process analysis with filtering
ps aux | awk '{print $2, $3, $11}' | sort -nrk 2 | head -10

# Network analysis
netstat -tuln | awk '{print $4}' | cut -d: -f1 | sort | uniq -c
```

#### File Operations with Pipes

```bash
# Find files and process them
find /var/log -name "*.log" -type f | xargs wc -l | sort -n

# Search and replace in multiple files
find . -name "*.txt" | xargs sed -i 's/old/new/g'

# Archive files older than 30 days
find /tmp -type f -mtime +30 | tar -czf old_files.tar.gz -T -
```

## Study Questions

1. How do command chaining operators (;, &&, ||) differ in behavior?
2. When would you use background processes in system administration?
3. How do pipes enable complex text processing workflows?
4. What are the practical applications of standard stream redirection?

## Next Class Preview

- Advanced text processing with grep
- Regular expressions and pattern matching
- System monitoring and log analysis
