## Ippsec Walkthrough of HTB Machines

# Monitors Two

- Starting from the NMAP
```
nmap -sC -sV -oA output_location ip
```

- ssh and http ports are available

- a login to cacti found! (on web, http)

- cacti version is vulnerable, going the description of the exploit.

**About CVE**

- This module exploit an unauthenticated command injection vulnerability in Cacti through 1.2.22 (CVE-20220-46169) in order to achieve unauthenticated remote code execution as the www-data user. 

- The module first attempth to obtaion the Cacti version to see if the target is affected. If LOCAL_DATA_ID and/ or HOST_ID are not set, the module will try to bruteforce the missing value(s). If a valid combination is found, the module will use these to attempt exploitation.

- During exploitation, the module sends a GET request to /remote_agent.php with the action parameter set to polldata and the X-Forwarded-For header set to the provided value for X_FORWARDED_FOR_IP (by default 127.0.0.1). In addition, the poller_id parameter is set to the payload and the host_id and local_id parameters are set to the bruteforced or provided values.
