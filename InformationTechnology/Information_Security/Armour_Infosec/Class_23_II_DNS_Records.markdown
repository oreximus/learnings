# Class 23-II: DNS Records

## Overview
This class covers DNS record types and their usage, with examples using `nslookup`.

## DNS Record Types
- **A**: Maps domain to IPv4 (e.g., `185.199.108.153`).
- **AAAA**: Maps domain to IPv6 (e.g., `2606:50c0:8000::153`).
- **CNAME**: Aliases one domain to another (e.g., `blog.example.com` to `myblog.example.com`).
- **MX**: Specifies mail servers (e.g., `mail.armourinfosec.io`).
- **TXT**: Stores text data (e.g., SPF, DKIM for email security).
- **NS**: Specifies authoritative name servers.
- **SOA**: Administrative info (e.g., primary NS, refresh interval).
- **PTR**: Reverse DNS (IP to domain).
- **SRV**: Service location (e.g., for VoIP).
- **CAA**: Specifies allowed certificate authorities.

## nslookup Examples
- **General Query**:
  ```bash
  nslookup armourinfosec.com
  ```
- **A Record**:
  ```bash
  nslookup -type=A armourinfosec.com
  ```
- **AAAA Record**:
  ```bash
  nslookup -type=AAAA armourinfosec.com
  ```
- **MX Record**:
  ```bash
  nslookup -type=MX armourinfosec.com
  ```
- **TXT Record**:
  ```bash
  nslookup -type=TXT armourinfosec.com
  ```
- **SOA Record**:
  ```bash
  nslookup -type=SOA armourinfosec.com
  ```
- **Specific DNS Server**:
  ```bash
  nslookup armourinfosec.com 64.6.64.6
  ```

## DNS Cache Management (Windows)
- **View Cache**:
  ```cmd
  ipconfig /displaydns
  ```
- **Clear Cache**:
  ```cmd
  ipconfig /flushdns
  ```

## Corrections
- Corrected `nslookup` output formatting for clarity.
- Added `SRV` and `CAA` record descriptions.