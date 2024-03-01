# Cheatsheet for CTFs, Pentesting and Bug Hunting.

## Web Application Specific:

**Network Scanning Top 1000 Ports**:

```
rustscan -a <target_ip> -- -sC -sV -oN tools/nmap/scan_box
```

**Subdomain Enumeration using Gobuser**:

```
gobuster vhost -u http://pov.htb/ -t 35 -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt --append-domain -k --no-error
```

**Directory Scanning using Feroxbuster**:

```

```
