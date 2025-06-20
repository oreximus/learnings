# Class 09: Network Topologies

## Overview

This class explores different network topologies, which describe the arrangement of devices and links in a network.

## Topologies by Generation

### Line Topology

* **Description**: Devices are connected in a linear series, one after the other.
* **Data Transfer**: Data flows through every device between the source and destination.
* **Security**: Data is not secure, as every intermediate device can see the data passing through it.
* **Usage**: Not in practical use for modern computer networks.

### Bus Topology

* **Description**: All devices are connected to a single common communication line called a bus.
* **Data Transfer**: Data sent by a device travels along the entire bus and is seen by all devices, but only the intended recipient accepts and processes it.
* **Failure**: If the main bus cable fails, the entire network goes down. However, if a single device fails, the rest of the network remains operational.

### Ring Topology

* **Description**: All devices are connected in a circular, ring-like manner. Each device is connected to exactly two other devices.
* **Data Transfer**: Data travels in one direction around the ring until it reaches its destination.

### Star Topology

* **Description**: All devices are connected to a central hub or switch. This is the most common topology in modern LANs.
* **Data Transfer**: Devices communicate by sending data to the central hub, which then forwards it to the destination device.
* **Failure**: If the central hub fails, the entire network fails. If a single device or its cable fails, only that device is affected.

### Mesh Topology

* **Description**: A network setup where devices are interconnected with many redundant interconnections between network nodes. It can be a combination of other topologies.
    * **Full Mesh**: Every device is connected to every other device. Highly reliable but expensive.
    * **Partial Mesh**: Some devices are connected to all others, but some are only connected to nodes with which they exchange the most data.

### Fully Connected Topology

* **Description**: All devices are connected to a single device and share data through it.
* (Note: This seems to be a description of a Star Topology or a misunderstanding. A fully connected topology is typically a full mesh.)

