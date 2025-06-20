# Class 23: System Monitoring and Advanced Troubleshooting

## Theory Section - Standard Data Streams

### Understanding Standard Streams

#### Standard Input (stdin) - File Descriptor 0

- **Purpose**: Default input source for commands
- **Default Source**: Keyboard input
- **Redirection**: Can be redirected from files or other commands

```bash
# Examples of stdin usage
cat                         # Read from keyboard
cat < file.txt             # Read from file
echo "data" | command      # Pipe data as input
command <<EOF              # Here document
input data
EOF
```

#### Standard Output (stdout) - File Descriptor 1

- **Purpose**: Default output destination for command results
- **Default Destination**: Terminal screen
- **Redirection**: Can be redirected to files or other commands

```bash
# Examples of stdout redirection
ls > file.txt              # Redirect to file (overwrite)
ls >> file.txt             # Redirect to file (append)
ls | less                  # Pipe to another command
```

#### Standard Error (stderr) - File Descriptor 2

- **Purpose**: Default output for error messages
- **Default Destination**: Terminal screen (same as stdout)
- **Separation**: Allows separate handling of errors and normal output

```bash
# Examples of stderr redirection
ls nonexistent 2>error.txt              # Redirect errors only
command 2>/dev/null                     # Discard error messages
command >output.txt 2>error.txt         # Separate output and errors
command &>combined.txt                  # Combine output and errors
command >output.txt 2>&1                # Redirect errors to same destination as output
```

### Advanced Redirection Examples

#### Practical Redirection Scenarios

```bash
# Accessing protected files as normal user
cat /etc/passwd /etc/shadow 1>output.txt 2>error.txt
# passwd content goes to output.txt, shadow access error goes to error.txt

# Combining streams
cat /etc/passwd /etc/shadow &>both.txt
# Both output and errors go to same file

# Alternative syntax for combining
cat /etc/passwd /etc/shadow >both.txt 2>&1
# Redirect stdout to file, then redirect stderr to same destination as stdout
```

#### Exit Code Checking

```bash
echo $?                    # Check exit code of last command
# 0 = success, non-zero = failure/error
```

## Theory Section - DNS Server Architecture

### DNS Server Hierarchy

#### 1. Root Domain Servers

- **Quantity**: 13 root servers worldwide (A through M)
- **Function**: Provide information about TLD nameservers
- **Content**: Names and IP addresses of TLD nameservers
- **Management**: Various organizations (Verisign, NASA, etc.)
- **Redundancy**: Multiple physical servers per letter identifier

#### 2. TLD (Top-Level Domain) Nameservers

- **Function**: Manage domain records for specific TLD (.com, .org, etc.)
- **Storage**: Delegation information for domains within their TLD
- **Content**: NS records pointing to authoritative nameservers
- **Examples**: Verisign for .com, PIR for .org

#### 3. Authoritative Nameservers

- **Function**: Hold actual DNS records for specific domains
- **Content**: A, AAAA, CNAME, MX, TXT, and other DNS records
- **Authority**: Final source of truth for domain information
- **Management**: Controlled by domain owners or DNS hosting providers

#### 4. Recursive (Caching) DNS Servers

- **Function**: Perform complete DNS resolution on behalf of clients
- **Process**: Query root → TLD → authoritative servers
- **Caching**: Store results to improve performance and reduce load
- **Examples**: ISP DNS servers, Google (8.8.8.8), Cloudflare (1.1.1.1)

#### 5. Forwarding DNS Servers

- **Function**: Forward DNS queries to other specified DNS servers
- **Configuration**: Configured with upstream DNS servers
- **Usage**: Corporate networks, content filtering, policy enforcement
- **Benefits**: Centralized control, caching, monitoring

### Complete DNS Resolution Process

#### Step-by-Step Query Resolution

