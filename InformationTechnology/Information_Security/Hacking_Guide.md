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

## Web Application Testing

### Spring Boot Tips:

- Check for the common errors that appeared in Springboot.

- Directory Scanning with spring-boot specific wordlist.

### DOM XSS

👉[**source**](https://www.youtube.com/watch?v=ojiOCfg-FXU)👈

- using portswigger webacademy

- taking place in browser client-side

- searching through scripts, apart from that we have strings

- referencing things with DOM XSS wiki

- testing the script function in console:

```
// i.e.

location.search

//output

'productId=1'

// For checking XSS, alter the Parameter in URL, where it's getting fetched from

'productID=1&test=test'
```

- if the last output comes in the output then the XSS worked!
