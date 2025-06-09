# Class 21-II: Windows Host File

## Overview
This class explains the purpose and usage of the hosts file in Windows.

## Hosts File
- **Location**: `C:\Windows\System32\drivers\etc\hosts`
- **Purpose**: Maps hostnames to IP addresses locally, bypassing DNS.
- **Access**: Requires administrator privileges to edit.
- **Usage**:
  - **Website Blocking**:
    ```text
    0.0.0.0 facebook.com www.facebook.com
    ```
  - **Custom Mapping**: Redirect domains to specific IPs (e.g., for testing).
- **Risk**: Misconfiguration can lead to DNS poisoning attacks.

## Corrections
- Clarified the risk of DNS poisoning.
- Added example for custom mapping.