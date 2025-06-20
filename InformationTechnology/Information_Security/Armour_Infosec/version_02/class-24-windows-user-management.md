# Class 24: Windows User and Group Management

## Theory Section

### Windows User Account Types

#### Local User Accounts

- **Definition**: User accounts stored locally on the computer
- **Scope**: Access limited to the local computer
- **Management**: Managed through Local Users and Groups (lusrmgr.msc)
- **Usage**: Standalone computers, workgroup environments

#### Domain User Accounts

- **Definition**: User accounts stored in Active Directory
- **Scope**: Access across domain-joined computers
- **Management**: Managed through Active Directory Users and Computers
- **Usage**: Enterprise environments with centralized authentication

#### Built-in User Accounts

- **Administrator**: Full system access (disabled by default in newer Windows)
- **Guest**: Limited access for temporary users (disabled by default)
- **DefaultAccount**: System account for default apps (Windows 10/11)

### Windows Group Types

#### Local Groups

- **Definition**: Groups stored locally on the computer
- **Scope**: Permissions apply only to local computer
- **Examples**: Administrators, Users, Power Users

#### Domain Groups

- **Definition**: Groups stored in Active Directory
- **Scope**: Permissions can apply across domain
- **Types**: Security groups, Distribution groups

### Built-in Windows Groups

#### Administrators Group

- **Purpose**: Full control over the computer
- **Capabilities**:
  - Install/uninstall software
  - Modify system settings
  - Access all files and folders
  - Manage other user accounts
- **Security Risk**: Members have unrestricted access

#### Users Group

- **Purpose**: Standard user access
- **Capabilities**:
  - Run applications
  - Access own files and folders
  - Change own password
  - Limited system modifications
- **Security**: Restricted access to system resources

#### Power Users Group

- **Purpose**: Enhanced user privileges (legacy)
- **Status**: Deprecated in modern Windows versions
- **Replacement**: Use specific permissions instead

#### Backup Operators Group

- **Purpose**: Special Windows group with backup and restore privileges
- **Permissions**: Can backup and restore files regardless of file permissions
- **Usage**: Assigned to users who need to perform system backups
- **Security**: Members can bypass normal file security for backup purposes
- **Capabilities**:
  - Backup files and directories
  - Restore files and directories
  - Log on as a service
  - Shut down the system

## Practical Section

### User Account Management

#### Creating User Accounts

1. **Local Users and Groups (lusrmgr.msc)**:

   - Right-click Users → New User
   - Enter username, full name, description
   - Set password and password options
   - Configure account options

2. **Command Line (net user)**:

   ```cmd
   net user username password /add
   net user username /active:yes
   net user username /passwordchg:yes
   ```

3. **PowerShell**:
   ```powershell
   New-LocalUser -Name "username" -Password (ConvertTo-SecureString "password" -AsPlainText -Force)
   ```

#### Managing User Properties

- **Account Options**:
  - User must change password at next logon
  - User cannot change password
  - Password never expires
  - Account is disabled
- **Profile Settings**: Home folder, logon script, profile path
- **Group Membership**: Add/remove from groups

### Group Management

#### Creating and Managing Groups

1. **Local Users and Groups**:

   - Right-click Groups → New Group
   - Enter group name and description
   - Add members to group

2. **Command Line**:
   ```cmd
   net localgroup groupname /add
   net localgroup groupname username /add
   ```

#### Group Membership Management

```cmd
# Add user to group
net localgroup "Administrators" username /add

# Remove user from group
net localgroup "Administrators" username /delete

# View group members
net localgroup "Administrators"
```

### File and Folder Permissions

#### NTFS Permissions

- **Full Control**: Complete access including permission changes
- **Modify**: Read, write, delete files and subfolders
- **Read & Execute**: View and run files
- **Read**: View files and folder contents
- **Write**: Create new files and folders

#### Permission Inheritance

- **Inheritance**: Child objects inherit permissions from parent
- **Explicit Permissions**: Directly assigned permissions
- **Effective Permissions**: Combination of inherited and explicit permissions

### Shared Folders and Network Access

#### Creating Shared Folders

1. **File Explorer Method**:

   - Right-click folder → Properties → Sharing tab
   - Click "Advanced Sharing"
   - Check "Share this folder"
   - Set share name and permissions

2. **Computer Management**:
   - Computer Management → Shared Folders → Shares
   - Right-click → New Share
   - Follow Share a Folder Wizard

#### Share Permissions vs NTFS Permissions

- **Share Permissions**: Control network access to shared folder
- **NTFS Permissions**: Control local and network access to files/folders
- **Effective Access**: Most restrictive of share and NTFS permissions

### Public Directory and Shared Resources

#### Public Directory

- **Location**: C:\Users\Public
- **Purpose**: Contains files and data accessible by any user
- **Usage**: Shared documents, common applications, public downloads
- **Access**: All users have read/write access by default

#### Accessing Shared Folders

- **UNC Path**: \\computername\sharename or \\IPaddress\sharename
- **Run Dialog**: Windows + R, then enter \\192.168.2.21
- **File Explorer**: Network section or direct UNC path entry

### Remote Access Tools

#### Remote Desktop Connection (mstsc)

- **Access**: Run dialog → mstsc
- **Purpose**: Remote desktop connection to other Windows machines
- **Requirements**:
  - Remote Desktop enabled on target computer
  - User account with "Allow log on through Remote Desktop Services" right
  - Network connectivity between computers
- **Security**: Encrypted connection, authentication required

#### Remote Desktop Configuration

1. **Enable Remote Desktop**:

   - System Properties → Remote tab
   - Enable "Enable Remote Desktop on this computer"
   - Configure user access

2. **Firewall Configuration**:
   - Windows Firewall must allow Remote Desktop
   - Default port: 3389 (TCP)

### User Account Control (UAC)

#### UAC Purpose

- **Security**: Prevent unauthorized system changes
- **Elevation**: Prompt for administrator credentials when needed
- **Standard User**: Run with standard user privileges by default

#### UAC Levels

- **Always Notify**: Highest security, prompts for all changes
- **Default**: Notify when programs try to make changes
- **Notify without Dimming**: Less secure, no secure desktop
- **Never Notify**: Lowest security, no prompts

### Security Best Practices

#### Account Security

1. **Principle of Least Privilege**: Give users minimum necessary permissions
2. **Regular Password Changes**: Enforce password policies
3. **Account Monitoring**: Monitor for unusual account activity
4. **Disable Unused Accounts**: Remove or disable accounts no longer needed

#### Group Management

1. **Use Groups for Permissions**: Assign permissions to groups, not individual users
2. **Regular Review**: Periodically review group memberships
3. **Nested Groups**: Use group nesting carefully to avoid complexity
4. **Document Permissions**: Maintain documentation of group purposes and permissions

## Study Questions

1. What is the difference between local and domain user accounts?
2. How do share permissions and NTFS permissions work together?
3. What are the security implications of the Backup Operators group?
4. How does User Account Control enhance Windows security?

## Next Class Preview

- Course review and practical applications
- Real-world scenarios and troubleshooting
- Best practices for network and system administration
