# Class 22: Advanced Text Processing and DNS Management

## Theory Section - Advanced Command Operations

### Multiple Command Execution Methods

#### Sequential Execution (;)

```bash
ifconfig; date; ls
# Executes all commands in sequence regardless of success or failure
# Each command runs independently
```

#### Conditional AND Execution (&&)

```bash
ifconfig && date && id
# Executes next command only if previous command succeeds (exit code 0)
# Stops execution chain if any command fails
```

#### Conditional OR Execution (||)

```bash
ifconfig || date || id
# Executes next command only if previous command fails (non-zero exit code)
# Stops when first command succeeds
```

### Background Process Management

#### Running Commands in Background

```bash
ping 8.8.8.8 &
# Runs command in background, returns shell prompt immediately
# Process continues running independently
```

#### Background Process Control

```bash
jobs                    # List active background jobs
fg                      # Bring most recent background job to foreground
fg %n                   # Bring job number n to foreground
bg                      # Send stopped job to background
kill %n                 # Terminate job number n
```

#### Suppressing Output

```bash
ping 8.8.8.8 >/dev/null &
# Run in background without displaying output on terminal
# Redirects output to null device (discards it)
```

### Advanced Pipe Operations

#### Basic Pipe Concept

- **Purpose**: Connect output of one command to input of another
- **Symbol**: | (vertical bar)
- **Data Flow**: Command1 | Command2 | Command3

#### Pipe Examples

```bash
# Directory listing with pagination
ls -l /etc/ | less

# Sort directory contents by size
ls -l /etc/ | sort -k5 -n

# Search for specific content
cat /etc/passwd | grep root

# Count lines in output
ps aux | wc -l

# Complex processing chain
cat /etc/passwd | grep "root" | sort | uniq
```

#### Advanced Pipe Combinations

```bash
# Process monitoring with sorting
ps aux | sort -nrk 3 | head -10

# Log analysis
cat /var/log/syslog | grep -i error | tail -20

# Network connection analysis
netstat -tuln | grep LISTEN | sort -k4
```

## Theory Section - DNS Records and Management

### DNS Record Types Deep Dive

#### A Record (Address Record)

- **Purpose**: Maps domain name to IPv4 address
- **Format**: domain.com IN A 192.168.1.100
- **TTL**: Time to Live (cache duration)
- **Usage**: Primary website hosting, service endpoints

#### AAAA Record (IPv6 Address Record)

- **Purpose**: Maps domain name to IPv6 address
- **Format**: domain.com IN AAAA 2001:db8::1
- **Future-Proofing**: Essential for IPv6 adoption
- **Dual Stack**: Often used alongside A records

#### CNAME Record (Canonical Name Record)

- **Purpose**: Creates alias for another domain name
- **Usage**: Point multiple subdomains to single target
- **Restriction**: Cannot coexist with other record types for same name
- **Example**: blog.example.com CNAME www.example.com

#### MX Record (Mail Exchange Record)

- **Purpose**: Specifies mail servers for domain
- **Priority**: Lower numbers indicate higher priority
- **Format**: domain.com IN MX 10 mail.example.com
- **Redundancy**: Multiple MX records for failover

#### TXT Record (Text Record)

- **Purpose**: Store arbitrary text data for domain
- **Usage**: Domain verification, email authentication, security policies

##### Email Authentication in TXT Records

- **SPF (Sender Policy Framework)**:
  ```
  "v=spf1 ip4:192.168.1.100 include:_spf.google.com -all"
  ```
- **DMARC (Domain-based Message Authentication)**:
  ```
  "v=DMARC1; p=quarantine; rua=mailto:dmarc@example.com"
  ```
- **DKIM (DomainKeys Identified Mail)**:
  ```
  "v=DKIM1; k=rsa; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQ..."
  ```

#### NS Record (Name Server Record)

- **Purpose**: Specifies authoritative nameservers for domain
- **Delegation**: Points to servers that host DNS records
- **Example**: example.com IN NS ns1.example.com

#### SOA Record (Start of Authority Record)

