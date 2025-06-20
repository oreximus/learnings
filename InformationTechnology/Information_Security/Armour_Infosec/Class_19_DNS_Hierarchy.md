# Class 19: The Domain Name System (DNS) Hierarchy

## Overview

This class provides a detailed breakdown of the Domain Name System's hierarchical structure, explaining how domain names are organized from the root down to subdomains.

## The DNS Hierarchy

DNS uses a hierarchical, tree-like structure to organize domain names. This structure is read from right to left, with the rightmost part being the highest level in the hierarchy.

**Full Domain Anatomy**: `subdomain.second-level-domain.top-level-domain.root`

**Example**: `www.google.com.`
* `.` (implicit): The Root Domain.
* `com`: The Top-Level Domain (TLD).
* `google`: The Second-Level Domain (SLD).
* `www`: The Subdomain (or hostname).

### 1. The Root Domain (`.`)

* The highest level in the DNS hierarchy.
* It is represented by a single dot (`.`) but is usually implied and not typed in web browsers.
* The root zone is managed by IANA and contains information about the authoritative servers for all TLDs.

### 2. Top-Level Domains (TLDs)

TLDs are the part of the domain name located to the right of the dot (e.g., `com` in `example.com`).

#### Types of TLDs

* **Generic TLDs (gTLDs)**: Used for general purposes.
    * **Unsponsored/Open**: `.com` (commercial), `.org` (organization), `.net` (network), `.info`.
    * **Restricted/Sponsored (sTLDs)**: Managed by specific agencies with eligibility rules. Examples include `.gov` (US government), `.edu` (educational institutions), `.mil` (US military).
* **Country-Code TLDs (ccTLDs)**: Two-letter codes for specific countries or territories, such as `.in` (India), `.us` (United States), `.uk` (United Kingdom).
* **Infrastructure TLD**: `.arpa` is used for internet infrastructure purposes.
* **New gTLDs**: Since 2012, hundreds of new TLDs have been introduced (e.g., `.tech`, `.blog`, `.google`).

### 3. Second-Level Domains (SLDs)

* The part of the domain name located directly to the left of the TLD.
* This is the "identity" part of the domain that individuals and organizations register (e.g., `google` in `google.com`).
* The SLD must be unique within its specific TLD.

### 4. Subdomains

* An additional level of the domain created to the left of the SLD, used to organize a site's content or services.
* The domain owner can create unlimited subdomains.
* Common examples:
    * `www`: for a website.
    * `blog`: for a blog section.
    * `mail`: for an email service.
    * `api`: for an Application Programming Interface.

