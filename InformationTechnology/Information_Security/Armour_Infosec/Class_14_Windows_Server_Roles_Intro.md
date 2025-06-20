# Class 14: Introduction to Windows Server Roles

## Overview

This class introduces the fundamental concepts of Roles and Features in Windows Server, which are the building blocks for customizing a server to perform specific functions.

## Server Manager

**Server Manager** is the central console in Windows Server used to install, manage, and remove server roles and features. It provides a dashboard to monitor the health and status of the server and any roles installed on it.

## Roles vs. Features

In Windows Server, functionality is organized into Roles and Features.

### Roles

* **Definition**: A server role is a primary function that a server is configured to perform. Roles are designed to provide services to clients or other devices on the network.
* **Purpose**: When you install a role, you are setting up the server to be a specific type of server. The role installation process adds the necessary services, components, and management tools.
* **Examples of Roles**:
    * **Active Directory Domain Services (AD DS)**: To create a domain controller.
    * **DHCP Server**: To automatically provide IP addresses to clients.
    * **DNS Server**: To perform name resolution.
    * **File and Storage Services**: To manage file shares and storage.
    * **Web Server (IIS)**: To host websites and web applications.
    * **Hyper-V**: To provide virtualization services.

### Features

* **Definition**: A feature is a software program that supports or augments the functionality of the server or its roles, but is not a primary function in itself.
* **Purpose**: Features provide additional capabilities that can be used by the server itself or by the roles installed on it.
* **Examples of Features**:
    * **.NET Framework**: A software framework required by many applications.
    * **BitLocker Drive Encryption**: To encrypt server volumes.
    * **Windows Server Backup**: To back up and restore the server.
    * **Telnet Client**: A tool for remote connectivity.
    * **Failover Clustering**: To create high-availability server clusters.

