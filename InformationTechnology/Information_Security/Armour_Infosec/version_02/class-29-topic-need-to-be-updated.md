# Class 01: Advanced Text Manipulation with sed

## Introduction to sed
The `sed` (Stream Editor) command is a powerful Unix utility for parsing and transforming text. It's commonly used for:
- Text substitution
- Selective line printing
- File editing
- Text analysis

## Basic Syntax
```bash
sed [options] 'command' input_file
```

## Common Operations with Real-world Examples

### 1. Viewing and Printing Content

#### Print Specific Lines
```bash
# Print lines 5-10 of a config file
sed -n '5,10p' /etc/nginx/nginx.conf

# Print first 5 lines
sed -n '1,5p' log.txt
```

#### Print Lines Matching Pattern
```bash
# Print lines containing IP addresses
sed -n '/\b[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\.[0-9]\{1,3\}\b/p' access.log

# Print lines with error messages
sed -n '/ERROR/p' application.log
```

### 2. Adding Content

#### Append After Match
```bash
# Add a warning comment after configuration lines
sed '/^config/a # WARNING: Do not modify without approval' settings.conf

# Add new DNS entry after nameserver line
sed '/nameserver/a nameserver 8.8.8.8' /etc/resolv.conf
```

#### Insert Before Match
```bash
# Add header before each section
sed '/^Section/i \# Important Section Below' document.txt

# Add prerequisite before installation step
sed '/^Installation:/i \# Ensure system is up to date first' readme.md
```

### 3. Deleting Content

#### Delete Lines by Pattern
```bash
# Remove comment lines
sed '/^#/d' config.ini

# Remove empty lines
sed '/^$/d' script.sh

# Remove lines with debugging information
sed '/DEBUG:/d' application.log
```

#### Delete Lines by Line Number
```bash
# Remove first 5 lines
sed '1,5d' file.txt

# Remove header (first line)
sed '1d' data.csv
```

### 4. Text Substitution

#### Basic Substitution
```bash
# Replace old version with new version
sed 's/version 2.0/version 2.1/' changelog.md

# Update IP address
sed 's/192.168.1.100/192.168.1.200/' config.conf
```

#### Global Substitution
```bash
# Replace all occurrences of 'error' with 'ERROR'
sed 's/error/ERROR/g' log.txt

# Update all URLs from HTTP to HTTPS
sed 's/http:/https:/g' links.txt
```

### 5. Advanced Pattern Matching

#### Multiple Pattern Operations
```bash
# Replace multiple words
sed -e 's/cat/dog/g' -e 's/rat/mouse/g' story.txt

# Complex transformations
sed -e 's/old/new/g' -e '/^#/d' -e '/^$/d' file.txt
```

#### Using Regular Expressions
```bash
# Match email addresses
sed -n '/[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}/p' contacts.txt

# Match and replace phone numbers
sed 's/[0-9]\{3\}-[0-9]\{3\}-[0-9]\{4\}/PHONE-NUMBER/g' data.txt
```

### 6. Working with Files

#### In-place Editing with Backup
```bash
# Make changes and create backup
sed -i.bak 's/old/new/g' config.conf

# Multiple changes with backup
sed -i.bak -e 's/foo/bar/g' -e 's/baz/qux/g' file.txt
```

#### Using sed with Multiple Files
```bash
# Apply same changes to multiple files
sed -i 's/error/ERROR/g' *.log

# Process multiple files with different patterns
sed -i -e 's/warning/WARNING/g' -e 's/error/ERROR/g' *.log
```

## Real-world Scenarios

### 1. Log File Processing
```bash
# Extract error messages and their timestamps
sed -n '/ERROR/p' application.log | sed 's/^\([0-9-]\{10\} [0-9:]\{8\}\).*ERROR: \(.*\)$/\1 - \2/'

# Remove sensitive information from logs
sed 's/password=[^[:space:]]*/password=****/g' access.log
```

### 2. Configuration File Management
```bash
# Update server settings
sed -i.bak -e 's/max_connections = 100/max_connections = 200/' \
    -e 's/timeout = 30/timeout = 60/' \
    server.conf

# Comment out deprecated settings
sed -i '/deprecated_setting/s/^/#/' config.ini
```

