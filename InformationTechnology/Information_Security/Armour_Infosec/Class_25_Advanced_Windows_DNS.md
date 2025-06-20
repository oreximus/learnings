# Class 25: Advanced Windows DNS Server Topics

## Overview

This class explores more advanced DNS server configurations in a Windows Server environment, including setting up a secondary DNS server for redundancy, configuring forwarders, and enabling dynamic DNS updates.

## 1. Secondary DNS Server

A secondary DNS server gets a read-only copy of a zone from a primary (master) server. This provides redundancy and load balancing.

#### Configuration

1.  On the **Primary Server**:
    * In the DNS zone's properties, go to the **Zone Transfers** tab.
    * Check "Allow zone transfers" and specify which servers are allowed to request a transfer (e.g., "Only to the following servers" and add the secondary server's IP).
2.  On the **Secondary Server**:
    * Install the DNS Server role.
    * In the DNS Manager, right-click "Forward Lookup Zones" and select "New Zone...".
    * Choose **Secondary zone**.
    * Enter the exact name of the zone you want to copy.
    * Enter the IP address of the primary (master) server.
    * The secondary server will now pull a copy of the zone from the primary.

#### Zone Transfers (IXFR/AXFR)

* When a record is updated on the primary server, its **Serial Number** in the SOA record increments.
* The secondary server periodically checks the primary's serial number. If it sees a higher number, it initiates a zone transfer to get the updates.
* **IXFR** (Incremental Zone Transfer): Transfers only the changes.
* **AXFR** (Full Zone Transfer): Transfers the entire zone.

**Testing Note**: By default, `nslookup` will query the primary DNS server listed in a client's configuration. To test a secondary server directly from a client, you can use `nslookup <domain> <secondary_dns_ip>`. The `ping` command, however, will use whichever DNS server the client is configured to use, which could be the secondary.

## 2. Forwarder and Conditional Forwarder

### Forwarder

* A **Forwarder** is a DNS server that a local DNS server forwards queries to when it cannot resolve them itself (i.e., for zones it is not authoritative for).
* Instead of performing the full recursive lookup process itself, the local server simply asks the forwarder (e.g., your ISP's DNS server or Google's `8.8.8.8`).
* **Configuration**: In DNS Manager, right-click the server, go to `Properties`, and use the `Forwarders` tab to add the IP addresses of the servers you want to forward queries to.

### Conditional Forwarder

* A **Conditional Forwarder** forwards queries for a *specific domain name* to a specific DNS server.
* **Example**: You can configure your server to forward all queries for `google.com` directly to `8.8.8.8`, while all other external queries go to a different forwarder or are resolved via recursion.
* **Configuration**: In DNS Manager, right-click "Conditional Forwarders" and select "New Conditional Forwarder...".

## 3. Dynamic DNS (DDNS)

* **Problem**: In a network where clients get their IP addresses from a DHCP server, a client's IP can change. This makes the static 'A' records in the DNS server incorrect.
* **Solution**: Dynamic DNS allows network clients to automatically register and update their DNS records with the DNS server whenever their IP address changes. This requires that the client has a fixed hostname.

#### Configuration

1.  **On the DNS Zone**:
    * In the zone's properties, on the `General` tab, set **Dynamic updates** to "Secure only" (recommended for Active Directory environments) or "Nonsecure and secure".
2.  **On the DHCP Scope**:
    * In the DHCP scope's properties, go to the `DNS` tab.
    * Configure the options to **Enable DNS dynamic updates** and have the DHCP server update records on behalf of the clients.
3.  **On the Client**:
    * In the advanced TCP/IP settings for the network adapter, on the `DNS` tab, ensure "Register this connection's addresses in DNS" is checked.

