# Curriculum of Advanced Web Applicaiton Security Testing (Armour Infosec)
## THIS IS THE UPDATED VERSION BY MENTIONED SOURCE

**Date: 2026-08-17**

**Source**: https://claude.ai/share/9a676608-9e1f-4143-8255-556b7f8552b9

Looking at this list, a few things stand out: some items don't belong in a "PHP and Web Application Fundamentals" module at all (they look like they wandered in from an AI/tooling module), and there are real gaps in PHP and web fundamentals that the later security-testing lessons (XSS, SQLi, LFI, etc.) will assume you already know.

**What's misplaced (should be removed or moved elsewhere):**
- **NVIDIA Driver and CUDA Toolkit Installation on Kali Linux** — this is GPU/AI tooling, not a web app or PHP topic. Doesn't belong here at all.
- **Running Local AI Models on Kali Linux** — same issue, and it's oddly dropped between "PHP Control Structures" and "PHP foreach Loops," breaking the PHP learning flow.
- **Indicator Sysmonitor Installation** — a desktop system-tray monitoring tool, unrelated to PHP/web fundamentals.

These three look like they belong to a separate "AI-assisted testing" or "Kali environment tooling" module, not this one.

**What's missing (needed before the security modules make sense):**
- PHP tags/syntax and variables (currently jumps straight to Comments → Data Types with no "how PHP code is structured" lesson)
- Operators in PHP
- String functions in PHP
- Regular Expressions in PHP (heavily used later in filtering/WAF bypass topics)
- Error handling / `try-catch` in PHP
- Basic OOP in PHP (classes/objects) — most modern vulnerable apps use OOP
- Connecting PHP to MySQL (`mysqli`/PDO) — you have "MySQL and Database Concepts" but nothing on PHP-to-DB connection
- Writing basic SQL queries (SELECT/INSERT/UPDATE/DELETE) — foundational before SQLi later
- Prepared Statements — important as the "secure baseline" contrast
- Same-Origin Policy & CORS — needed context for later CSRF/XSS modules
- HTTPS/TLS basics — sits naturally after HTTP
- URL Encoding/Decoding — needed to understand `$_GET`, payloads, etc.
- Client-side vs Server-side execution (JS vs PHP) — good to add near "Static vs Dynamic Files"

Here's the reorganized list:

**Environment Setup**
1. Vulnerable VM Setup
2. Debian System Setup
3. Apache2 Setup on Debian

**Web Fundamentals**
4. Web Application
5. Client-Side vs Server-Side Execution *(new)*
6. HTTP (HyperText Transfer Protocol)
7. HTTPS and TLS Basics *(new)*
8. HTTP Methods: API Endpoint vs Server Level
9. Static Files and Dynamic Files on the Server
10. Same-Origin Policy & CORS *(new)*
11. URL Encoding/Decoding *(new)*

**PHP Language Basics**
12. PHP and MySQL
13. PHP Syntax, Tags and Variables *(new)*
14. PHP Comments
15. Environment Types in Software Development
16. PHP Operators *(new)*
17. PHP Data Types
18. Arrays in PHP
19. PHP String Functions *(new)*
20. PHP Control Structures
21. PHP foreach Loops
22. PHP Functions
23. Basic OOP in PHP: Classes and Objects *(new)*
24. Error Handling in PHP *(new)*
25. Regular Expressions in PHP *(new)*

**PHP Superglobals, Forms & Sessions**
26. PHP Super Global Variables
27. PHP $_GET – Using URL Parameters
28. PHP $_POST Superglobal
29. Detecting Form Submissions in PHP
30. PHP $_SERVER
31. PHP File Upload Using $_FILES
32. PHP Cookie
33. PHP $_SESSION
34. PHP Form Validation: Step-by-Step Guide
35. Including and Requiring Files in PHP

**Output Handling & Security Headers**
36. HTML Encoding Functions
37. Modifying Headers
38. Content-Security-Policy (CSP)
39. Referrer-Policy

**Database Layer**
40. MySQL and Database Concepts
41. Connecting PHP to MySQL (mysqli/PDO) *(new)*
42. Writing Basic SQL Queries (SELECT/INSERT/UPDATE/DELETE) *(new)*
43. Prepared Statements *(new)*

A couple of clarifying questions worth considering: do you want the NVIDIA/CUDA, local AI models, and Indicator Sysmonitor lessons kept somewhere else in the course (e.g., a "Kali tooling" module), or dropped entirely? And should GET/POST/SERVER superglobals keep the literal `$_GET`/`$_POST` naming (your original list has some inconsistent slashes/underscores in the titles, e.g. "PHP $GET" vs "PHP $_GET") — worth cleaning up for consistency on the site.

## Advanced Version:

