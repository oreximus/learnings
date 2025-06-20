# Class 12: Linux Fundamentals

## Theory Section

### Linux History and Development

- **Developer**: Linus Torvalds
- **Year**: 1991
- **Original Purpose**: Personal project to create a free operating system kernel
- **Inspiration**: UNIX operating system
- **License**: GNU General Public License (GPL)

### What is a Shell?

- **Literal Meaning**: Outer layer of something
- **Technical Meaning**: Interface between user and kernel
- **Function**: Interprets user commands and communicates with the kernel
- **Role**: Kernel operates hardware, shell provides user interaction

```
User → Shell → Kernel → Hardware
     ←       ←        ←
```

### Linux Features and Advantages

#### 1. Open Source (GPL License)

- **Source Code**: Freely available for viewing and modification
- **Community Development**: Thousands of developers worldwide
- **No Licensing Costs**: Free to use, distribute, and modify
- **Transparency**: Security through visibility

#### 2. Multitasking

- **Definition**: Ability to run multiple processes simultaneously
- **Process Management**: Efficient CPU time sharing
- **Background Processes**: Services and daemons
- **Process Isolation**: Processes don't interfere with each other

#### 3. Multiuser

- **Concurrent Users**: Multiple users can access system simultaneously
- **User Isolation**: Each user has separate environment
- **Permission System**: Fine-grained access control
- **Resource Sharing**: Efficient use of system resources

#### 4. Portability

- **Hardware Independence**: Runs on various architectures
- **Supported Platforms**: x86, ARM, PowerPC, SPARC, etc.
- **Embedded Systems**: From smartphones to supercomputers
- **Cross-Platform**: Applications can be ported easily

#### 5. Security

- **Open Source Advantage**: Vulnerabilities found and patched quickly
- **Permission Model**: Strong user and file permissions
- **No Single Point of Failure**: Distributed development model
- **Regular Updates**: Frequent security patches

#### 6. Stability and Reliability

- **Uptime**: Systems can run for months/years without restart
- **Memory Management**: Efficient memory usage and protection
- **Error Handling**: Robust error recovery mechanisms
- **Process Isolation**: One process crash doesn't affect others

#### 7. Community Support

- **Documentation**: Extensive online documentation
- **Forums**: Active community forums and mailing lists
- **Professional Support**: Commercial support available
- **Learning Resources**: Tutorials, books, courses

#### 8. Performance

- **Resource Efficiency**: Maximum utilization of hardware
- **Customization**: Remove unnecessary components
- **Optimization**: Kernel can be optimized for specific use cases
- **Scalability**: From embedded devices to supercomputers

#### 9. Unix Compatibility

- **POSIX Compliance**: Follows UNIX standards
- **Command Compatibility**: Similar commands and utilities
- **Shell Scripts**: Portable across UNIX-like systems
- **Development Tools**: Standard UNIX development environment

## Practical Section

### Basic Linux Concepts

#### File System Hierarchy

```
/           # Root directory
/bin        # Essential user binaries
/boot       # Boot loader files
/dev        # Device files
/etc        # Configuration files
/home       # User home directories
/lib        # Essential shared libraries
/opt        # Optional software packages
/proc       # Process information
/root       # Root user home directory
/sbin       # Essential system binaries
/tmp        # Temporary files
/usr        # User programs and data
/var        # Variable data files
```

#### User Types

- **Root User**: Superuser with unlimited privileges
- **System Users**: Used by system services and daemons
- **Regular Users**: Normal user accounts with limited privileges

#### Permission System

```
rwxrwxrwx
|||||||└── Others execute
||||||└─── Others write
|||||└──── Others read
||||└───── Group execute
|||└────── Group write
||└─────── Group read
|└──────── Owner execute
└───────── Owner write
           Owner read
```

### Getting Started with Linux

#### Common Commands Introduction

```bash
ls          # List directory contents
cd          # Change directory
pwd         # Print working directory
mkdir       # Create directory
rmdir       # Remove directory
cp          # Copy files/directories
mv          # Move/rename files/directories
rm          # Remove files/directories
cat         # Display file contents
less        # View file contents page by page
grep        # Search text patterns
find        # Find files and directories
```

#### System Information Commands

```bash
uname -a    # System information
whoami      # Current username
id          # User and group IDs
ps          # Running processes
top         # System resource usage
df          # Disk space usage
free        # Memory usage
```

## Study Questions

1. What are the main advantages of Linux over proprietary operating systems?
2. How does the shell interact with the kernel?
3. What makes Linux suitable for both desktop and server environments?
4. Why is Linux considered more secure than some other operating systems?

## Next Class Preview

- Linux distributions and package management
- Debian vs Red Hat families
- Package managers and software installation
