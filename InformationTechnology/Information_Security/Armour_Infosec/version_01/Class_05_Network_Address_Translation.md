# Class 05: Network Address Translation (NAT)

## Overview

This class explains how devices in a private network can communicate with the public internet using Network Address Translation (NAT) and Port Forwarding. It also clarifies the difference between the Internet and an Intranet.

## How Private and Public IPs Work Together

Devices within a private network (e.g., a home or office) use private IP addresses. To access the internet, these private addresses must be translated into a single public IP address provided by the ISP. This process is called **NAT (Network Address Translation)**.

* **NATTING**: The router uses NAT to translate private IP addresses to its public IP address when sending requests to the internet, and vice-versa for incoming responses.

* **Port Forwarding**: When an external device on the internet needs to initiate a connection with a specific device inside the private network (like a web server), **Port Forwarding** is used. The router is configured to forward traffic arriving on a specific port to a designated private IP address.

## Communication Flow Example

1.  A device with a private IP (e.g., 192.168.1.10) wants to access `google.com`.
2.  The request goes to the local network's gateway (the router).
3.  The router, using NAT, replaces the private source IP (192.168.1.10) with its own public IP address and sends the request to the internet. It keeps a record of this translation.
4.  When `google.com` responds, it sends the data back to the router's public IP.
5.  The router checks its translation table and forwards the response to the correct internal device (192.168.1.10).

## Internet vs. Intranet

* **Internet**: The global, public network that is accessible to everyone.
* **Intranet**: A private, internal network belonging to an organization, accessible only by its members. Private networks are also known as intranets.

