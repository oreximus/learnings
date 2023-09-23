# Hacking Guide

**This guide contains the collection of strategies and ways to get the job done at playing CTF or Doing something tweaky-twisty to get the way around with Information Technology.**

## Privilege Escalation

### Systemctl Status

- **systemctl status** privilege escalation: https://exploit-notes.hdks.org/exploit/linux/privilege-escalation/sudo/sudo-systemctl-privilege-escalation/
- you can put !sh in the less.

## Tools Usages:

### Ffuf

- **for subdomain enumeration**:

👉[**source**](https://medium.com/quiknapp/fuzz-faster-with-ffuf-c18c031fc480)👈
```
ffuf -w subdomains.txt -u http://website.com/ -H “Host: FUZZ.website.com”
```