- **Purpose**: Contains administrative information about DNS zone
- **Components**:
  - Primary nameserver
  - Administrator email address
  - Serial number (for zone transfers)
  - Refresh interval (secondary server check frequency)
  - Retry interval (retry failed zone transfer)
  - Expire time (secondary server data validity)
  - Minimum TTL (negative caching time)

#### PTR Record (Pointer Record)

- **Purpose**: Reverse DNS lookup (IP address to domain name)
- **Usage**: Email server verification, logging, security
- **Format**: 1.100.168.192.in-addr.arpa PTR www.example.com

### DNS Query Tools and Analysis

#### nslookup Command Examples

```bash
# Basic domain lookup
nslookup armourinfosec.com

# Specific record type queries
nslookup -type=A armourinfosec.com
nslookup -type=AAAA armourinfosec.com
nslookup -type=MX armourinfosec.com
nslookup -type=TXT armourinfosec.com
nslookup -type=SOA armourinfosec.com
nslookup -type=NS armourinfosec.com

# Query specific DNS server
nslookup armourinfosec.com 8.8.8.8
nslookup armourinfosec.com 64.6.64.6
```

#### DNS Cache Management

##### Windows DNS Cache

```cmd
# Display current DNS cache
ipconfig /displaydns

# Clear DNS cache
ipconfig /flushdns

# Register DNS records
ipconfig /registerdns
```

##### Linux DNS Cache

```bash
# Clear systemd-resolved cache
sudo systemd-resolve --flush-caches

# Clear nscd cache (if running)
sudo systemctl restart nscd

# Clear dnsmasq cache (if running)
sudo systemctl restart dnsmasq
```

## Practical Section

### Advanced Text Processing

#### Exit Code Checking

```bash
echo $?                 # Check exit code of last command
# 0 = success, non-zero = failure
```

#### Standard Data Streams

##### Standard Input (stdin) - File Descriptor 0

```bash
# Reading from stdin
cat                     # Read from keyboard input
cat < file.txt          # Read from file
echo "data" | command   # Pipe data to command
```

##### Standard Output (stdout) - File Descriptor 1

```bash
# Redirecting stdout
ls > file.txt           # Redirect output to file
ls >> file.txt          # Append output to file
ls | less               # Pipe output to another command
```

##### Standard Error (stderr) - File Descriptor 2

```bash
# Redirecting stderr
ls nonexistent 2>error.txt              # Redirect errors to file
command 2>/dev/null                     # Discard error messages
command >output.txt 2>error.txt         # Separate output and errors
command &>combined.txt                  # Combine output and errors
command >output.txt 2>&1                # Redirect errors to same file as output
```

#### Practical Redirection Examples

```bash
# Separate normal output and errors
cat /etc/passwd /etc/shadow 1>output.txt 2>error.txt

# Combine both streams
cat /etc/passwd /etc/shadow &>combined.txt

# Alternative syntax for combining
cat /etc/passwd /etc/shadow >combined.txt 2>&1
```

### DNS Server Types and Configuration

#### Types of DNS Servers

##### 1. Root Domain Servers

- **Function**: Provide TLD nameserver information
- **Quantity**: 13 servers worldwide (A-M)
- **Management**: Various organizations

##### 2. TLD Nameservers

- **Function**: Manage domains within specific TLD
- **Examples**: .com servers, .org servers
- **Content**: NS records for authoritative servers

##### 3. Authoritative Nameservers

- **Function**: Hold actual DNS records for domains
- **Content**: A, AAAA, CNAME, MX, TXT records
- **Authority**: Final source of domain information

##### 4. Recursive (Caching) DNS Servers

- **Function**: Perform complete DNS resolution
- **Examples**: ISP DNS, Google (8.8.8.8), Cloudflare (1.1.1.1)
- **Caching**: Store results for performance

##### 5. Forwarding DNS Servers

- **Function**: Forward queries to other DNS servers
- **Usage**: Corporate networks, filtered DNS
- **Configuration**: Specify upstream servers

### Practical DNS Examples

#### DNS Record Analysis

