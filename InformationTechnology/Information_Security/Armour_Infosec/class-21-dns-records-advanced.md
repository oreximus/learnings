# Class 21: DNS Records and Advanced Concepts

## DNS Records Deep Dive

### DNS Record Storage

- **Location**: Stored in authoritative nameservers
- **Management**: Controlled by domain owners
- **Propagation**: Changes spread across global DNS infrastructure
- **TTL**: Time To Live determines cache duration

## Essential DNS Record Types

### 1. A Record (Address Record)

- **Purpose**: Maps domain name to IPv4 address
- **Format**: `domain.com. 3600 IN A 93.184.216.34`
- **Usage**: Primary record for website hosting
- **Example**: `www.example.com → 192.168.1.100`

### 2. AAAA Record (IPv6 Address)

- **Purpose**: Maps domain name to IPv6 address
- **Format**: `domain.com. 3600 IN AAAA 2001:db8::1`
- **Usage**: IPv6 website hosting
- **Example**: `www.example.com → 2001:db8:85a3::8a2e:370:7334`

### 3. CNAME Record (Canonical Name)

- **Purpose**: Creates alias for another domain name
- **Usage**: Point multiple subdomains to single domain
- **Restriction**: Cannot coexist with other record types for same name
- **Example**: `blog.example.com CNAME myblog.hosting.com`

### 4. MX Record (Mail Exchange)

- **Purpose**: Specifies mail server for domain
- **Priority**: Lower numbers indicate higher priority
- **Format**: `example.com. 3600 IN MX 10 mail.example.com.`
- **Usage**: Email routing and delivery

#### MX Record Priority Examples

```
example.com. IN MX 10 mail1.example.com.
example.com. IN MX 20 mail2.example.com.
example.com. IN MX 30 mail3.example.com.
```

### 5. TXT Record (Text Record)

- **Purpose**: Store arbitrary text data
- **Usage**: Domain verification, email security, general information
- **Multiple Values**: Single domain can have multiple TXT records

#### Common TXT Record Uses

##### SPF (Sender Policy Framework)

```
"v=spf1 ip4:192.168.1.100 include:_spf.google.com ~all"
```

- **Purpose**: Prevent email spoofing
- **Function**: Specify authorized mail servers

##### DMARC (Domain-based Message Authentication)

```
"v=DMARC1; p=quarantine; rua=mailto:dmarc@example.com"
```

- **Purpose**: Email authentication and reporting
- **Function**: Policy for handling failed authentication

##### DKIM (DomainKeys Identified Mail)

```
"v=DKIM1; k=rsa; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQ..."
```

- **Purpose**: Digital signature for emails
- **Function**: Verify email authenticity

### 6. NS Record (Name Server)

- **Purpose**: Specifies authoritative nameservers for domain
- **Format**: `example.com. 3600 IN NS ns1.example.com.`
- **Requirement**: Every domain must have at least two NS records
- **Example**:

```
example.com. IN NS ns1.hosting.com.
example.com. IN NS ns2.hosting.com.
```

### 7. SOA Record (Start of Authority)

- **Purpose**: Contains administrative information about domain
- **Unique**: Only one SOA record per zone
- **Components**: Primary nameserver, admin email, serial number, timers

#### SOA Record Format

```
example.com. IN SOA ns1.example.com. admin.example.com. (
    2024061100 ; Serial number
    28800      ; Refresh (8 hours)
    7200       ; Retry (2 hours)
    604800     ; Expire (7 days)
    600        ; Minimum TTL (10 minutes)
)
```

### 8. PTR Record (Pointer Record)

- **Purpose**: Reverse DNS lookup (IP address to domain name)
- **Location**: Stored in reverse DNS zones
- **Format**: `34.216.184.93.in-addr.arpa. IN PTR example.com.`
- **Usage**: Email server verification, security

### 9. SRV Record (Service Record)

- **Purpose**: Specify location of services
- **Format**: `_service._protocol.domain. IN SRV priority weight port target`
- **Example**: `_sip._tcp.example.com. IN SRV 10 60 5060 sip.example.com.`

### 10. CAA Record (Certificate Authority Authorization)

- **Purpose**: Specify which Certificate Authorities can issue SSL certificates
- **Format**: `example.com. IN CAA 0 issue "letsencrypt.org"`
- **Security**: Prevent unauthorized certificate issuance

## DNS Record Example Analysis

### Sample DNS Record Set

```
example.com.        3600    IN  SOA     ns1.example.com. admin.example.com. 2024061100 28800 7200 604800 600
example.com.        3600    IN  NS      ns1.example.com.
example.com.        3600    IN  NS      ns2.example.com.
example.com.        3600    IN  A       93.184.216.34
example.com.        3600    IN  AAAA    2606:2800:220:1:248:1893:25c8:1946
example.com.        3600    IN  MX      10 mail.example.com.
www.example.com.    3600    IN  CNAME   example.com.
mail.example.com.   3600    IN  A       93.184.216.35
blog.example.com.   3600    IN  CNAME   hosting.provider.com.
```

## DNS Lookup Tools and Commands

### nslookup Command Examples

#### Basic Domain Lookup

```bash
nslookup armourinfosec.com
# Returns: A and AAAA records
```

#### Specific Record Type Queries

```bash
# A records only
nslookup -type=A armourinfosec.com

# AAAA records (IPv6)
nslookup -type=AAAA armourinfosec.com

# MX records (mail servers)
nslookup -type=MX armourinfosec.com

# TXT records
nslookup -type=TXT armourinfosec.com

# SOA record
nslookup -type=SOA armourinfosec.com

# All records
nslookup -type=ANY armourinfosec.com
```

#### Using Specific DNS Server

```bash
# Query using specific DNS server
nslookup armourinfosec.com 8.8.8.8
nslookup armourinfosec.com 1.1.1.1
```

### DNS Cache Management

#### Windows DNS Cache

```cmd
# Display DNS cache
ipconfig /displaydns

# Clear DNS cache
ipconfig /flushdns
```

#### Linux DNS Cache

```bash
# Clear systemd-resolved cache
sudo systemd-resolve --flush-caches

# Clear nscd cache
sudo service nscd restart
```

## DNS Troubleshooting

### Common DNS Issues

1. **Propagation Delays**: Changes take time to spread globally
2. **TTL Issues**: Old records cached due to high TTL values
3. **Misconfigured Records**: Incorrect IP addresses or syntax
4. **Missing Records**: Required records not configured

### DNS Testing Tools

- **dig**: Advanced DNS lookup tool (Linux/Mac)
- **nslookup**: Basic DNS lookup (cross-platform)
- **host**: Simple DNS lookup (Linux/Mac)
- **Online Tools**: DNS propagation checkers, DNS health checkers

### Best Practices

1. **Use appropriate TTL values**: Balance between performance and flexibility
2. **Monitor DNS changes**: Verify propagation after changes
3. **Implement redundancy**: Multiple nameservers and MX records
4. **Regular testing**: Periodic DNS health checks
5. **Security**: Implement DNSSEC where possible
