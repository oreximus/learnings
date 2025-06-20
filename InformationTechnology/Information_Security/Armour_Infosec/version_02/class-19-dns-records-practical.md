# Class 19: DNS Records and Practical Implementation

## Theory Section

### Complete Domain Name System Structure

#### Domain Name Anatomy

```
subdomain.second-level.top-level.root
    │         │           │      │
    │         │           │      └── Root (invisible .)
    │         │           └───────── TLD
    │         └───────────────────── SLD
    └─────────────────────────────── Subdomain/Hostname
```

#### Reading Direction

Domain names are read **right to left** in terms of hierarchy:

- Rightmost = Highest level in DNS hierarchy
- Leftmost = Lowest level in DNS hierarchy

### Top-Level Domains (TLD) Categories

#### 1. Generic Top-Level Domains (gTLD)

##### Unsponsored gTLDs (Open Registration)

- **.com** - Commercial (most popular)
- **.net** - Network infrastructure
- **.org** - Organizations
- **.info** - Information sites
- **.biz** - Business

##### Restricted gTLDs

- **.gov** - US Government only
- **.edu** - Educational institutions
- **.mil** - US Military
- **.int** - International organizations

#### 2. Sponsored Top-Level Domains (sTLD)

- **.aero** - Aviation industry
- **.museum** - Museums
- **.travel** - Travel industry
- **.coop** - Cooperatives

#### 3. Country Code Top-Level Domains (ccTLD)

- **.us** - United States
- **.uk** - United Kingdom
- **.in** - India
- **.de** - Germany
- **.jp** - Japan

#### 4. New gTLD Program (Since 2012)

- **.google** - Google Inc.
- **.apple** - Apple Inc.
- **.blog** - Blogging
- **.tech** - Technology

### Second-Level Domains (SLD)

- **Definition**: Part directly to the left of TLD
- **Examples**:
  - **google**.com - "google" is SLD
  - **wikipedia**.org - "wikipedia" is SLD
- **Registration**: Must be unique within TLD
- **Limitations**: 63 characters max, letters/numbers/hyphens

### Subdomains

- **Definition**: Additional levels under SLD
- **Examples**:
  - **www**.example.com - Web service
  - **mail**.google.com - Email service
  - **api**.service.com - API endpoint
- **Control**: Managed by domain owner
- **Unlimited**: Can create unlimited subdomains

## DNS Records Detailed Analysis

### A Record (Address Record)

- **Purpose**: Maps domain to IPv4 address
- **Format**: domain.com IN A 192.168.1.100
- **TTL**: Cache duration (e.g., 3600 seconds)
- **Usage**: Primary website hosting

### AAAA Record (IPv6 Address)

- **Purpose**: Maps domain to IPv6 address
- **Format**: domain.com IN AAAA 2001:db8::1
- **Future**: IPv6 adoption increasing
- **Dual Stack**: Often used with A records

### CNAME Record (Canonical Name)

- **Purpose**: Creates alias for another domain
- **Usage**: Point multiple subdomains to single target
- **Restriction**: Cannot coexist with other records
- **Example**: blog.example.com CNAME myblog.example.com

### MX Record (Mail Exchange)

- **Purpose**: Specifies mail servers for domain
- **Priority**: Lower number = higher priority
- **Format**: domain.com IN MX 10 mail.example.com
- **Multiple**: Can have multiple MX records for redundancy

### TXT Record (Text Record)

- **Purpose**: Store arbitrary text data
- **Usage**: Domain verification, email authentication

#### Email Authentication Records

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
  "v=DKIM1; k=rsa; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC..."
  ```

### NS Record (Name Server)

- **Purpose**: Specifies authoritative nameservers
- **Delegation**: Points to servers hosting DNS records
- **Example**: example.com IN NS ns1.example.com

### SOA Record (Start of Authority)

- **Purpose**: Administrative information about zone
- **Components**:
  - Primary nameserver
  - Admin email address
  - Serial number (for zone transfers)
  - Refresh interval
  - Retry interval
  - Expire time
  - Minimum TTL

### PTR Record (Pointer Record)

- **Purpose**: Reverse DNS lookup (IP to domain)
- **Usage**: Email server verification, logging
- **Format**: 1.100.168.192.in-addr.arpa PTR www.example.com

## Practical Section

### DNS Query Examples

#### Basic nslookup Queries

```bash
# Basic domain lookup
nslookup armourinfosec.com

# Output example:
Server:  dns.google
Address:  8.8.8.8

Non-authoritative answer:
Name:    armourinfosec.com
Addresses:  185.199.108.153
          185.199.111.153
          185.199.109.153
          185.199.110.153
```

#### Specific Record Type Queries

```bash
# A Record query
nslookup -type=A armourinfosec.com

# AAAA Record query
nslookup -type=AAAA armourinfosec.com