```bash
# Comprehensive DNS analysis script
#!/bin/bash

domain="armourinfosec.com"

echo "=== DNS Analysis for $domain ==="
echo

echo "A Records:"
nslookup -type=A $domain | grep "Address:" | grep -v "#"

echo
echo "AAAA Records:"
nslookup -type=AAAA $domain | grep "Address:" | grep -v "#"

echo
echo "MX Records:"
nslookup -type=MX $domain | grep "mail exchanger"

echo
echo "TXT Records:"
nslookup -type=TXT $domain | grep "text ="

echo
echo "NS Records:"
nslookup -type=NS $domain | grep "nameserver"

echo
echo "SOA Record:"
nslookup -type=SOA $domain | grep -A 10 "origin"
```

#### DNS Troubleshooting

```bash
# DNS connectivity test
#!/bin/bash

dns_servers=("8.8.8.8" "1.1.1.1" "9.9.9.9")
test_domain="google.com"

for server in "${dns_servers[@]}"; do
    echo "Testing DNS server: $server"
    result=$(nslookup $test_domain $server 2>/dev/null | grep "Address:" | tail -1)
    if [ $? -eq 0 ]; then
        echo "  Success: $result"
    else
        echo "  Failed to resolve"
    fi
    echo
done
```

### Advanced Command Examples

#### System Monitoring with Pipes

```bash
# Top CPU consuming processes
ps aux | sort -nrk 3 | head -10

# Top memory consuming processes
ps aux | sort -nrk 4 | head -10

# Network connections summary
netstat -tuln | grep LISTEN | awk '{print $4}' | sort | uniq -c

# Disk usage analysis
du -h /var/log/* 2>/dev/null | sort -hr | head -10
```

#### Log Analysis Examples

```bash
# Error analysis in system logs
grep -i error /var/log/syslog | tail -20

# Failed login attempts
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c

# Web server access analysis (if Apache/Nginx logs available)
cat /var/log/apache2/access.log | awk '{print $1}' | sort | uniq -c | sort -nr | head -10
```

### Practical Exercises

#### Exercise 1: Command Chaining Practice

```bash
# Create a system health check script
#!/bin/bash

echo "System Health Check - $(date)"
echo "================================"

# Check if services are running
systemctl is-active ssh >/dev/null 2>&1 && echo "SSH: Running" || echo "SSH: Not running"
systemctl is-active networking >/dev/null 2>&1 && echo "Network: Running" || echo "Network: Not running"

# Check disk space
echo
echo "Disk Usage:"
df -h | grep -E "/$|/home|/var" | awk '{print $6 ": " $5 " used"}'

# Check memory
echo
echo "Memory Usage:"
free -h | grep Mem | awk '{print "Memory: " $3 "/" $2 " (" int($3/$2*100) "%)"}'

# Check load average
echo
echo "System Load:"
uptime | awk -F'load average:' '{print "Load Average:" $2}'
```

#### Exercise 2: DNS Analysis Tool

```bash
#!/bin/bash
# Comprehensive DNS analysis tool

if [ $# -eq 0 ]; then
    echo "Usage: $0 <domain>"
    exit 1
fi

domain=$1

echo "DNS Analysis for: $domain"
echo "========================="

# Test multiple DNS servers
dns_servers=("8.8.8.8" "1.1.1.1" "208.67.222.222")

for server in "${dns_servers[@]}"; do
    echo
    echo "Testing with DNS server: $server"
    echo "--------------------------------"

    # A record
    a_record=$(nslookup -type=A $domain $server 2>/dev/null | grep "Address:" | grep -v "#" | head -1 | awk '{print $2}')
    echo "A Record: ${a_record:-Not found}"

    # MX record
    mx_record=$(nslookup -type=MX $domain $server 2>/dev/null | grep "mail exchanger" | head -1)
    echo "MX Record: ${mx_record:-Not found}"
done
```

## Study Questions

1. How do different command chaining operators affect script execution flow?
2. What are the practical applications of standard stream redirection?
3. How do different types of DNS servers work together in the resolution process?
4. What information can be gathered from different DNS record types?

## Next Class Preview

- Advanced system monitoring and process management
- Network troubleshooting tools and techniques
- Log file analysis and system diagnostics
- Performance monitoring and optimization
