# Class 13: Linux Distributions and Package Managers

## Overview

This class explores the concept of a Linux distribution (distro) and highlights the two major families of distributions: Debian-based and Red Hat-based.

## What is a Linux Distribution?

A Linux distribution is an operating system made from a software collection that is based upon the Linux kernel. It typically includes the kernel, a package management system, and a curated selection of software.

### 1. Debian-Based Distributions

* **Debian**: One of the oldest and most influential open-source projects, first developed in 1993. It is known for its stability and commitment to free software.
    * **Package Manager**: Uses `dpkg` and front-ends like `apt` (Advanced Package Tool).
    * **Package Format**: `.deb` packages.
    * **Availability**: A minimal "net-install" version contains only core packages, allowing users to build up their system.

* **Associated Distributions**:
    * **Ubuntu**: Developed in 2004, Ubuntu is the most popular desktop Linux distribution. It is based on Debian and focuses on usability and ease of installation. Its first version was targeted as a replacement for Windows XP.
    * **Kali Linux**: A Debian-derived distribution designed for digital forensics and penetration testing.

### 2. Red Hat-Based Distributions

* **Red Hat Enterprise Linux (RHEL)**: A commercial distribution developed by Red Hat, first released in 1993. It is widely used in corporate and server environments due to its stability and long-term support.
    * **Package Manager**: Uses `rpm` and front-ends like `yum` (Yellowdog Updater, Modified) and its successor, `dnf` (Dandified YUM).
    * **Package Format**: `.rpm` packages.

* **Associated Distributions**:
    * **Fedora**: A community-driven distribution sponsored by Red Hat. It serves as an upstream source and testing ground for RHEL, featuring cutting-edge software and new technologies.
    * **CentOS (Community ENTerprise Operating System)**: Historically, CentOS was a free, community-supported version of RHEL. It aimed to be functionally compatible with its upstream source. As of CentOS Stream, its role has shifted to be a rolling-release version that sits between Fedora and RHEL.

