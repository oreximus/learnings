# Class 18: Domain Name System (DNS) Fundamentals

## Theory Section

### Domain Name Structure

#### Domain Name Components

```
subdomain.second-level.top-level.root
    │         │           │      │
    │         │           │      └── Root (invisible .)
    │         │           └───────── TLD
    │         └───────────────────── SLD
    └─────────────────────────────── Subdomain
```

#### Example: www.google.com

- **Root**: . (implicit)
- **TLD**: .com
- **SLD**: google
- **Subdomain**: www

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

### DNS Server Hierarchy

#### 1. Root DNS Servers

- **Quantity**: 13 root servers worldwide (A through M)
- **Operators**: Various organizations (Verisign, NASA, etc.)
- **Function**: Don't store domain-to-IP mappings
- **Storage**: Information about TLD nameserver locations
- **Content**: Names and IPs of TLD nameservers

#### 2. TLD (Top-Level Domain) Nameservers

- **Function**: Manage TLD domain records
- **Storage**: Delegation information for domains within their TLD
- **Content**: NS records for authoritative nameservers
- **Examples**: .com servers, .org servers, .net servers

#### 3. Authoritative Nameservers

- **Function**: Hold actual DNS records for domains
- **Storage**: A, AAAA, CNAME, MX, TXT records
- **Authority**: Final source of truth for domain records
- **Management**: Controlled by domain owners

### DNS Resolution Process

#### Step-by-Step Query Resolution

1. **Browser Cache Check**: Local browser DNS cache
2. **Operating System Cache**: System DNS cache
3. **Hosts File Check**: /etc/hosts or C:\Windows\System32\drivers\etc\hosts
4. **Recursive DNS Server**: ISP or public DNS (8.8.8.8)
5. **Root Server Query**: Query root servers for TLD info
6. **TLD Server Query**: Query TLD servers for authoritative NS
7. **Authoritative Query**: Query authoritative servers for record
8. **Response Chain**: Answer travels back through the chain

## Practical Section

### WHOIS Information

#### WHOIS Database Contents

- **Domain Name and Status**: Registration status, locks
- **Registrar Information**: Company managing the domain
- **Registrant Details**: Domain owner information
- **Registration Dates**: Created, updated, expires
- **Nameservers**: Authoritative DNS servers
- **Technical Contacts**: Technical management contacts
- **Administrative Contacts**: Administrative contacts

### DNS Records Overview

#### A Record (Address Record)

- **Purpose**: Maps domain name to IPv4 address
- **Format**: domain.com → 192.168.1.100
- **TTL**: Time to Live (cache duration)
- **Example**: www.example.com → 203.0.113.1

#### AAAA Record (IPv6 Address Record)

- **Purpose**: Maps domain name to IPv6 address
- **Format**: domain.com → 2001:db8::1
- **Usage**: IPv6 connectivity
- **Example**: www.example.com → 2001:db8:85a3::8a2e:370:7334

#### CNAME Record (Canonical Name)

- **Purpose**: Creates alias for another domain name
- **Usage**: Point multiple subdomains to single domain
- **Restriction**: Cannot coexist with other records for same name
- **Example**: blog.example.com → myblog.wordpress.com

#### MX Record (Mail Exchange)

- **Purpose**: Specifies mail servers for domain
- **Priority**: Lower numbers = higher priority
- **Format**: domain.com → priority mail-server.com
- **Example**: example.com → 10 mail.example.com

#### TXT Record (Text Record)

- **Purpose**: Store text information for domain
- **Usage**: Domain verification, email authentication
- **SPF**: Sender Policy Framework (email spoofing protection)
- **DMARC**: Domain-based Message Authentication
- **DKIM**: DomainKeys Identified Mail (email signatures)

#### NS Record (Name Server)

- **Purpose**: Specifies authoritative nameservers for domain
- **Delegation**: Points to servers that host DNS records
- **Example**: example.com → ns1.example.com, ns2.example.com

#### SOA Record (Start of Authority)

- **Purpose**: Administrative information about domain
- **Contents**: Primary nameserver, admin email, serial number
- **Timers**: Refresh, retry, expire, minimum TTL

#### PTR Record (Pointer Record)

- **Purpose**: Reverse DNS lookup (IP to domain)
- **Usage**: Email server verification, logging
- **Format**: IP address → domain name
- **Example**: 1.113.0.203.in-addr.arpa → www.example.com

### DNS Query Tools

#### nslookup Command

```bash
# Basic query
nslookup armourinfosec.com

# Specific record types
nslookup -type=A armourinfosec.com
nslookup -type=AAAA armourinfosec.com
nslookup -type=MX armourinfosec.com
nslookup -type=TXT armourinfosec.com
nslookup -type=SOA armourinfosec.com
nslookup -type=NS armourinfosec.com

# Query specific DNS server
nslookup armourinfosec.com 8.8.8.8
nslookup armourinfosec.com 1.1.1.1
```

### DNS Cache Management

#### Windows DNS Cache

```cmd
# Display DNS cache
ipconfig /displaydns

# Flush DNS cache
ipconfig /flushdns

# Register DNS
ipconfig /registerdns
```

#### Linux DNS Cache

```bash
# Flush systemd-resolved cache
sudo systemd-resolve --flush-caches

# Restart DNS service
sudo systemctl restart systemd-resolved

# Check DNS statistics
systemd-resolve --statistics
```

## Study Questions

1. How does the DNS hierarchy ensure scalability and reliability?
2. What is the difference between recursive and authoritative DNS servers?
3. How do different DNS record types serve different purposes?
4. What information can be gathered from WHOIS databases?

## Next Class Preview

- DNS record types in detail
- DNS server configuration
- DNS troubleshooting techniques
