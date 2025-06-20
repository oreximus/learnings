# Class 23: Advanced Text Processing and Pattern Matching

## Theory Section

### Text Processing Importance

- **System Administration**: Analyzing log files and configuration files
- **Data Analysis**: Extracting information from large text files
- **Automation**: Processing command output in scripts
- **Troubleshooting**: Finding specific patterns in system outputs

### Regular Expressions (Regex)

- **Definition**: Patterns used to match character combinations in strings
- **Power**: Enable complex pattern matching beyond simple text searches
- **Applications**: Text searching, validation, data extraction, text replacement

#### Basic Regex Concepts

- **Literal Characters**: Match exact characters (a, b, 1, 2)
- **Metacharacters**: Special characters with special meaning (., \*, +, ?, ^, $)
- **Character Classes**: Match any character from a set ([abc], [0-9])
- **Anchors**: Match positions in text (^, $)
- **Quantifiers**: Specify how many times to match (\*, +, ?, {n})

### grep Command Fundamentals

- **grep**: Global Regular Expression Print
- **Purpose**: Search for patterns in text files or command output
- **Usage**: Essential tool for system administration and log analysis
- **Power**: Supports regular expressions for complex pattern matching

## Practical Section

### Basic grep Usage

#### Simple Pattern Matching

```bash
# Search for exact text
grep "error" /var/log/syslog

# Case-insensitive search
grep -i "error" /var/log/syslog

# Show line numbers
grep -n "error" /var/log/syslog

# Count matches
grep -c "error" /var/log/syslog
```

#### File and Directory Operations

```bash
# Search in multiple files
grep "pattern" file1.txt file2.txt

# Recursive search in directories
grep -r "pattern" /var/log/

# Show only filenames with matches
grep -l "pattern" *.txt

# Show filenames without matches
grep -L "pattern" *.txt
```

### Advanced grep Options

#### Context and Output Control

```bash
# Show lines before and after match
grep -A 3 -B 3 "error" /var/log/syslog  # 3 lines after and before
grep -C 5 "error" /var/log/syslog       # 5 lines of context

# Show only matching part
grep -o "pattern" file.txt

# Invert match (show non-matching lines)
grep -v "pattern" file.txt

# Quiet mode (no output, just exit status)
grep -q "pattern" file.txt
```

#### Pattern Matching with Regex

##### Anchors

```bash
# Lines starting with pattern
grep "^error" /var/log/syslog

# Lines ending with pattern
grep "error$" /var/log/syslog

# Whole word matching
grep "\berror\b" /var/log/syslog
```

##### Character Classes

```bash
# Match any digit
grep "[0-9]" file.txt

# Match any letter
grep "[a-zA-Z]" file.txt

# Match specific characters
grep "[aeiou]" file.txt

# Negate character class
grep "[^0-9]" file.txt  # Non-digits
```

##### POSIX Character Classes

```bash
# Alphabetic characters
grep "[[:alpha:]]" file.txt

# Alphanumeric characters
grep "[[:alnum:]]" file.txt

# Digits
grep "[[:digit:]]" file.txt

# Uppercase letters
grep "[[:upper:]]" file.txt

# Lowercase letters
grep "[[:lower:]]" file.txt

# Whitespace
grep "[[:space:]]" file.txt
```

### Practical Text Processing Examples

#### Log File Analysis

```bash
# Find error messages
grep -i "error\|fail\|critical" /var/log/syslog

# Find IP addresses
grep -o "[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}" /var/log/auth.log

# Find failed login attempts
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c

# Find successful logins
grep "Accepted password" /var/log/auth.log | awk '{print $9, $11}'
```

#### System Configuration Analysis

```bash
# Remove comments and empty lines from config files
grep -v "^#" /etc/ssh/sshd_config | grep -v "^$"

# Find active configuration lines
grep -v "^#\|^$" /etc/apache2/apache2.conf

# Search for specific configuration
grep -i "port" /etc/ssh/sshd_config
```

#### Process and System Analysis

```bash
# Find processes by name
ps aux | grep -v grep | grep apache

# Find listening ports
netstat -tuln | grep LISTEN | grep ":80"

# Find large files
ls -la | grep "^-" | sort -k5 -nr | head -10
```

### Advanced Pattern Matching

#### Extended Regular Expressions (grep -E)

```bash
# Alternative patterns (OR)
grep -E "error|warning|critical" /var/log/syslog

# One or more occurrences
grep -E "a+" file.txt

# Zero or more occurrences
grep -E "a*" file.txt

# Zero or one occurrence
grep -E "a?" file.txt

# Specific number of occurrences
grep -E "a{3}" file.txt      # Exactly 3 a's
grep -E "a{2,5}" file.txt    # 2 to 5 a's
grep -E "a{3,}" file.txt     # 3 or more a's
```

#### Complex Pattern Examples

```bash
# Email addresses
grep -E "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" file.txt

# Phone numbers (US format)
grep -E "$$[0-9]{3}$$ [0-9]{3}-[0-9]{4}" file.txt

# URLs
grep -E "https?://[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" file.txt

# Time stamps (HH:MM:SS)
grep -E "[0-9]{2}:[0-9]{2}:[0-9]{2}" /var/log/syslog
```

### Combining grep with Other Commands

#### Pipeline Processing

```bash
# Process output and search
ps aux | grep -v grep | grep apache | awk '{print $2, $11}'

# Log analysis pipeline
cat /var/log/apache2/access.log | grep "404" | awk '{print $1}' | sort | uniq -c | sort -nr

# System monitoring
df -h | grep -v "tmpfs" | grep -E "[8-9][0-9]%|100%" # Find filesystems > 80% full
```

#### File Processing

```bash
# Find and process files
find /var/log -name "*.log" | xargs grep -l "error"

# Search in compressed files
zgrep "pattern" /var/log/*.gz

# Search in multiple file types
grep -r --include="*.txt" --include="*.log" "pattern" /path/
```

### Text Filtering and Cleaning

#### Removing Unwanted Content

```bash
# Remove empty lines
grep -v "^$" file.txt

# Remove comments
grep -v "^#" file.txt

# Remove both empty lines and comments
grep -Ev "(^#|^$)" file.txt

# Remove lines containing specific pattern
grep -v "unwanted_pattern" file.txt
```

#### Data Extraction

```bash
# Extract specific fields
grep "pattern" file.txt | cut -d: -f1,3

# Extract and count unique values
grep "pattern" file.txt | awk '{print $2}' | sort | uniq -c

# Extract between patterns
grep -A 10 "START" file.txt | grep -B 10 "END"
```

## Study Questions

1. How do regular expressions enhance text searching capabilities?
2. What are the advantages of using POSIX character classes?
3. How can grep be combined with other commands for complex text processing?
4. What are some practical applications of pattern matching in system administration?

## Next Class Preview

- Windows user and group management
- Windows security and permissions
- Remote access and administration tools
