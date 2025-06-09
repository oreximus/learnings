# Class 10: MAC Address

## Overview
This class covers the Media Access Control (MAC) address, its structure, and its uses.

## MAC Address Definition
- **Definition**: A unique 48-bit identifier assigned to network interfaces during manufacturing.
- **Purpose**: Identifies devices at the Data Link Layer (Layer 2) of the OSI model.

## Characteristics
- **Format**: 48 bits, represented as 12 hexadecimal digits (e.g., 00:A0:C9:12:34:56).
- **Representations**:
  - Colon-separated: 00:A0:C9:12:34:56
  - Dash-separated: 00-A0-C9-12-34-56
  - No separation: 00A0C9123456
- **Structure**:
  - **OUI (Organizationally Unique Identifier)**: First 24 bits, assigned by IEEE to manufacturers.
  - **Unique Identifier**: Last 24 bits, assigned by the manufacturer.
- **Example OUI Range**:
  - Smallest: 00:A0:C9:00:00:00
  - Largest: 00:A0:C9:FF:FF:FF

## Types of MAC Addresses
- **Unicast**: Targets a single device.
- **Multicast**: Targets a group of devices.
- **Broadcast**: Targets all devices in the network (FF:FF:FF:FF:FF:FF).

## Features
- **Static Assignment**: Burned into the NIC during manufacturing.
- **MAC Spoofing**: Possible to change MAC addresses for testing or bypassing restrictions.
- **Wake-on-LAN**: Some NICs support remote power-up via MAC address.

## Connectors
- **RJ45**: Used for Ethernet connections in PCs.
- **RJ11**: Used for telephone lines.

## Corrections
- Clarified the OUI range and MAC address types.
- Added details on MAC spoofing and Wake-on-LAN.