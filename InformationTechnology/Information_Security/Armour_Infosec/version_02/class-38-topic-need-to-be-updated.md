# Class 01

## Topic: NATTING

> `Switch`: holds CAN(Content Addressable Memory) memory.

- First the request is made from the internal device from the WAN. (REQUEST)

- In the NAT table the record will entered and the private IP of the internal device
  will get converted into the public IP. - With the Private IP and the port used by the client from the internal device packet.

- And the response from the server will get the public IP of the client from the WAN with
  having the details of the IP and the Port Information, so that response from the server will
  reach back to the WAN with that Public IP.

- from the NAT table it will then send the response from the server to the Private IP of the device
  with the already containing port in the table which was sent back then in the requested packet.

#### NATTING FLOW IN THE NUTSHELL

1. Request from the device: Packet sent to NAT router
2. NAT Translation: Source IP/port replaced with public IP/Port
3. Response from the server
4. NAT reverse translation
5. Packet delivered inside

## Topic Port Forwarding

- It's like reverse work of the NATTING

- Port forwarding used to manage the external traffic coming from the internet in the internal LAN devices.

- Port forwarding configuration for internal LAN devices:
  - setting the Public IP and it's defined Port, for handling that defined Port traffic on the Private IP for
    that defied or maybe same port.

- Some port that bydefault disabled by our ISPs:
  - HTTP: 80
  - HTTPS: 443
  - FTP: 23
  - Xbox Live:
