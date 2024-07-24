# 40 Windows Commands you NEED to know

**source**: https://www.youtube.com/watch?v=Jfvg3CS1X3A&t=15s

## ipconfig

- ip info:

```
ipconfig
```

- all info through `ipconfig`:

```
ipconfig /all
```

- filtering in `ipconfig`:

```

// finding all info related to DNS
ipconfig /all | findstr DNS
```

- renewing ip address:

```
// first releasing the IP that we have!
ipconfig /release
```

```
// then we can renew it
// but remember it'll renew all of the interfaces!
ipconfig /renew
```

> if don't want to do that, you can also specify the
> interface.

- you can list all of the dns cache:

```
ipconfig /displaydns
```

- you can take backup of it:

```
ipconfig /displaydns | clip
```

- it'll copy all the output in the clipboard.

- for removing all of the DNS cache:

```
ipconfig /flushdns
```

## nslookup

- you can check what DNS server that you're using:

```
nslookup somewebsite.com
```

- we can also specify the other DNS server and get the
  output details it provides:

```
nslookup somewebsite.com 8.8.8.8
```

- we can also check the other types of record, i.e. MX,
  TXT, etc.

```
nslookup -type=TXT somewebsite.com

nslookup -type=ptr somewebsite.com
```

- clear your screen with `cls`.

## getmac

- getting your mac address:

```
getmac /V
```

## powercfg

- this command will provide the details about any energy
  related issue on your computer:

```
powercfg /energy
```

- also you can check your battery report:

```
powercfg /batteryreport
```

## assoc

- it tells you which filetype is associated with which
  program:

```
assoc
```

- we can also specify the program to use by the specific
  filetype:

```
assoc .mp4=VLC.vlc
```

## chkdsk

- checking if there is any errors in your disk and fix
  them:

```
chkdsk /f
```

- checking physical sector issues:

```
chkdsk /r
```

## sfc

- it'll check your windows system files, like windows .dll
  files and replace them if they are bad:

```
sfc /scannow
```

## DISM (Deployment Image Servicing and Management)

- commandline tools that will fix your system image:

- basic checkup:

```
DISM /Online /Cleanup-Image /CheckHealth
```

- go a bit deeper with a longer scan:

```
DISM /Online /Cleanup-Image /ScanHealth
```

- and if does comes up with some issues, then we can
  restore:

```
DISM /Online /Cleanup-Image /RestoreHealth
```

> you can try `sfc scannow` command once more to fix
> things again.

## tasklist

- we can find specific program PID by:

```
tasklist | findstr programName
```

- and killing the process by:

```
taskkill /f /pid PID
```

## netsh

- getting the detailed report of `wlan`:

```
netsh wlan show wlanreport
```

- and we can open the file!

- listing the interface details:

```
netsh interface show interface
```

- finding ip addresses:

```
netsh interface ip show address | findstr "IP Address"
```

- dnsserver details:

```
netsh interface ip show dnsservers
```

- turn-on and turn-off the Windows Defender Firewall:

```
// turn off
netsh advfirewall set allprofile state off

// turn on
netsh advfirewall set allprofile state on
```
