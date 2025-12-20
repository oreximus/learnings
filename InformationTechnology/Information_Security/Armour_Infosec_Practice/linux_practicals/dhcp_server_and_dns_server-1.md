# Notes

## source: perplexity.ai: https://www.perplexity.ai/search/provide-the-instructions-to-co-jpditXguS7e.h2qSTdmZXg#0

## DHCP Server

- installing the required packages:

```
yum install dhcp-server
```

- now configuring the `/etc/dhcp/dhcpd.conf`:

```
option domain-name "example.local";
option domain-name-servers your.dns.ip;
default-lease-time 600;
max-lease-time 7200;
authoritative;
subnet 192.168.1.0 netmask 255.255.255.0 {
  range dynamic-bootp 192.168.1.200 192.168.1.254;
  option broadcast-address 192.168.1.255;
  option routers 192.168.1.1;
}
```
