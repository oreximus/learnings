# Class 23: DNS Records and `nslookup`

## Overview

This class delves into the different types of records stored in DNS and introduces the `nslookup` command-line tool for querying DNS servers to retrieve this information.

## DNS Records

DNS records are instructions stored in authoritative DNS servers that provide information about a domain.

* **`A` Record (Address Record)**: Maps a domain name to an IPv4 address.
* **`AAAA` Record (Quad A Record)**: Maps a domain name to an IPv6 address.
* **`CNAME` Record (Canonical Name)**: Creates an alias, pointing one domain name to another. It's useful for pointing multiple subdomains (like `www.example.com` and `blog.example.com`) to a single main domain.
* **`MX` Record (Mail Exchanger)**: Specifies the mail servers responsible for accepting email messages on behalf of a domain. It includes a preference value to prioritize servers.
* **`NS` Record (Name Server)**: Delegates a DNS zone to use the given authoritative name servers. It tells the internet where to find the domain's DNS records.
* **`TXT` Record (Text Record)**: Provides text information to sources outside your domain. It is widely used for domain verification and email security policies like:
    * **SPF (Sender Policy Framework)**: Helps prevent email spoofing by listing authorized mail servers.
    * **DKIM (DomainKeys Identified Mail)**: Adds a digital signature to emails to verify their authenticity.
    * **DMARC (Domain-based Message Authentication, Reporting, and Conformance)**: An email authentication policy and reporting protocol that builds on SPF and DKIM.
* **`SOA` Record (Start of Authority)**: Contains administrative information about the domain, such as the primary name server, the email of the domain administrator, and timers for zone refreshes.
* **`PTR` Record (Pointer Record)**: Used for reverse DNS lookups, mapping an IP address back to a domain name.
* **`SRV` Record (Service Record)**: Specifies the location (hostname and port number) of servers for specific services, like VoIP or instant messaging.
* **`CAA` Record (Certification Authority Authorization)**: Specifies which Certificate Authorities (CAs) are allowed to issue SSL/TLS certificates for a domain.

---

## Using `nslookup`

`nslookup` is a command-line tool for querying DNS to obtain domain name or IP address mapping information.

* **Note**: `nslookup` queries do not go into the local DNS cache.

#### Basic Query

This will look up the A and AAAA records by default.

```bash
nslookup armourinfosec.com
```


#### Querying for a Specific Record Type

Use the `-type=` option to specify the record you want to see.

* **A Records**:
    ```bash
    nslookup -type=A armourinfosec.com
    ```
   

* **AAAA Records**:
    ```bash
    nslookup -type=AAAA armourinfosec.com
    ```
   

* **MX Records**:
    ```bash
    nslookup -type=MX armourinfosec.com
    ```
   

* **TXT Records**:
    ```bash
    nslookup -type=TXT armourinfosec.com
    ```
   

* **SOA Record**:
    ```bash
    nslookup -type=SOA armourinfosec.com
    ```
   

#### Querying a Specific DNS Server

You can tell `nslookup` to use a specific DNS server for the query, instead of your system's default.

```bash
# Query armourinfosec.com using Verisign's public DNS server (64.6.64.6)
nslookup armourinfosec.com 64.6.64.6
```

