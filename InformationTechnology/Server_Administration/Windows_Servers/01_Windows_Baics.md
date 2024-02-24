# Windows Fundamentals

### Source of Notes: HTB Academy; Windows Fundamentals Module

- Microsoft first introduced the Windows Operating System on November 20, 1985.

- The first version of Windows was a graphical operating system shell for MS-DOS. Later versions of Windows Desktop introduced the Windows File Manager, and Print Manager programs.

- Windows 95 was the first full integration of Windows and DOS and offered built-in internet support for the first time. This version also debuted the Internet Explorer web browser. Since the initial version, there have been over a dozen versions of Windows released, such as Windows XP, Vista, and 8, up to the current version: Windows 10.

- Windows Server was first released in 1993 with the release of Windows NT 3.1 Advanced Server. Windows NT saw several updates over the years, adding in technologies such as Internet Information Services (IIS), various networking protocols, Administrative Wizards to facilitate admin tasks, and more.

- With the release of Windows 2000, Microsoft debuted Active Directory, originally intended to help sysadmins set up file sharing, data encryption, VPNs, etc.

- Windows Server 2000 also included the Microsoft Management Console(MMC) and supported dynamic disk volumes.

- Windows Server 2003 came next with sever roles, a built-in firewall the Volume Shadow Copy Service, and more. Windows Server 2008 included failover clustering, Hyper-V virtualization software, Server Core, Event Viewer, and major enhancements to Active Directory.

- Over the years, Microsoft released further Server versions, including Server 2012, Server 2016, and most recently, Server 2019. This latest version added support for Kubernetes, Linux containers and more advanced security features.

- As new versions of Windows are introduced, older versions are deprecated and no longer receive Microsoft updates (unless a long-term support contract is purchased in some cases). Windows Server 2008 and 2012 reached end of life for security updates on January 14, 2020. Currently, only Server 2012 R2 and later are in support.

- However, Microsoft has released out-of-band patches for earlier versions of Windows in the past few years due to the discovery of critical SMBv1 vulnerability (EternalBlue).

### Windows Versions:

| **Operating Systems Names** | **Version Numbers** |
|-----------------------------|---------------------|
| Windows NT 4 | 4.0 |
| Windows 2000 | 5.0 |
| Windows XP | 5.1 |
| Windows Server 2003, 2003 R2 | 5.2 |
| Windows Vista, Server 2008 | 6.0 |
| Windows 7, Server 2008 R2 | 6.1 |
| Windows 8, Server 2012 | 6.2 |
| Windows 8.1, Server 2012 R2 | 6.3 |
| Windows 10, Server 2016, Server 2019 | 10.0 |

- We can use the **Get-WmiObject cmdlet** to find information about the operating sytem.

- This cmdlet can be used to getr instances of WMI classes or information about the available WMI classes. There are a variety of ways to find the version and build number of our system. We can easily obtain this information using the **win32_OperatingSystem** class, which shows that we are on a Windows 10 host, build number 19041.

```
Get-WmiObject -Class win32_OperatingSystem | select Version, BuildNumber
```

- Above command will output the Build Number and Version of the Current Operating System.

- Some other useful classes that can be used with **Get-WmiObject** are **Win32_Process** to get a process listing, **Win32_Service** to get a listing of services, and **Win32_Bios** to get **Basic Input/Output System (BIOS)** information.

- The BIOS is firmware installed on a computer's motherboard that controls the computer's essential functions, such as power management, input/output interfaces, and system configuration. We can use the **ComputerName** parameter to get information about remote computers.

- **Get-WmiObject** can be used to start and stop services on local and remote computers, and more.

### Accessing Windows

**Local Access Concepts**

- Local access is the most common way to access any computer, including computer running Windows, **Input** is likely happening through a keyboard, trackpad, trackpad &/or mouse. **Output** is coming from the display screen(s).

**Remote Access Concepts**

- Remote Access is accessing a computer over a network. Local access to a computer is needed before one can access another computer remotely. There are countless methods for remote access.

- Consider **MSPs** & **MSSPs**, both industries are primarily dependent on managing their client's computer systems remotely. This functionality allow them to centralize management, standardize what technologies are used, automate numerous tasks, enable remote work arrangements and allow for quick response time when issues surface, or potential security threats emerge.

- Organizations with IT, Software Development &/or Security teams use remote access methods daily to build applications, manage servers and administer employee workstations. Some of the most common remote access technologies include but aren't limited to:

    - Virtual Private Network (VPN)
    - Secure Shell (SSH)
    - File Transfer Protocol (FTP)
    - Virtual Network Computing (VNC)
    - Windows Remote Management (or PowerShell Remoting) (WinRM)
    - Remote Desktop Protocol (RDP)

**Remote Desktop Protocol (RDP)**

- RDP uses a client/server architecture where a client-side application is used to specify a computer's target IP address or hostname over a network where RDP access is enabled. The target computer where RDP remote access is enabled is considered the server.

- The target computer where RDP remote access is enabled is considered the server. RDP listens by default on logical port 3389.

- Keep in mind that an IP address is used as a logical identifier for a computer on a network, and a logical port is an identifier assigned to an application.

- In simpler terms, we could consider a network subnet a street in a town (the corporate network), an IP address in that subnet assigned to a host as a house on that street, and logical ports as windows/doors that can be used to access the house.

- Once a require (encapsulated inside a packet) has reached a destination computer via its IP address, the request will be directed to an application hosted on the computer based on the port specified in that request (included as a header inside a packet).

- IP addressing and protocol encapsulation are covered in greater detail in the module **Introduction to Networking**. From a networking perspective.
