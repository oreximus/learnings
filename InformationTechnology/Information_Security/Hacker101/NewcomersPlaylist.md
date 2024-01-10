# Newcomers Playlist Notes

### Source: https://www.hacker101.com/playlists/newcomers

## Introduction - By Cody Brocious

### Tools Required:

- Burp proxy
- Firefox

### Finding Vulnerabilities

- Try to find-out every functionality of the applications, and think about what
  could possibly go wrong with them?

- Then prioritize the function to compromize according to the value they
  provide.

- Understand the developer pain side in the application deployment. Which can
  provide the Idea for where to look.

### Severity

- `Informational`: Issue has no real impact
- `Low`: The business impact is minimal
- `Medium`: Potential to cause harm to users, but not revealing data
- `High`: Potential to reveal user data or aids in exploitation of other
  vulnerabilities.
- `Critical`: High risk of personal/confidential data exposure, general system
  compromise, and other severe impacts to the business.

## The Web In Depth

### Requests

**Basic Format of Web Request**:

```
VERB /resource/locator HTTP/1.1
Header1: Value1
Header2: Value2

...
<body of the request>
```

### Request Headers

- **Host**: Indicates the desired host handling the request
- **Accept**: Indicates what MIME type(s) are accepted by the client; often used
  to specify JSON or XML output for web-services
- **Cookie**: Passes cookie data to the server
- **Referer**: Page leading to this request (note: this is not passed to other
  servers when using HTTPS on the origin)
- **Authorization**: Used for 'basic auth' pages (mainly). Takes the form "Basic
  <base64'd username:password>"

### Cookies

- Key-value
- Fixed-Period
- Domain Pattern
- Comes from the server or added by the javascript
- If you are able to set cookies on the domains where you're not supposed that's
  also a breach of security.

### Cookies Security

- Cookies added for .example.com can be read by any subdomain of example.com
- Cookies added for a subdomain can only be read in that subdomain and its
  subdomains
- A subdomain can set cookies for its own subdomains and parent, but it can't
  set cookies for siblings domains
  - E.g. test.example.com can't set cookies on test2.example.com, can't set
    cookies on test2.example.com, but can set them on example.com and
    foo.test.example.com

- There are two important flags to know for cookies:

  - Secure: The cookie will only be accessible to HTTPS pages
  - HTTPOnly: The cookie cannot be read by Javascript

- The server indicates these flags in the Set-Cookie header that passed them in
  the first place.

### HTML

#### Parsing

- HTML should be parsed according to the relevant spec, generally HTML5 now.

- But when you're talking about security, it's often not just parsed by your
  browser, but also Web-Application Firewalls and other filters.

- Wherever there's a discrepancy in how these two items parse things, there's
  probably a vulnerability.

#### Canonical Example

- You go to http://example.com/vulnerable?
  `name=<script/xss%20src=http://evilsite.com/my.js`> and it generates:

```
<!doctype html><html>
    <head>
        <title>Vulnerable page name <script/xss src=http://evilsite.com/my.js></title>
    </head>
</html>
```

- A bad XSS filter on the web application may not see that as a scipt tag due to
  it being a 'script/xss' tag. But Firefox's HTML parser, for instance, will
  treat the slash as whitespace, enabling the attack!

#### Legacy Parsing

- Due to decades of bad HTML, browsers are quite excellent at cleaning up after
  authors, and these conditions are often exploitable.

  - <script> tag on its own will automatically be closed at the end of the page.
  - A tag missing its closing angle bracket will automatically be closed by the
    angle bracket of the next tag on the page.

### Content Sniffing

#### MIME Sniffing

not very relevant these days but was a security issue at some time.

- The browser will often not just look

## Todos

- Take a look at request library in Python, practice some example scripts!

- Playaround with Cookies, practice the hierarchical scenarios and test to
  manipulate the cookies.

- Also try to go further in any topic to find out if there is anything more you
  should know.
