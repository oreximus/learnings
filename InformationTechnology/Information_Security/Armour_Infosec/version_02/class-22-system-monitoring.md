# Class 22: System Monitoring and Performance Analysis

## Theory Section

### System Monitoring Concepts

#### Why Monitor Systems?

- **Performance Optimization**: Identify bottlenecks and resource constraints
- **Troubleshooting**: Diagnose system issues and failures
- **Capacity Planning**: Predict future resource needs
- **Security**: Detect unusual activity or intrusions
- **Compliance**: Meet regulatory and operational requirements

#### Key System Resources to Monitor

1. **CPU Usage**: Processor utilization and load
2. **Memory Usage**: RAM consumption and availability
3. **Disk I/O**: Storage read/write operations
4. **Network Activity**: Bandwidth usage and connections
5. **Process Activity**: Running processes and their resource usage

### Performance Metrics

#### CPU Metrics

- **CPU Utilization**: Percentage of CPU time used
- **Load Average**: Average system load over time periods
- **Context Switches**: Process switching frequency
- **Interrupts**: Hardware interrupt frequency

#### Memory Metrics

- **Total Memory**: Physical RAM installed
- **Used Memory**: Currently allocated memory
- **Free Memory**: Available memory
- **Cached Memory**: File system cache
- **Swap Usage**: Virtual memory usage

#### Disk Metrics

- **Disk Usage**: Storage space utilization
- **I/O Operations**: Read/write operations per second
- **I/O Wait**: Time spent waiting for disk operations
- **Disk Throughput**: Data transfer rates

#### Network Metrics

- **Bandwidth Usage**: Network traffic volume
- **Connection Count**: Active network connections
- **Packet Loss**: Network reliability indicator
- **Latency**: Network response times

## Practical Section

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

# Analyze system boot messages
dmesg | grep -i error
```

### Network Troubleshooting

#### Connectivity Testing

```bash
# Basic connectivity
ping -c 4 8.8.8.8          # Test internet connectivity
ping -c 4 gateway_ip       # Test gateway connectivity

# DNS resolution testing
nslookup google.com        # Test DNS resolution

# Route tracing
traceroute google.com      # Trace network path
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
lsof +D /path              # Files open in directory
```

### System Health Monitoring

#### Key Health Indicators

1. **System Load**: Should be below number of CPU cores
2. **Memory Usage**: Should not exceed 80-90% regularly
3. **Disk Space**: Should maintain 10-20% free space
4. **Disk I/O Wait**: Should be low (< 10%)
5. **Network Errors**: Should be minimal

#### Automated Monitoring

```bash
# Simple system health check
echo "=== System Health - $(date) ==="
echo "Load Average: $(cat /proc/loadavg | awk '{print $1, $2, $3}')"
echo "Memory Usage: $(free | grep Mem | awk '{printf "%.1f%%", $3/$2 * 100.0}')"
echo "Disk Usage: $(df / | tail -1 | awk '{print $5}')"
echo "Active Connections: $(netstat -tuln | grep LISTEN | wc -l)"
```

### Performance Optimization Tips

#### System Optimization

1. **Identify Bottlenecks**: Use monitoring tools to find resource constraints
2. **Optimize Processes**: Tune or replace resource-intensive applications
3. **Memory Management**: Ensure adequate RAM and optimize swap usage
4. **Disk Optimization**: Use appropriate file systems and storage configurations
5. **Network Tuning**: Optimize network settings for your workload

#### Monitoring Best Practices

1. **Establish Baselines**: Know normal system behavior
2. **Set Thresholds**: Define alert levels for key metrics
3. **Regular Reviews**: Analyze trends and patterns
4. **Document Changes**: Track system modifications and their impact
5. **Automate Monitoring**: Use scripts and tools for continuous monitoring

## Study Questions

1. What are the key system resources that should be monitored regularly?
2. How can you identify system bottlenecks using command-line tools?
3. What information can log files provide for system troubleshooting?
4. How do you establish performance baselines for a system?

## Next Class Preview

- Advanced text processing with grep
- Regular expressions and pattern matching
- File manipulation and text filtering