1. **Browser Cache Check**: Local browser DNS cache
2. **Operating System Cache**: System-level DNS cache
3. **Hosts File Check**: Local hosts file lookup
4. **Recursive DNS Server**: Query configured DNS server
5. **Root Server Query**: If not cached, query root servers
6. **TLD Server Query**: Query appropriate TLD servers
7. **Authoritative Server Query**: Query domain's authoritative servers
8. **Response Chain**: Answer travels back through the chain
9. **Caching**: Results cached at multiple levels
10. **Browser Connection**: Finally connect to resolved IP address

## Practical Section - System Monitoring

### Process Management and Monitoring

#### Process Information Commands

```bash
ps aux                     # Show all running processes
ps aux | grep process_name # Find specific process
top                        # Real-time process monitor
htop                       # Enhanced process monitor (if installed)
pstree                     # Show process tree
```

#### Process Sorting and Analysis

```bash
# Sort processes by CPU usage
ps aux | sort -nrk 3 | head -10

# Sort processes by memory usage
ps aux | sort -nrk 4 | head -10

# Find processes using most resources
ps aux | awk '{print $2, $3, $4, $11}' | sort -nrk 2 | head -10
```

### System Resource Monitoring

#### Memory Analysis

```bash
free -h                    # Human-readable memory usage
cat /proc/meminfo          # Detailed memory information
vmstat                     # Virtual memory statistics
vmstat 1 5                 # Update every second, 5 times
```

#### Disk Usage Analysis

```bash
df -h                      # Filesystem disk usage
du -h /path                # Directory disk usage
du -sh /var/log/*          # Size of each log directory
lsof                       # List open files
lsof /path/to/file         # Show processes using specific file
```

#### Network Monitoring

```bash
netstat -tuln              # Show listening ports
netstat -i                 # Network interface statistics
ss -tuln                   # Modern replacement for netstat
iftop                      # Real-time network usage (if installed)
```

### Log File Analysis

#### System Log Analysis

```bash
# View recent system messages
tail -f /var/log/syslog    # Follow log in real-time
tail -100 /var/log/syslog  # Last 100 lines

# Search for errors
grep -i error /var/log/syslog | tail -20
grep -i "failed\|error\|critical" /var/log/syslog

# Analyze authentication logs
grep "Failed password" /var/log/auth.log
grep "Accepted password" /var/log/auth.log
```

#### Log Analysis with Pipes

```bash
# Count error types
grep -i error /var/log/syslog | awk '{print $5}' | sort | uniq -c

# Find most active IP addresses in auth log
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -nr

# Analyze web server logs (if available)
cat /var/log/apache2/access.log | awk '{print $1}' | sort | uniq -c | sort -nr | head -10
```

## Practical Section - Advanced Troubleshooting

### Network Troubleshooting

#### Connectivity Testing

```bash
# Basic connectivity
ping -c 4 8.8.8.8          # Test internet connectivity
ping -c 4 gateway_ip       # Test gateway connectivity

# DNS resolution testing
nslookup google.com        # Test DNS resolution
dig google.com             # Alternative DNS testing

# Route tracing
traceroute google.com      # Trace network path
mtr google.com             # Continuous trace (if installed)
```

#### Port and Service Testing

```bash
# Test specific ports
telnet hostname 80         # Test HTTP port
nc -zv hostname 22         # Test SSH port with netcat

# Check listening services
netstat -tuln | grep :80   # Check if web server is listening
ss -tuln | grep :22        # Check if SSH is listening
```

### System Performance Analysis

#### CPU and Load Monitoring

```bash
uptime                     # System uptime and load average
w                          # Users and system load
cat /proc/loadavg          # Load average details

# CPU usage analysis
iostat                     # I/O and CPU statistics
sar -u 1 5                # CPU usage every second, 5 times
```

#### Disk I/O Analysis

```bash
iostat -x 1 5              # Extended I/O statistics
iotop                      # Real-time I/O usage by process (if installed)
lsof +D /path              # Files open in directory
```

