# Notes

## source: perplexity.ai: https://www.perplexity.ai/search/provide-the-instructions-to-co-jpditXguS7e.h2qSTdmZXg#0

## DHCP Server

- installing the required packages:

```
yum install dhcp-server
```

- now configuring the `/etc/dhcp/dhcpd.conf`:

```
option domain-name "ai.local";
```

- and check the syntax of the configuration by this command:

```
sudo dhcpd -t -cf /etc/dhcp/dhpcd.conf
```

- example configuration:

```
option domain-name "ai.local";
option domain-name-servers 192.168.1.100;
default-lease-time 600;
max-lease-time 7200;
authoritative;
subnet 192.168.1.0 netmask 255.255.255.0 {
    range dynamic-bootp 192.168.1.200 192.1.254;
    option routers 192.168.1.1;
    option domain-name-servers 192.168.1.100;
}
```

## DNS Server:

- installing the required packages:

```
sudo dnf install bind bind-utils -y
```

-
