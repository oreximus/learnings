# Class 20: How DNS Works

## Overview

This class explains the process of DNS resolution, detailing the roles of the different types of DNS servers that work together to translate a domain name into an IP address.

## The DNS Resolution Process

When you type a domain name into your browser, the following steps typically occur:

1.  **Browser/OS Cache Check**: Your computer first checks its own local DNS cache to see if it has recently looked up this domain. Windows users can view this cache with `ipconfig /displaydns`.
2.  **Hosts File Check**: If not in the cache, the system checks the `hosts` file (`C:\Windows\System32\drivers\etc\hosts` on Windows, `/etc/hosts` on Linux). This file can be used to manually map domain names to IP addresses.
3.  **Recursive DNS Server Query**: If the address is not found locally, the query is sent to a **Recursive DNS Server** (also called a resolver). This server is usually provided by your ISP or a public DNS service like Google (`8.8.8.8`) or Cloudflare (`1.1.1.1`). The recursive server's job is to find the answer for you.
4.  **Root Server Query**: The recursive server, if it doesn't have the answer cached, queries one of the 13 **Root DNS Servers**. These root servers don't know the IP address, but they know where to find the servers for the Top-Level Domain (TLD). They respond with the IP address of the `.com` TLD name server.
5.  **TLD Name Server Query**: The recursive server then queries the **TLD Name Server** (in this case, for `.com`). The TLD server doesn't have the final IP address either, but it knows the authoritative name server for the specific domain (`example.com`). It responds with the IP address of the domain's authoritative name server.
6.  **Authoritative Name Server Query**: Finally, the recursive server queries the **Authoritative Name Server** for `example.com`. This server is the final authority for the domain and holds the actual DNS records. It looks up the 'A' record for `www.example.com` and responds with the definitive IP address.
7.  **Response to Client**: The recursive server sends the IP address back to your computer. It also caches this information for a set amount of time (defined by the TTL, or Time-To-Live) so it can answer future requests for the same domain more quickly.
8.  **Browser Connects**: Your browser now has the IP address and can establish a direct connection to the web server to load the website.

## Types of DNS Servers

* **Recursive (Caching) DNS Server**: The server that receives the initial query from the client and performs the full resolution process.
* **Root DNS Server**: There are 13 logical root servers (named A to M) that sit at the top of the hierarchy and direct traffic to the TLD servers.
* **TLD Name Server**: Manages all the domain names for a specific TLD (like `.com` or `.org`).
* **Authoritative Name Server**: Holds the actual DNS records (A, CNAME, MX, etc.) for a specific domain.

## Whois

**Whois** is a protocol used to query databases that store the registration information of a domain name. A Whois lookup can provide:
* Domain Name and Status
* Registrar and Registrant Information
* Registration and Expiry Dates
* Name Servers used by the domain
* Technical and Administrative Contacts