### Comprehensive System Health Check

#### System Health Script

```bash
#!/bin/bash
# Comprehensive system health check

echo "=== System Health Report - $(date) ==="
echo

# System information
echo "=== System Information ==="
echo "Hostname: $(hostname)"
echo "Uptime: $(uptime -p)"
echo "Load Average: $(cat /proc/loadavg | awk '{print $1, $2, $3}')"
echo

# Memory usage
echo "=== Memory Usage ==="
free -h | grep -E "Mem|Swap"
echo

# Disk usage
echo "=== Disk Usage ==="
df -h | grep -E "/$|/home|/var|/tmp"
echo

# Top processes by CPU
echo "=== Top CPU Processes ==="
ps aux | sort -nrk 3 | head -5 | awk '{print $2, $3"%", $11}'
echo

# Top processes by Memory
echo "=== Top Memory Processes ==="
ps aux | sort -nrk 4 | head -5 | awk '{print $2, $4"%", $11}'
echo

# Network connections
echo "=== Network Listening Ports ==="
netstat -tuln | grep LISTEN | awk '{print $4}' | sort | uniq
echo

# Recent errors
echo "=== Recent System Errors ==="
grep -i error /var/log/syslog | tail -5 | cut -d' ' -f1-3,5-
```

### DNS Troubleshooting Tools

#### Comprehensive DNS Testing

```bash
#!/bin/bash
# DNS troubleshooting script

domain=${1:-"google.com"}
dns_servers=("8.8.8.8" "1.1.1.1" "208.67.222.222" "9.9.9.9")

echo "DNS Troubleshooting for: $domain"
echo "================================="

# Test each DNS server
for server in "${dns_servers[@]}"; do
    echo
    echo "Testing DNS Server: $server"
    echo "----------------------------"

    # Test A record
    a_result=$(nslookup -type=A $domain $server 2>/dev/null | grep "Address:" | grep -v "#" | head -1)
    echo "A Record: ${a_result:-Failed}"

    # Test response time
    start_time=$(date +%s%N)
    nslookup $domain $server >/dev/null 2>&1
    end_time=$(date +%s%N)
    response_time=$(( (end_time - start_time) / 1000000 ))
    echo "Response Time: ${response_time}ms"
done

# Test local DNS resolution
echo
echo "Local DNS Resolution:"
echo "--------------------"
local_result=$(nslookup $domain 2>/dev/null | grep "Address:" | grep -v "#" | head -1)
echo "Result: ${local_result:-Failed}"
```

### Performance Monitoring Script

#### Resource Monitoring Tool

```bash
#!/bin/bash
# Continuous system monitoring

interval=${1:-5}
count=${2:-12}

echo "System Performance Monitor (${interval}s intervals, ${count} samples)"
echo "======================================================================"

for i in $(seq 1 $count); do
    echo
    echo "Sample $i - $(date)"
    echo "-------------------"

    # CPU usage
    cpu_usage=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}' | cut -d'%' -f1)
    echo "CPU Usage: ${cpu_usage}%"

    # Memory usage
    mem_usage=$(free | grep Mem | awk '{printf "%.1f", $3/$2 * 100.0}')
    echo "Memory Usage: ${mem_usage}%"

    # Load average
    load_avg=$(cat /proc/loadavg | awk '{print $1}')
    echo "Load Average: $load_avg"

    # Disk usage for root
    disk_usage=$(df / | tail -1 | awk '{print $5}')
    echo "Disk Usage (/): $disk_usage"

    sleep $interval
done
```

## Study Questions

1. How do standard streams enable flexible command-line data processing?
2. What role does each type of DNS server play in the resolution process?
3. How can system monitoring help prevent performance issues?
4. What are the key indicators of system health to monitor regularly?

## Next Class Preview

- Advanced shell scripting and automation
- Security monitoring and log analysis
- Network security fundamentals
- System hardening and best practices
