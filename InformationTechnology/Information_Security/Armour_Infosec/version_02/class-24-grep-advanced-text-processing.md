# Class 24: Advanced Text Processing with grep and Pattern Matching

## Theory Section - grep Command Fundamentals

### What is grep?

- **grep**: Global Regular Expression Print
- **Purpose**: Search for patterns in text files or command output
- **Usage**: Essential tool for system administration and log analysis
- **Power**: Supports regular expressions for complex pattern matching

### Basic grep Syntax

```bash
grep [options] pattern [file(s)]
```

## Practical Section - grep Command Examples

### Removing Empty Lines and Comments

#### Removing Empty Lines

```bash
# Remove all empty lines from a file
grep -v '^$' file-name
```

- **^**: Beginning of line anchor
- **$**: End of line anchor
- **^$**: Matches lines that start and end immediately (empty lines)
- **-v**: Invert match (show lines that DON'T match)

#### Removing Comments

```bash
# Remove lines starting with # (comments)
grep -v '^#' file-name
```

- **^#**: Lines that start with # character
- **-v**: Show lines that don't start with #

#### Removing Both Empty Lines and Comments

```bash
# Method 1: Using pipe
grep -v '^#' file-name | grep -v '^$'

# Method 2: Using extended regex (more efficient)
grep -Ev "(^#|^$)" file-name
```

- **-E**: Extended regular expressions
- **|**: OR operator in regex
- **(^#|^$)**: Match lines starting with # OR empty lines

### Pattern Matching Examples

#### Filtering Content Starting with Specific Text

```bash
# Filter lines starting with 'log'
grep '^log' file-name
```

#### Character Class Matching

```bash
# Filter lines containing 'a' or 'n'
grep "[an]" file-name
```

- **[an]**: Character class matching either 'a' or 'n'

#### Using Pattern Files

```bash
# Match patterns from one file against another file
grep -f file-with-the-pattern file-to-match-the-pattern
```

- **-f**: Read patterns from file
- **file-with-the-pattern**: File containing search patterns (one per line)
- **file-to-match-the-pattern**: File to search in

### POSIX Character Classes

#### Alphabetic Characters

```bash
# Filter lines containing alphabetic characters
grep "[[:alpha:]]" filename
```

#### Alphanumeric Characters

```bash
# Filter lines containing letters and numbers
grep "[[:alnum:]]" filename
```

#### Uppercase Letters

```bash
# Filter lines containing uppercase letters
grep "[[:upper:]]" filename
```

#### Lowercase Letters

```bash
# Filter lines containing lowercase letters
grep "[[:lower:]]" filename
```

#### Numeric Characters

```bash
# Filter lines containing numbers
grep "[[:digit:]]" filename
```

### Command Output Filtering

#### Network Interface Filtering

```bash
# Filter 'inet' from ifconfig command output
ifconfig | grep 'inet '
```

- **Note**: Space after 'inet' to avoid matching 'inet6'

#### Process Filtering

##### Filtering Root Processes

```bash
# Show processes running as root
ps aux | grep '^root'
```

##### Filtering Non-Root Processes

```bash
# Show processes NOT running as root
ps aux | grep -v '^root'
```

### Advanced grep Options

#### Recursive Directory Search

```bash
# Search for pattern recursively in directory
grep -inr "/path/" /directory/ 2>/dev/null
```

- **-i**: Case-insensitive search
- **-n**: Show line numbers
- **-r**: Recursive search through directories
- **2>/dev/null**: Suppress error messages

#### File Name Only Output

```bash
# Show only filenames containing the pattern
grep -ilR "/path/" /directory/ 2>/dev/null
```

- **-l**: Show only filenames (not content)
- **-R**: Recursive search (same as -r)

### Pattern Matching with Repetition

#### Exact Number Matching

```bash
# Match exactly four digits
grep '[0-9][0-9][0-9][0-9]' /etc/passwd

# Show only the matched portion
grep '[0-9][0-9][0-9][0-9]' /etc/passwd -o
```

- **-o**: Show only the matched part of the line

#### Advanced Pattern Examples

```bash
# Match lines containing single character after 'name'
grep "name." filename

# Match lines containing double character after 'name'
grep "name.." filename

# Match lines containing triple character after 'name'
grep "name..." filename
```

- **.**: Matches any single character

#### Number Pattern Matching

```bash
# Match 'name' followed by exactly three digits
grep "name[0-9][0-9][0-9]" filename

# Match numbers starting with 9 followed by two digits
grep "9[0-9][0-9]" filename
```

### Character Range Matching

#### Alphabetic Ranges

```bash
# Match lowercase letters
grep '[a-z]' filename

# Case-insensitive alphabetic matching
grep -i '[a-z]' filename
```

#### Numeric Ranges

```bash
# Match four-digit numbers (regular users in /etc/passwd)
grep "[0-9][0-9][0-9][0-9]" /etc/passwd

# Show only the matched four-digit numbers
grep "[0-9][0-9][0-9][0-9]" /etc/passwd -o
```

## Advanced grep Techniques

### Regular Expression Anchors

```bash
# Beginning of line
grep '^pattern' file

# End of line
grep 'pattern$' file

# Whole word matching
grep '\bword\b' file

# Case-insensitive search
grep -i 'pattern' file
```

### Combining grep with Other Commands

#### Log Analysis Examples

```bash
# Find error messages in system logs
grep -i error /var/log/syslog | tail -20

# Count occurrences of a pattern
grep -c 'pattern' filename

# Show context around matches
grep -A 3 -B 3 'pattern' filename  # 3 lines after and before
```

#### System Administration Examples

```bash
# Find listening ports
netstat -tuln | grep LISTEN

# Find specific processes
ps aux | grep -v grep | grep apache

# Search configuration files
grep -r "ServerName" /etc/apache2/

# Find files modified today
find /var/log -name "*.log" -mtime 0 | xargs grep -l "error"
```

### Practical Exercises

#### Exercise 1: Log File Cleaning

```bash
# Create a sample configuration file with comments and empty lines
cat > sample.conf << EOF
# This is a configuration file
ServerName example.com

# Database settings
DatabaseHost localhost
DatabasePort 3306

# Cache settings

CacheEnabled true
# End of file
EOF

# Clean the file (remove comments and empty lines)
grep -Ev "(^#|^$)" sample.conf
```

#### Exercise 2: User Analysis

```bash
# Find all regular users (UID >= 1000)
grep "[0-9][0-9][0-9][0-9]" /etc/passwd

# Extract usernames of regular users
grep "[0-9][0-9][0-9][0-9]" /etc/passwd | cut -d: -f1

# Find users with bash shell
grep "/bin/bash$" /etc/passwd
```

#### Exercise 3: Network Analysis

```bash
# Find all IP addresses in log files
grep -oE '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}' /var/log/auth.log

# Find failed SSH login attempts
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c

# Find successful SSH logins
grep "Accepted password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c
```

### Windows User and Group Management

#### User Account Management

- **Public Directory**: Contains files accessible by any user
- **Shared Folders**: Visible under Computer Management → Shared Folders
- **Remote Access**: Access shared folders via IP address in Run dialog

#### Accessing Shared Resources

```cmd
# In Run dialog (Windows + R)
\\192.168.2.21
```

#### Remote Desktop Connection

```cmd
# In Run dialog
mstsc
```

- **mstsc**: Microsoft Terminal Services Client
- **Purpose**: Remote desktop connection to other Windows machines

### Backup Operator Group

- **Purpose**: Special Windows group with backup and restore privileges
- **Permissions**: Can backup and restore files regardless of file permissions
- **Usage**: Assigned to users who need to perform system backups
- **Security**: Members can bypass normal file security for backup purposes

## Study Questions

1. How do regular expressions enhance text searching capabilities?
2. What are the advantages of using POSIX character classes?
3. How can grep be combined with other commands for system administration?
4. What is the difference between basic and extended regular expressions in grep?

## Next Class Preview

- Advanced shell scripting techniques
- System automation and cron jobs
- Security monitoring and intrusion detection
- Performance optimization strategies
