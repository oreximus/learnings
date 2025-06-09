# Class 18-II: DNS Server

## Overview
This class explains how DNS servers work and their hierarchy.

## DNS Server Hierarchy
1. **Root DNS Servers**:
   - 13 globally distributed servers (A–M).
   - Store locations of TLD name servers, not domain-to-IP mappings.
2. **TLD Name Servers**:
   - Manage TLD records (e.g., .com, .org).
   - Store NS records and glue records for domains.
3. **Authoritative Name Servers**:
   - Hold actual DNS records (e.g., A, MX) for a domain.

## DNS Resolution Process
1. Browser checks local cache.
2. Queries hosts file (`/etc/hosts` or `C:\Windows\System32\drivers\etc\hosts`).
3. Queries recursive DNS server (e.g., 8.8.8.8).
4. Recursive server queries:
   - Root server for TLD server location.
   - TLD server for authoritative server location.
   - Authoritative server for IP address.
5. Returns IP to browser for connection.

## Corrections
- Clarified that root servers store TLD server locations, not domain IPs.
- Added detailed DNS resolution process.