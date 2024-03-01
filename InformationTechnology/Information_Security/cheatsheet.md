# Cheatsheet for CTFs, Pentesting and Bug Hunting.

## Web Application Specific:

**Network Scanning Top 1000 Ports**:

```
rustscan -a <target_ip> -- -sC -sV -oN tools/nmap/scan_box
```

**Subdomain Enumeration using Ffuf**:

```
ffuf -w ~/HacknTools/wordlists/subdomain/subdomains-10000.txt -u TARGET -fc 200
```

**Directory Scanning using Feroxbuster**:

```

```