# MX Record query
nslookup -type=MX armourinfosec.com
# Output: armourinfosec.com MX preference = 10, mail exchanger = mail.armourinfosec.io

# TXT Record query
nslookup -type=TXT armourinfosec.com
# Output: "v=spf1 ip4:155.133.27.166 ip6:2a02:c206:2112:8075::1 -all"

# SOA Record query
nslookup -type=SOA armourinfosec.com
# Output shows primary nameserver, admin email, serial number, timers
```

#### Querying Specific DNS Servers

```bash
# Query specific DNS server
nslookup armourinfosec.com 64.6.64.6

# Output shows different server:
Server:  rec1pubns1.ultradns.net
Address:  64.6.64.6
```

### DNS Cache Management

#### Windows DNS Cache Operations

```cmd
# Display current DNS cache
ipconfig /displaydns

# Clear DNS cache
ipconfig /flushdns

# Register DNS name
ipconfig /registerdns
```

#### Linux DNS Cache Operations

```bash
# Clear systemd-resolved cache
sudo systemd-resolve --flush-caches

# Clear nscd cache (if running)
sudo systemctl restart nscd

# Clear dnsmasq cache (if running)
sudo systemctl restart dnsmasq
```

### Advanced DNS Tools

#### dig Command (Linux/macOS)

```bash
# Basic dig query
dig armourinfosec.com

# Specific record types
dig armourinfosec.com A
dig armourinfosec.com MX
dig armourinfosec.com TXT

# Query specific server
dig @8.8.8.8 armourinfosec.com

# Trace query path
dig +trace armourinfosec.com

# Short answer only
dig +short armourinfosec.com
```

#### host Command (Linux/macOS)

```bash
# Basic host query
host armourinfosec.com

# Specific record type
host -t MX armourinfosec.com
host -t TXT armourinfosec.com

# Reverse lookup
host 8.8.8.8
```

### DNS Record Examples

#### Complete DNS Zone File Example

```
$TTL 86400
@   IN  SOA ns1.example.com. admin.example.com. (
        2023061801  ; Serial number
        28800       ; Refresh (8 hours)
        7200        ; Retry (2 hours)
        604800      ; Expire (7 days)
        86400       ; Minimum TTL (1 day)
        )

; Name servers
@       IN  NS      ns1.example.com.
@       IN  NS      ns2.example.com.

; A records
@       IN  A       203.0.113.1
www     IN  A       203.0.113.1
mail    IN  A       203.0.113.2
ftp     IN  A       203.0.113.3

; AAAA records (IPv6)
@       IN  AAAA    2001:db8::1
www     IN  AAAA    2001:db8::1

; CNAME records
blog    IN  CNAME   www.example.com.
shop    IN  CNAME   www.example.com.

; MX records
@       IN  MX  10  mail.example.com.
@       IN  MX  20  backup-mail.example.com.

; TXT records
@       IN  TXT     "v=spf1 mx ip4:203.0.113.2 -all"
@       IN  TXT     "google-site-verification=abc123def456"

; SRV records
_sip._tcp   IN  SRV 10 5 5060 sip.example.com.
```

### DNS Troubleshooting

#### Common DNS Issues

1. **DNS Cache Problems**: Stale cache entries
2. **Propagation Delays**: DNS changes not yet propagated
3. **Misconfigured Records**: Incorrect DNS record values
4. **Nameserver Issues**: Authoritative servers down
5. **Network Connectivity**: Cannot reach DNS servers

#### Troubleshooting Steps

```bash
# 1. Check local DNS resolution
nslookup domain.com

# 2. Try different DNS servers
nslookup domain.com 8.8.8.8
nslookup domain.com 1.1.1.1

# 3. Check authoritative servers
nslookup -type=NS domain.com
nslookup domain.com ns1.domain.com

# 4. Verify specific records
nslookup -type=A domain.com
nslookup -type=MX domain.com

# 5. Test connectivity to DNS servers
ping 8.8.8.8
telnet 8.8.8.8 53
```

### DNS Security Considerations

#### DNS Security Extensions (DNSSEC)

- **Purpose**: Authenticate DNS responses
- **Protection**: Against DNS spoofing and cache poisoning
- **Records**: RRSIG, DNSKEY, DS, NSEC

#### DNS over HTTPS (DoH) / DNS over TLS (DoT)

- **Purpose**: Encrypt DNS queries
- **Privacy**: Prevent DNS query interception
- **Providers**: Cloudflare (1.1.1.1), Google (8.8.8.8)

## Study Questions

1. How does the DNS hierarchy ensure global scalability?
2. What are the differences between authoritative and recursive DNS servers?
3. How do different DNS record types work together to provide services?
4. What security measures can protect DNS infrastructure?

## Next Class Preview

- DHCP server configuration and policies
- Linux command chaining and background processes
- Text processing with pipes and filters
- System monitoring and process management