### 3. Batch File Processing
```bash
# Update copyright year in all files
sed -i 's/Copyright 2023/Copyright 2024/' *.txt

# Fix formatting in multiple files
sed -i 's/  */ /g' *.md
```

### 4. Data Cleaning
```bash
# Clean CSV data
sed -e 's/^[[:space:]]*//g' \  # Remove leading spaces
    -e 's/[[:space:]]*$//g' \  # Remove trailing spaces
    -e 's/,,/,NA,/g' \        # Replace empty fields
    -e '/^$/d' \              # Remove empty lines
    data.csv
```

## Best Practices

1. **Always Backup**
   ```bash
   # Create backup before making changes
   sed -i.bak 's/old/new/g' file.txt
   ```

2. **Test Commands First**
   ```bash
   # Test without -i flag first
   sed 's/pattern/replacement/' file.txt | head
   ```

3. **Use Extended Regular Expressions**
   ```bash
   # More readable regex with -E flag
   sed -E 's/[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+/IP-ADDRESS/g' file.txt
   ```

4. **Document Complex Commands**
   ```bash
   # Add comments for complex operations
   sed -i.bak \
       -e 's/foo/bar/g'    # Replace all foo with bar \
       -e '/^#/d'          # Remove comments \
       -e '/^$/d'          # Remove empty lines \
       file.txt
   ```

## Common Pitfalls and Solutions

1. **Escaping Special Characters**
   ```bash
   # Correct way to escape forward slashes
   sed 's/http:\/\//https:\/\//g' urls.txt
   ```

2. **Handling Multiple Lines**
   ```bash
   # Use N command for multi-line operations
   sed 'N;s/\n/ /' file.txt
   ```

3. **Case Sensitivity**
   ```bash
   # Case-insensitive substitution
   sed 's/pattern/replacement/gI' file.txt
   ```

## Practice Exercises

1. **Log Analysis**
   ```bash
   # Extract and format error messages
   sed -n '/ERROR/p' log.txt | sed 's/.*ERROR: \(.*\)/\1/'
   ```

2. **Configuration Update**
   ```bash
   # Update multiple settings
   sed -i.bak \
       -e 's/debug=true/debug=false/' \
       -e 's/port=8080/port=9090/' \
       config.properties
   ```

3. **Data Cleaning**
   ```bash
   # Clean and format data
   sed -e 's/^[[:space:]]*//g' \
       -e 's/[[:space:]]*$//g' \
       -e '/^$/d' \
       input.txt
   ```

# Class 02: Active Directory Domain Services:

> SAM file: (Security Account Managment): every local user on your windows os
is managed from this file.

> When we use the Active Directory Domain Services, then we'll get shifted to 
the NTDS.


- Key Features of AD DS:
    - AD stores information about
        - Users
        - Computers
        - Group
        - Resources (Printers, files, etc.)
    - Centralized structure manage users and resources in the network.
    - Heirarchical structure:
        - Forest
        - Domain
        - OU
        - 

- Core Components of AD DS:
    1. Logical Components
        a. Domains
        b. Organizational Units
        c. Trees
        d. Forests

    2. Physical Components:
        a. Domain Controllers
        b. Global Catalog (GC)
        c. Read-only Domain Controller (RODC)

    3. Data Store:
        - The SAM is a Windows Subsystem that manages local user accounts and
        their credentials.
        - These credentials are stored hashed(usually NTLM format)

- NTDS.dit (Database file) file
    - Data this file contains:

- SYSVOL file: contains group policies related information.

> The SAM and SYSTEM file are useful for enumeration purposes we can extract
passwords from this file.

#### AD DS Configuration:

##### DNS

- the zone properties option where we have the DNS update setting set to
the secure only, will enable the Joined Domain, Domain users can only update
the information here

> Remove the FQDN that's setup on your client otherwise domain joining is 
problem.

> Domain joining can be done via anyone and only admin can remove the joined
domain users.

> To ensure that your server works, try nslookup, pinging server IP and ping
server domain.
