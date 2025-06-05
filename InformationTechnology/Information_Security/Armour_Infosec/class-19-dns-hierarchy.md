# Class 19: Complete DNS System Hierarchy

## DNS Server Hierarchy and Functionality

### 1. Root DNS Servers

- **Quantity**: 13 root servers worldwide (labeled A through M)
- **Operators**: Various organizations (VeriSign, NASA, US Army, etc.)
- **Function**: Do NOT store actual domain-to-IP mappings
- **Storage**: Information about TLD (Top-Level Domain) name servers
- **Response**: Provides names and IP addresses of TLD nameservers

#### Root Server Locations

- **A**: VeriSign (Dulles, VA)
- **B**: USC-ISI (Marina del Rey, CA)
- **C**: Cogent Communications (multiple locations)
- **D**: University of Maryland (College Park, MD)
- **E**: NASA Ames Research Center (Mountain View, CA)
- **F**: Internet Systems Consortium (Palo Alto, CA)
- **G**: US DOD Network Information Center (Vienna, VA)
- **H**: US Army Research Lab (Aberdeen, MD)
- **I**: Netnod (Stockholm, Sweden)
- **J**: VeriSign (multiple locations)
- **K**: RIPE NCC (London, Amsterdam)
- **L**: ICANN (Los Angeles, CA)
- **M**: WIDE Project (Tokyo, Japan)

### 2. TLD (Top-Level Domain) Name Servers

- **Function**: Manage TLD domain records (.com, .org, .net, etc.)
- **Storage**: Do NOT store final IP addresses
- **Response**: Provide authoritative nameserver information for domains
- **Examples**:
  - .com managed by VeriSign
  - .org managed by Public Interest Registry
  - .net managed by VeriSign

#### TLD Server Responsibilities

- **Domain Registration**: Track registered domains in their TLD
- **Nameserver Delegation**: Point to authoritative nameservers
- **Glue Records**: Provide IP addresses when nameserver is in same domain

### 3. Authoritative Name Servers

- **Function**: Hold actual DNS records for specific domains
- **Storage**: A records, AAAA records, MX records, etc.
- **Response**: Provide final IP addresses for domain queries
- **Control**: Managed by domain owners or their DNS providers

## DNS Resolution Process (Complete Flow)

### Step-by-Step DNS Query Resolution

#### 1. Initial Query

\`\`\`
User types: www.example.com
Browser initiates DNS lookup
\`\`\`

#### 2. Local DNS Cache Check

- **Browser Cache**: Check browser's DNS cache
- **OS Cache**: Check operating system DNS cache
- **Hosts File**: Check local hosts file (/etc/hosts or C:\Windows\System32\drivers\etc\hosts)

#### 3. Recursive DNS Server Query

- **ISP DNS**: Query ISP's recursive DNS server
- **Public DNS**: Query public DNS (8.8.8.8, 1.1.1.1)
- **Cache Check**: Recursive server checks its cache

#### 4. Root Server Query

\`\`\`
Recursive DNS → Root Server
Query: "Where can I find .com domains?"
Response: "Ask the .com TLD servers at these IPs"
\`\`\`

#### 5. TLD Server Query

\`\`\`
Recursive DNS → .com TLD Server
Query: "Where can I find example.com?"
Response: "Ask example.com's nameservers at these IPs"
\`\`\`

#### 6. Authoritative Server Query

\`\`\`
Recursive DNS → example.com Authoritative Server
Query: "What's the IP for www.example.com?"
Response: "93.184.216.34"
\`\`\`

#### 7. Response Chain

\`\`\`
Authoritative Server → Recursive DNS → Client
Final Response: www.example.com = 93.184.216.34
\`\`\`

## Internet Statistics and Scale

### Current Internet Size (May 2025)

- **Total Sites**: 1,227,232,638 sites
- **Total Domains**: 277,546,948 domains
- **Web-facing Computers**: 13,470,692 computers
- **Monthly Growth**: 8.9 million new sites
- **Source**: Netcraft Web Server Survey

### DNS Query Volume

- **Global DNS Queries**: Trillions per day
- **Root Server Queries**: Hundreds of billions daily
- **Response Time**: Typically under 100ms
- **Cache Hit Rate**: 85-95% of queries served from cache

## DNS Performance Optimization

### Caching Strategies

- **Browser Cache**: 1-24 hours typical TTL
- **OS Cache**: System-level DNS caching
- **ISP Cache**: Large-scale regional caching
- **CDN Integration**: Content delivery network DNS optimization

### Geographic Distribution

- **Anycast**: Same IP announced from multiple locations
- **Edge Servers**: DNS servers closer to users
- **Load Balancing**: Distribute queries across servers
- **Redundancy**: Multiple servers prevent single points of failure

## DNS Security Considerations

### Common DNS Attacks

- **DNS Spoofing**: Fake DNS responses
- **Cache Poisoning**: Corrupt DNS cache entries
- **DDoS Attacks**: Overwhelm DNS servers
- **DNS Tunneling**: Use DNS for unauthorized data transfer

### Security Measures

- **DNSSEC**: Digital signatures for DNS records
- **DNS over HTTPS (DoH)**: Encrypted DNS queries
- **DNS over TLS (DoT)**: TLS-encrypted DNS
- **Rate Limiting**: Prevent abuse and attacks

## Practical DNS Tools

### Command Line Tools

```bash
# DNS lookup tools
nslookup domain.com
dig domain.com
host domain.com

# Trace DNS resolution path
dig +trace domain.com
```

### Online DNS Tools

- **DNS Propagation Checkers**: Check global DNS updates
- **DNS Lookup Tools**: Web-based DNS queries
- **WHOIS Databases**: Domain registration information
- **DNS Health Checkers**: Validate DNS configuration
