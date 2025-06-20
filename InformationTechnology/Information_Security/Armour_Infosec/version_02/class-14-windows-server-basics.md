# Class 14: Windows Server Management Fundamentals

## Theory Section

### Windows Server Management Tools

#### Computer Management Console (MMC)

- **Access Methods**:
  - Windows + X, then press 'G'
  - Run dialog: `compmgmt.msc`
  - Control Panel → Administrative Tools

#### System Tools in Computer Management

##### Task Scheduler

- **Purpose**: Schedule automated tasks
- **Common Uses**:
  - System updates
  - Backup operations
  - Maintenance scripts
  - User environment changes (night mode, etc.)
- **Task Types**:
  - Time-based triggers
  - Event-based triggers
  - System startup/shutdown triggers
- **Location**: Task Scheduler Library contains all scheduled tasks

##### Event Viewer

- **Purpose**: View system logs and events
- **Log Categories**:
  - Application Logs
  - Security Logs
  - System Logs
  - Setup Logs
  - Forwarded Events
- **Event Types**:
  - Information
  - Warning
  - Error
  - Critical
  - Success Audit
  - Failure Audit

## Practical Section

### Windows Server Roles and Features

#### Common Server Roles

- **Active Directory Domain Services**: Directory services
- **DNS Server**: Domain name resolution
- **DHCP Server**: IP address assignment
- **Web Server (IIS)**: Web hosting
- **File and Storage Services**: File sharing
- **Print and Document Services**: Print management

#### Common Features

- **Windows PowerShell**: Command-line management
- **Remote Server Administration Tools**: Remote management
- **Windows Backup**: System backup and recovery
- **Failover Clustering**: High availability

### Task Scheduler Configuration

#### Creating Basic Tasks

1. **Open Task Scheduler**

   ```
   taskschd.msc
   ```

2. **Create Basic Task**

   - Action: Create Basic Task
   - Name: System Cleanup
   - Trigger: Daily at 2:00 AM
   - Action: Start a program
   - Program: cleanmgr.exe

3. **View Scheduled Tasks**
   - Navigate to Task Scheduler Library
   - Review existing system tasks
   - Check task history and status

### Event Viewer Analysis

#### Analyzing System Events

1. **Open Event Viewer**

   ```
   eventvwr.msc
   ```

2. **Review Event Logs**

   - Windows Logs → System
   - Look for recent errors or warnings
   - Check Application logs for software issues
   - Review Security logs for authentication events

3. **Create Custom Views**
   - Filter events by level (Error, Warning)
   - Filter by time range
   - Filter by event source

### Windows File System Structure

#### Viewing Hidden Files and Folders

To see the actual Windows file structure:

1. **File Explorer Options**:
   - View → Options → Change folder and search options
   - View tab → Show hidden files, folders, and drives
   - Uncheck "Hide protected operating system files"

#### Root Drive (C:) Structure

##### Program Files

- **Purpose**: Contains installed programs and applications
- **Architecture**: Default folder for 64-bit applications
- **Location**: C:\Program Files\
- **Permissions**: Requires administrator rights to modify

##### Program Files (x86)

- **Purpose**: Contains 32-bit applications on 64-bit systems
- **Compatibility**: Maintains separation between 32-bit and 64-bit programs
- **Location**: C:\Program Files (x86)\
- **Legacy Support**: Ensures older applications work correctly

##### ProgramData

- **Purpose**: Application data shared across all users
- **Visibility**: Hidden by default
- **Usage**: Configuration files, shared databases, logs
- **Access**: All users can access, but modification may require privileges

##### Users

- **Purpose**: Contains user profiles and personal folders
- **Structure**: Each user has a separate folder
- **Contents**: Desktop, Documents, Downloads, Pictures, etc.
- **Profile Types**: Local profiles, roaming profiles, mandatory profiles

##### Windows

- **Purpose**: Core Windows operating system files
- **Critical Subfolders**:
  - **System32**: Essential system files and executables
  - **WinSxS**: Windows Side-by-Side store (component store)
  - **Temp**: Temporary files used by Windows
  - **Logs**: System and application log files

##### Other Important Folders

- **Recovery**: System recovery tools and files
- **System Volume Information**: System restore points and indexing
- **Recycle Bin**: Deleted files storage (hidden)
- **PerfLogs**: Performance monitoring logs
- **pagefile.sys**: Virtual memory file
- **swapfile.sys**: Modern apps virtual memory
- **hiberfil.sys**: Hibernation file

## Study Questions

1. What is the purpose of separating Program Files and Program Files (x86)?
2. How can Task Scheduler help in system administration?
3. What information can Event Viewer provide for troubleshooting?
4. Why are some Windows folders hidden by default?

## Next Class Preview

- Windows Server roles and features
- Service management and configuration
- Server administration tools
- Remote management capabilities
