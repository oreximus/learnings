# Notes

## Static IP Settings:

- edit the file in the CentOS `/etc/sysconfig/network-scripts/ifcfg-interface_name`:

```
sudo vim /etc/sysconfig/network-scripts/ifcfg-interface_name
```

- with the following details:

```
TYPE="Ethernet"
**BOOTPROTO="none"**
**ONBOOT="yes"**
**IPADDR="192.168.1.10"**
**PREFIX="24"**
**GATEWAY="192.168.1.1"**
**DNS1="8.8.8.8"**
**DNS2="8.8.4.4"**
NAME="interface_name"
DEVICE="interface_name"
```

- and then restart the NetworkManger:

```
sudo systemctl restart NetworkManger
```

-
