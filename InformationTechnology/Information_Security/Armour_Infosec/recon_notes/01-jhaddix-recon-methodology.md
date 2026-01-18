# Notes
![[Pasted image 20260119043921.png]]

![[Pasted image 20260119043959.png]]

- Jason usually color code according to where he is in the recon process:
  - orange: currently working on
  - green: things which are completed

### Mission

- Wide Recon is the art of discovering as many assets related to a target
  as possible. Make sure your scope permits testing these sites: 1. Scope Domains 2. Acquisitions 3. ASN Enumeration 4. Reverse WHOIS 5. Subdomain Enumeration 6. Port Analysis 7. Other: - Vulns: - Subdomain Takeover - Buckets - Github leaks - Automation/Helper - Interlace - Screenshotting - Frameworks

![[Pasted image 20260119044029.png]]

## Finding Seeds/Roots

### Checking the Scope Domains:

**Scope Domains (Bugcrowd)**:

![[Pasted image 20260119044101.png]]

> Verizon Media: really supports bug hunting related things a lot. Worth checking
> out for the beginners.
![[Pasted image 20260119044120.png]]

### Acquisitions (Crunchbase)

- Using the crunchbase which is a business intelligence portal.

![[Pasted image 20260119044143.png]]

![[Pasted image 20260119044203.png]]

> Understand what is okay and what is not okay to hack!

### ASN Enumeration (bgp.he.net)

![[Pasted image 20260119044238.png]]
- Autonomous System Numbers are given to large enough networks. These
  ASN's will help us track down some semblance of an entity's IT
  infrastructure. The most reliable way to get these is manually through
  Hurricane Electric's free-form search: - http://bgp.he.net

- Because of the advent of cloud infrastructure, ASNs aren't always
  a complete picture of a network. Rogue assets could exists on cloud
  environments like AWS and Azure. Here we can see several IP ranges.

> jhaddix use the http://bgp.he.net when he does manually searching
> for ASNs.

> He recommend both scripted way to do it and manual way to perform
> the Enumeration based on the requirement and the need of the information
> that you're looking for

### ASN Enumeration (cmd line)

![[Pasted image 20260119044319.png]]

> jhaddix suggests two tools for ASN enumeration:

    1. metabigor: by j3ssiejjj which will fetch ASN data from a keyword from

bgp.he.net and asnlookup.com 2. anslookup: by Yassine Aboukir which utilizes the maxmind.com dataset.

> One problem with these tools is they are giving you the data based on the
> keyword or string that you're providing them (i.e. "Tesla") and there could
> be multiple companies or organizations which goes by the same name, and could
> possibly provide you some extra or different organizations ASNs information.
> So make sure that data is related to what you're looking for.

### ASN Enumeration (with Amass)

![[Pasted image 20260119044344.png]]

- for discovering more seed domains we want to scan the whole ASN with a port
  scanner and return any root domains we see in SSL certificates, etc.

- We can do this with Amass intel

- Amass is written by Jeff Foley and the Amass team.

> checkout the author amass workshop, to learn how to use it at the best.

- basic command:

```
amass intel -asn <asn-number>
```

### Reverse WHOIS (with Whoxy.com)

![[Pasted image 20260119044412.png]]

- Every website has some registeration info on file with the registrars. Two
  key pieces of data we can use are Organization name and any emails in the
  WHOIS data. To do this you need access to a large WHOIS database. WHOXY.com
  is one such database.

- You can use whoxy.com in this fashion, after you register and your free API key:
  - http://api.whoxy.com/?key=APIKeyHERE&reverse=whois&name=Twitch+Hostmaster

- Careful with reverse whois data as it is the least high fidelity source of new
  root/seed domains. It might include many parked domains or redirects to out of
  scope assets.

> Looking out for the domain related data from the whois lookup, looking throughout
> the changed domains and all.

### Reverse WHOIS (with DOMLink)

![[Pasted image 20260119044443.png]]

- DOMLink is a tool written by Vincent Yiu (@vysecurity) which will recursively query
  the WHOXY WHOIS API. It will start by querying our targets WHOIS record, then analyze
  all the data and look for the other records which contain the organization name or are
  registered to emails in the record. It does this recursively until it finds no more
  records of match.

### Ad/Analytics Relationships (builtwith.com)

![[Pasted image 20260119044529.png]]

- You can also glean related domains and subdomains by looking at a target's ad/analytics
  tracker codes. Many sites use the same codes across all their domains. Google analytics and
  New Relic codes are the most common. We can look at these "relationships" via a site called
  BuiltWith. BuiltWith also has a Chrome and Firefox extension to do this on the fly.

      - https://builtwith.com/relationships/twitch.tv

- BuiltWith is also a tool we'll use to profile the technology stack of a target in later
  slides.

img

### Ad/Analytics Relationships (getrelationships.py)

- for command-line information

![[Pasted image 20260119044550.png]]

### Google-Fu

- You can Google the:
  - Copyright text
  - Terms of service text
  - Privacy Policy text

- from a main target to glean related hosts on Google.

![[Pasted image 20260119044621.png]]

### Shodan

![[Pasted image 20260119044703.png]]

- Shodan is a tool that continuously spiders infrastructure on the internet. It is much
  more verbose than regular spiders. It captures `response data`, `cert data`, `stack profiling
data`, and more. It requires registeration.

> according to jhaddix the Shodan is basically a website which hosts information from an
> infrastructure based spider.

## Finding Subdomains

![[Pasted image 20260119044718.png]]

### Subdomain Enumeration:

- Subdomain Enumeration:
  - Linked and JS Discovery
  - Subdomain Scraping
  - Subdomain Bruteforce

### Linked and JS Discovery

- Another way to do widen our scope is to examine all the links or our main target. We can do this
  using Burp Suite Pro.

- We can visit a seed/root and recursively spider all the links for a team with regex, examining those
  links... and their links, and so on... until we have found all sites that could be in our scope.

- This is a hybrid technique that will find both roots/seeds and subdomains.

Things to setup:

1. Turn off passive scanning
2. Set forms auto to submit (If you're feeling frisky)
3. Set scpe to advanced control and use "keyword" of a target name (not a normal FQDN)
4. Walk+browse main site, then spider all hosts recursively!
5. Profit

### Linked Discovery (with Burp Suite Pro)

![[Pasted image 20260119044808.png]]

- setting up a rule from the `target` tab.
  - then `scope` tab.
    - use advanced scope control (in host or IP range)
      - enter the keyword like ("twitch")
  - then in the Site map
    - filter by request type:
      - show only in-scope items

- Selecting all of the filtered links and spider them via burpsuite.
  - and everything in the white are the new stuffs.

![[Pasted image 20260119044825.png]]

![[Pasted image 20260119044845.png]]

- Exporting the fetched data/information from the burpsuite:
  - Select all hosts in the site tree
  - In PRO ONLY right clic the selected hosts
  - Go to "Engagement Tools" -> "Analyze target"
  - Save report as an html file
  - Copy the hosts from the "Target" section

![[Pasted image 20260119044904.png]]
### Linked Discovery (with GoSpider or hakrawler)

- Linked discovery really just counts on using a spider recursively.

- One of the most extensible spiders for general automation is **GoSpider**
  written by **j3ssiejjj** which can be used for many things and supports
  parsing js very well.

- In addition **hakrawler** by **hakluke** has any parsing strategies that
  interest bug hunters.

### Subdomain Enumeration (with SubDomainizer)

- **Subdomainizer** by Neeraj Edwards is a tool with three purposes in
  **analyzing javascript**. It will take a page and run 1. Find subdomains referenced in js files 2. Find cloud services referenced in js files 3. Use the **Shannon Entropy** formula to find potentially sensitive
  items in js files

- It will take a **single page** and scan for js files to analyze.

_If just looking for subdomains ***subscraper*** by Cillian-Collins
might be better because it has recursion_.

![[Pasted image 20260119045054.png]]

### Subdomain Scraping

#### Subdomain Scraping Sources:

- The next set of tools scrape domain information from all sorts of projects that
  expose databases of URLs or domains.
  - Infrastructure Sources:
    - censys
    - robtex!
    - wayback machine
    - dnsdumpster.com
    - netcraft
    - PTRarchive.com
    - PASSIVE TOTAL
  - Certificate Sources:
    - crt.sh
    - certificate search
    - sslmate cert spotter
    - certDB
  - Security Sources:
    - hacker target
    - security trails
    - f-secure riddler
  - Search Engines
    - Google
    - Baidu
    - Bing
    - Ask.com
    - dogpile

- New sources are coming out all the time so the tools must evolve constantly.

![[Pasted image 20260119045010.png]]
