# Class 22-II: DNS Resolution

## Overview
This class recaps the DNS resolution process and server types.

## DNS Server Types
1. **Root Domain Servers**: 13 servers (A–M), store TLD server locations.
2. **TLD Name Servers**: Manage TLDs, store NS and glue records.
3. **Authoritative Name Servers**: Store domain DNS records (e.g., A, MX).

## DNS Resolution Process
1. Browser checks cache.
2. Checks hosts file.
3. Queries recursive DNS server.
4. Recursive server queries:
   - Root server.
   - TLD server.
   - Authoritative server.
5. Returns IP to browser.

## Corrections
- Original recap was accurate; added structure for clarity.