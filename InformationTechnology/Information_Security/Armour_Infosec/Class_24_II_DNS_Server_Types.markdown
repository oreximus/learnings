# Class 24-II: DNS Server Types

## Overview
This class categorizes DNS server types and their roles.

## DNS Server Types
1. **Root Domain Servers**:
   - 13 servers globally, store TLD server locations.
2. **TLD Name Servers**:
   - Manage TLD records (e.g., `.com`, `.org`).
   - Store NS and glue records.
3. **Authoritative Name Servers**:
   - Store domain-specific records (e.g., A, MX).
4. **Recursive (Caching) DNS Servers**:
   - Resolve queries by querying root, TLD, and authoritative servers.
   - Cache results for faster future queries.
   - Example: Google DNS (8.8.8.8).
5. **Forwarding DNS Servers**:
   - Forward queries to another DNS server (e.g., ISP’s DNS).
   - Used in small networks for simplicity.

## Corrections
- Added recursive and forwarding DNS server descriptions for completeness.