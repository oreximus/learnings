# Class 13: Linux Distributions and Package Management

## Theory Section

### Distribution Families

#### 1. Debian-Based Distributions

##### Debian

- **Founded**: 1993
- **Philosophy**: Commitment to free and open-source software
- **Package Format**: .deb (Debian package)
- **Package Manager**: APT (Advanced Package Tool)
- **Release Model**: Stable, Testing, Unstable branches
- **Characteristics**:
  - Extremely stable
  - Extensive package repository
  - Strong community governance
  - Available in compact form with core packages only

##### Ubuntu

- **Founded**: 2004 by Canonical Ltd.
- **Based On**: Debian
- **Original Target**: Replace Windows XP on desktop
- **Versions**:
  - Desktop Edition
  - Server Edition
  - LTS (Long Term Support) - 5 years support
- **Release Cycle**: Every 6 months, LTS every 2 years
- **Package Management**: APT with Ubuntu-specific tools

#### 2. Red Hat Enterprise Linux (RHEL) Family

##### Red Hat Enterprise Linux (RHEL)

- **Founded**: 1993
- **Target Market**: Enterprise customers
- **Support Model**: Commercial support and certification
- **Package Format**: .rpm (Red Hat Package Manager)
- **Package Manager**: YUM (Yellowdog Updater Modified) / DNF (Dandified YUM)

##### Fedora

- **Purpose**: Community-driven testing ground for RHEL
- **Release Cycle**: Every 6 months
- **Characteristics**:
  - Cutting-edge software
  - Latest kernel and technologies
  - Short support lifecycle (13 months)
  - Innovation platform

##### CentOS (Community Enterprise Operating System)

- **Purpose**: Free, community-supported version of RHEL
- **Compatibility**: Binary compatible with RHEL
- **Support**: Community-based support
- **Usage**: Popular for servers and development environments
- **Note**: CentOS Stream is now the upstream for RHEL

## Practical Section

### Package Management Commands

#### Debian/Ubuntu (APT)

```bash
sudo apt update                    # Update package database
sudo apt upgrade                   # Upgrade all packages
sudo apt install package-name     # Install specific package
sudo apt remove package-name      # Remove package
sudo apt purge package-name       # Remove package and config files
sudo apt autoremove               # Remove unused dependencies
sudo apt search keyword           # Search for packages
apt list --installed              # List installed packages
```

#### RHEL/CentOS/Fedora (YUM/DNF)

```bash
sudo yum update                    # Update all packages (older systems)
sudo dnf update                    # Update all packages (newer systems)
sudo yum install package-name     # Install package
sudo yum remove package-name      # Remove package
sudo yum search keyword           # Search packages
yum list installed                # List installed packages
sudo yum groupinstall "Group Name" # Install package groups
```

### Other Notable Distributions

#### SUSE Linux

- **SUSE Linux Enterprise**: Commercial distribution
- **openSUSE**: Community version
- **Package Manager**: Zypper
- **Unique Features**: YaST configuration tool

#### Arch Linux

- **Philosophy**: Simplicity and user control
- **Package Manager**: Pacman
- **Characteristics**: Rolling release, minimal base system

#### Gentoo

- **Philosophy**: Source-based distribution
- **Package Manager**: Portage
- **Characteristics**: Compile from source, highly customizable

### Distribution Selection Guide

#### For Beginners

- **Ubuntu**: User-friendly, extensive documentation
- **Linux Mint**: Windows-like interface, based on Ubuntu
- **Fedora**: Modern features, good hardware support

#### For Servers

- **CentOS/RHEL**: Enterprise stability, long support
- **Ubuntu Server**: Easy management, cloud integration
- **Debian**: Rock-solid stability, minimal resource usage

#### For Advanced Users

- **Arch Linux**: Complete control, rolling release
- **Gentoo**: Source-based, maximum optimization
- **Slackware**: Traditional UNIX-like experience

### Package Management Comparison

#### APT (Debian/Ubuntu)

```bash
# Update package database
sudo apt update

# Search for package
apt search apache2

# Install package
sudo apt install apache2

# Remove package
sudo apt remove apache2

# Show package information
apt show apache2
```

#### YUM/DNF (RHEL/CentOS/Fedora)

```bash
# Update package database
sudo dnf update

# Search for package
dnf search httpd

# Install package
sudo dnf install httpd

# Remove package
sudo dnf remove httpd

# Show package information
dnf info httpd
```

## Study Questions

1. What are the main differences between Debian-based and Red Hat-based distributions?
2. How do package managers differ between Linux distributions?
3. What factors should you consider when choosing a Linux distribution?
4. Why do different distributions use different package formats?

## Next Class Preview

- Windows Server fundamentals
- Computer Management tools
- Windows services and administration
