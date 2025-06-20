# Class 12: Windows User and Computer Management

## Overview

This class covers the fundamentals of local user and computer management in Windows. It introduces the Microsoft Management Console (MMC) and its key snap-ins and provides a detailed practical guide to managing local user accounts, groups, and permissions.

## 1. Theory: Windows Management Tools

### Microsoft Management Console (MMC)

MMC is a framework that provides a common user interface for performing system administration tasks. It hosts management tools called "snap-ins".

#### Computer Management (`compmgmt.msc`)

This is a pre-built console that gathers several administrative snap-ins in one place.
* **Shortcut**: Press `Win + X`, then `G`, or type `compmgmt.msc` in the Run dialog.

Key snap-ins within Computer Management include:

* **Task Scheduler**: Schedule automated tasks to run at specific times or in response to events (e.g., running backups, system updates).
* **Event Viewer**: View logs about program, security, and system events on your Windows PC. Essential for troubleshooting.
* **Local Users and Groups**: Manage user accounts and groups that are stored locally on the machine.

---

## 2. Practical: Local User Management

### Windows Account Types

#### 1. Built-in Administrator Account

* **Characteristics**: Has the highest level of privileges and a SID ending in 500. It cannot be deleted, only disabled, and is not affected by User Account Control (UAC) by default.
* **Best Practice**: This account should be renamed and kept disabled for security. Use separate, regular admin accounts for daily administrative tasks.

#### 2. Regular Administrator Accounts

* **Capabilities**: Can create and manage other users, install software, change system-wide settings, and access all files.
* **Limitations**: Subject to UAC prompts, which require explicit approval for tasks that need elevated privileges.

#### 3. Power Users

* **Capabilities**: A legacy group providing some administrative capabilities, like installing certain user-specific applications, but cannot modify system-wide settings or manage other users.

#### 4. Standard Users

* **Capabilities**: Can run installed applications and change their own user settings and password. They cannot install most software or make system-wide changes.
* **Recommendation**: This is the recommended account type for daily computer use to enhance security.

#### 5. Guest Account

* **Characteristics**: Has extremely limited rights and is disabled by default for security reasons. It should remain disabled in most cases.

#### 6. Service Accounts

* **Purpose**: Special accounts used to run Windows services.
* **Types**:
    * **Local Service**: Minimal privileges on the local system.
    * **Network Service**: More privileges than Local Service; acts as the computer on the network.
    * **System (Local System)**: Highest level of privilege, used by the OS itself. Should not be used for regular services.

### Practical Exercises

#### Exercise 1: Manage Built-in Accounts

1.  Open Computer Management (`compmgmt.msc`).
2.  Navigate to `System Tools > Local Users and Groups`.
3.  **Secure the Administrator**: Right-click the `Administrator` account, choose `Rename`, and give it a non-obvious name. Right-click again, go to `Properties`, and check `Account is disabled`.
4.  **Secure the Guest Account**: Ensure the `Guest` account is also disabled.

#### Exercise 2: Create a New Administrative User

1.  In `Local Users and Groups`, right-click the `Users` folder and select `New User...`.
2.  Fill in the user details and create a strong password.
3.  Right-click the newly created user, go to `Properties`, click the `Member Of` tab.
4.  Click `Add...`, type `Administrators`, and click `OK` to add the user to the Administrators group.

#### Exercise 3: Create a Service Account

1.  Create a new local user as in the previous exercise.
2.  In the user's properties, it's best practice to check `User cannot change password` and `Password never expires`.
3.  Use the Local Security Policy (`secpol.msc`) to grant this account specific rights, like "Log on as a service".

