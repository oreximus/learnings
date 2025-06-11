# DNS Server Practical Notes:

## Secondary Server Setup:

**Initial Setup**

- Installing one extra server, besides your primary server:
  - configure the name (i.e. ns2)
  - configure the domain (i.e. armour.local)
  - configure the static IP for the secondary server

**Installing the DNS server**:

- Installing the DNS from the roles and features.

**Configuring the Secondary DNS Server from ns2 server from it's zone**

- setting up the

![dns_img02](../../../assets/images/dns_img02.png)

- setting our master DNS server IP here:
  ![dns_img03](../../../assets/images/dns_img03.png)

- for zone transferring create a A Record in your Primary DNS Server:

![dns_img04](../../../assets/images/dns_img04.png)

- add the IP for zone transfer from your master DNS Server:

![dns_img05](../../../assets/images/dns_img05.png)

- ensure you've this setting in the Zone Transfer Tab:

![dns_img06](../../../assets/images/dns_img06.png)

- for AXFR zone transfer from the master dns server to the secondary dns server.
  ![dns_img07](../../../assets/images/dns_img07.png)

- and after completion of the AXFR zone transferrring, you'll see the records:

![dns_img08](../../../assets/images/dns_img08.png)

![dns_img09](../../../assets/images/dns_img09.png)

![dns_img10](../../../assets/images/dns_img10.png)

**For checking the AXFR Zone Transferring through Wireshark**:

**filter**:

```
ip.addr == 192.168.2.10 && tcp.port == 53 || udp.port == 53
```


