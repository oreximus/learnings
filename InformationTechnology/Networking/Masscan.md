# Masscan

- can be used for Internal Pentesting

- for example, we can check if any webserver is available in the network.

### Some Info:

- it can upto 25 million packets/seconds.

### Example Commands

1.
```
masscan -p80,443,445 <ip-address/range> -oG output_name.txt --rate=100000
```
