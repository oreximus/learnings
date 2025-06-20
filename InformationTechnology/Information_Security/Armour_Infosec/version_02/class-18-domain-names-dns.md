# Class 18: Domain Name System and DNS Records

## Theory Section

### Domain Name Structure and Valuation

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

### Domain Appraisal Factors

#### 1. Top-Level Domain (TLD) Impact

- **.com**: Highest value, most trusted
- **.org**: Good for organizations
- **.net**: Technical/network related
- **Country TLDs**: Local market value
- **New gTLDs**: Variable value

#### 2. Domain Length and Simplicity

- **Short domains**: Higher value (1-6 characters premium)
- **Easy to type**: Reduces user errors
- **Easy to remember**: Better for branding
- **No hyphens/numbers**: Generally more valuable

#### 3. Keyword Value and Search Volume

- **Exact match domains**: SEO benefits
- **High search volume keywords**: More valuable
- **Commercial intent**: Business-related terms
- **Industry relevance**: Sector-specific value

#### 4. Brandability

- **Pronounceable**: Easy to say and remember
- **Unique**: Distinctive and memorable
- **Trademark issues**: Avoid conflicts
- **Global appeal**: International usability

#### 5. Market Trends and Niche Popularity

- **Emerging industries**: AI, crypto, green energy
- **Seasonal trends**: Holiday, event-related
- **Geographic trends**: Local market demands
- **Technology trends**: New tech adoption

#### 6. Existing Traffic and SEO Metrics

- **Direct traffic**: Type-in traffic value
- **Backlink profile**: SEO authority
- **Search rankings**: Existing positions
- **Social media presence**: Brand recognition

#### 7. Past Sales of Similar Domains

- **Comparable sales**: Similar domain transactions
- **Market benchmarks**: Industry standards
- **Auction results**: Public sale prices
- **Broker valuations**: Professional assessments

## DNS Server Architecture

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

#### WHOIS Query Examples

```bash
# Command line WHOIS
whois google.com
whois armourinfosec.com

# Online WHOIS tools
# whois.net, whois.com, domain registrar websites
```

### DNS Records Deep Dive

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
- **Example**: Contains zone transfer and caching parameters

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

#### dig Command (Linux)

```bash
# Basic query
dig armourinfosec.com

# Specific record types
dig armourinfosec.com A
dig armourinfosec.com AAAA
dig armourinfosec.com MX
dig armourinfosec.com TXT

# Query specific server
dig @8.8.8.8 armourinfosec.com

# Trace query path
dig +trace armourinfosec.com
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

### Practical DNS Examples

#### Example DNS Record Set

```
example.com.        IN  SOA   ns1.example.com. admin.example.com. (
                            2023061801  ; Serial
                            28800       ; Refresh (8 hours)
                            7200        ; Retry (2 hours)
                            604800      ; Expire (7 days)
                            86400       ; Minimum TTL (1 day)
                            )

example.com.        IN  NS    ns1.example.com.
example.com.        IN  NS    ns2.example.com.
example.com.        IN  A     203.0.113.1
www.example.com.    IN  A     203.0.113.1
mail.example.com.   IN  A     203.0.113.2
example.com.        IN  MX    10 mail.example.com.
blog.example.com.   IN  CNAME www.example.com.
example.com.        IN  TXT   "v=spf1 mx -all"
```

#### DNS Troubleshooting Commands

```bash
# Test DNS resolution
ping google.com

# Trace DNS query path
dig +trace google.com

# Check specific nameserver
nslookup google.com ns1.google.com

# Verify reverse DNS
nslookup 8.8.8.8
```

## Study Questions

1. What factors determine the value of a domain name?
2. How does the DNS hierarchy ensure scalability and reliability?
3. What is the difference between recursive and authoritative DNS servers?
4. How do different DNS record types serve different purposes?

## Next Class Preview

- DHCP configuration and policies
- Linux command chaining and pipes
- Background process management
- Text processing and filtering
