---
title: Virtual Network Peering
aliases:
  - Virtual Network Peering
draft: false
tags:
  - AZ-104
author:
  - Sarthak Chandajkar
---
 ![[Virtual Network Peering.png]]
 
# What is Virtual Network Peering?

- **Virtual Network Peering** allows you to connect to different virtual networks in the same or different regions.
- There are two types of VNet Peerings:
	- **Regional virtual network peering**: Connect Virtual Networks in the same region.
	- **Global virtual network peering**:Connect Virtual Networks in different regions.
- Azure Virtual Network Peering offers private network connections ensuring secure transfers. 
- Traffic between the VMs in the Virtual Networks are routed via the Microsoft Backbone Architecture.
- [[Azure VPN Gateway]] can be configured in the peered Virtual Networks as a transit point.
- A minimum of two Virtual Networks are required for peering.
- The second virtual network in the peering is referred to as the _remote network_.
- The Virtual Network Peering is considered to be successful when the status is **Connected**


> [!Warning] Overlapping CIDR Blocks
> Two virtual networks with overlapping **CIDR** blocks cannot be directly peered.

# Key Features of Virtual Network Peering

- Private Network Connections
- Strong Performance
- Simplified Communication
- Seamless Data Transfer
- No Resource Disruptions/Downtime.