Here's the Advanced module — this is where everything trimmed from Fundamentals (SQLi/XSS/CSRF deep-dives, API security, auth attacks, dev-tooling security) properly belongs, organized as a progression from injection basics through modern app architecture attacks.

## Injection Vulnerabilities
1. SQL Injection Fundamentals (Error-Based, Union-Based, Boolean-Based)
2. Blind and Time-Based SQL Injection
3. SQLi in PHP: mysqli vs PDO, Emulated Prepares Risk, Bypassing Weak Filters
4. Second-Order SQL Injection
5. NoSQL Injection Basics (MongoDB Operators, PHP Drivers)
6. Command Injection and OS Command Execution via PHP (`exec`, `shell_exec`, `system`)
7. Code Injection and PHP Object Injection (`unserialize()` Exploitation)
8. LDAP and XML Injection (XXE – XML External Entity Attacks)
9. Server-Side Template Injection (SSTI) in PHP Templating Engines

## Cross-Site Scripting and Client-Side Attacks
10. Reflected XSS
11. Stored XSS
12. DOM-Based XSS
13. Context-Aware Output Encoding and Where It Fails (HTML/JS/URL/CSS Contexts)
14. Bypassing WAFs and Filters (Encoding Tricks, Polyglots)
15. Content-Security-Policy Bypass Techniques
16. Clickjacking and Frame-Busting Defenses

## Request Forgery and Session Attacks
17. CSRF – Token Implementation and Bypass Scenarios
18. CSRF vs SameSite Cookies as Defense-in-Depth
19. Session Fixation and Session Hijacking
20. Session Prediction and Insecure Token Generation
21. Insecure Direct Object References (IDOR)
22. Cross-Origin Resource Sharing (CORS) Misconfigurations

## Authentication and Access Control
23. Password Attacks (Brute Force, Credential Stuffing, Password Spraying)
24. Weak Password Hashing Exploitation (MD5/SHA1 vs bcrypt/Argon2id)
25. Multi-Factor Authentication Bypass Techniques
26. Broken Access Control and Privilege Escalation
27. JWT Vulnerabilities (Algorithm Confusion, Weak Secrets, `none` Algorithm)
28. OAuth2 Flow Abuse (Redirect URI Manipulation, Token Leakage)
29. API Key and Secrets Exposure in Client-Side Code

## File Handling and Upload Attacks
30. Local File Inclusion (LFI) and Path Traversal
31. Remote File Inclusion (RFI)
32. Malicious File Upload Bypass (MIME Spoofing, Double Extensions, Null Byte Tricks)
33. Web Shell Deployment via Upload Vulnerabilities
34. Insecure Deserialization Leading to RCE

## Server and Infrastructure-Level Attacks
35. Server-Side Request Forgery (SSRF)
36. HTTP Request Smuggling
37. HTTP Parameter Pollution
38. Security Misconfiguration (Default Credentials, Debug Mode in Production, Verbose Errors)
39. Missing/Misconfigured Security Headers (HSTS, X-Frame-Options, X-Content-Type-Options)
40. Subdomain Takeover and DNS Misconfigurations

## API and Modern Architecture Security
41. RESTful API Testing Methodology (Endpoint Enumeration, Method Fuzzing)
42. Broken Object Level Authorization (BOLA) in APIs
43. GraphQL Security Testing (Introspection Abuse, Query Depth/Batching Attacks)
44. Rate Limiting and Brute-Force Protections on Login/Reset Endpoints
45. Mass Assignment Vulnerabilities
46. Business Logic Flaws (Race Conditions, Workflow Bypass)

## Dependency, Supply Chain, and Code-Level Risks
47. Composer Dependency Vulnerabilities (`composer audit`, Known CVEs)
48. Outdated PHP Version and Extension Exploits
49. Static Analysis for Vulnerability Discovery (PHPStan/Psalm Security Rules)
50. Reviewing PHP Source Code for Injection Points (Manual Code Review Techniques)

## Exploitation Chaining and Reporting
51. Chaining Vulnerabilities for Full Compromise (e.g., XSS → CSRF → Account Takeover)
52. Privilege Escalation Post-Exploitation on the Web Server
53. Writing a Professional Penetration Test Report (Findings, CVSS Scoring, Remediation Guidance)

---

A note on sequencing: I put **Injection** and **XSS/Client-Side** first since they build most directly on the PHP superglobals and output-encoding fundamentals you already covered. **Auth/Access Control** and **File Handling** come next since they assume familiarity with sessions and file uploads from fundamentals. **API/Modern Architecture** and **Supply Chain** are placed later since they're more specialized and often optional depending on whether your course targets classic web apps, modern API-driven apps, or both — happy to split those into an optional track if you'd rather keep the core advanced module tighter.
