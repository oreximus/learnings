# Class 04: IANA and IP Management

## Overview
This class discusses the role of the Internet Assigned Numbers Authority (IANA) and IP address management, including public and private IPs.

## IANA Responsibilities
- **IP Address Management**: Allocates IP address blocks to Regional Internet Registries (RIRs).
- **DNS Management**: Oversees the root zone of the DNS.
- **Protocol Assignment**: Manages protocol numbers and ports.

## IP Distribution
- **From IANA to GOI (Gateway of India)**: IANA allocates IP blocks to RIRs (e.g., APNIC for Asia-Pacific), which distribute to ISPs (T1).
- **From GOI to Country ISPs**: ISPs like BSNL or Jio receive IP blocks for national distribution (T2).
- **From ISPs to Cities**: Local ISPs distribute IPs to cities (e.g., Indore) (T3).
- **Submarine Cables**: Physical infrastructure connecting global networks to India.

## Public vs. Private IP
- **Public IP**: Assigned by ISPs, routable on the internet.
- **Private IP**: Used within private networks, not routable on the internet.
  - **Purpose**: Conserves IPv4 addresses by allowing reuse in private networks.
  - **Ranges**:
    - Class A: 10.0.0.0 to 10.255.255.255 (/8)
    - Class B: 172.16.0.0 to 172.31.255.255 (/12)
    - Class C: 192.168.0.0 to 192.168.255.255 (/16)
    - Special Range: 100.64.0.0 to 100.127.255.255 (/10, for CGNAT)
  - **Loopback Address**: 127.0.0.0 to 127.255.255.255 (used for local testing).

## IP Conflicts
- **Issue**: Duplicate IPs in the same network cause communication failures.
- **Solution**: Ensure unique IP assignments within the same network.

## Corrections
- Corrected the Class B private IP range (originally listed as 175.16.0.0 to 10.255, which is incorrect).
- Clarified the role of submarine cables in global IP distribution.