# Class 19-I: Domain Name System (DNS)

## Overview
This class provides comprehensive notes on the Domain Name System (DNS), its structure, and key concepts.

## Domain Name Structure
- **Format**: `subdomain.second-level.top-level.root`
- **Example**: `www.example.com.`
  - **Root**: `.` (implicit)
  - **TLD**: `.com`
  - **SLD**: `example`
  - **Subdomain**: `www`
- **Reading**: Right to left (highest to lowest hierarchy).

## Top-Level Domains (TLD)
1. **Generic TLDs (gTLDs)**:
   - Unsponsored: `.com`, `.net`, `.org`, `.info`, `.biz`
   - Restricted: `.gov`, `.edu`, `.mil`
2. **Sponsored TLDs (sTLDs)**:
   - `.aero`, `.museum`, `.travel`, `.coop`, `.jobs`
3. **Country Code TLDs (ccTLDs)**:
   - `.us`, `.uk`, `.in`, `.jp`, `.au`
4. **Infrastructure TLD**: `.arpa`
5. **New gTLDs**: `.google`, `.tech`, `.blog`

## Second-Level Domains (SLD)
- **Definition**: The part to the left of the TLD (e.g., `google` in `google.com`).
- **Registration**: Must be unique within TLD; 63-character limit; letters, numbers, hyphens allowed.

## Subdomains
- **Definition**: Levels under SLD (e.g., `www`, `mail`).
- **Properties**: Unlimited, no registration needed, controlled by domain owner.

## Domain Registration
- **Process**:
  1. Choose SLD + TLD.
  2. Register via ICANN-accredited registrar (e.g., GoDaddy).
  3. Pay annual fee.
  4. Provide WHOIS data.
  5. Configure DNS records.
- **Pricing**: $10–$15/year (standard); $100–millions (premium).

## DNS Hierarchy
- **Root Level**: 13 servers, store TLD server info.
- **TLD Level**: Manage SLD records.
- **SLD Level**: Authoritative servers for domain records.
- **Subdomain Level**: Additional records under SLD.

## Key Terminology
- **FQDN**: Fully Qualified Domain Name (e.g., `www.example.com.`).
- **Hostname**: Subdomain or device name (e.g., `www`).
- **DNS Records**:
  - **A**: IPv4 address.
  - **AAAA**: IPv6 address.
  - **CNAME**: Alias to another domain.
  - **MX**: Mail server.
  - **NS**: Name server.
  - **TXT**: Text data (e.g., SPF, DKIM).

## Best Practices
- **Domain Selection**: Choose memorable, brandable names; avoid hyphens/numbers.
- **DNS Management**: Use reliable providers, monitor propagation, use DNSSEC.
- **Security**: Enable domain locking, use strong passwords.

## Corrections
- Original notes were accurate and comprehensive; minor clarifications added for readability.