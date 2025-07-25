---
title: Module 4
aliases:
  - Module 4
draft: false
tags:
  - AZ-104
  - Cloud
author:
  - Sarthak Chandajkar
---
# AZ-104: Deploy and manage Azure compute resources

- [[Virtual Machines]]
- Purge Protection

## Availability Sets

When you host your virtual machines in Azure, you sometimes need to cater to the following

1. An unplanned event wherein the underlying infrastructure fails unexpectedly. The failures could be attributed to network failures , local disk failures or even rack failures.
2. Planned maintenance events , wherein Microsoft needs to make planned updates to the underlying physical environment. In such cases , a reboot might be required on your virtual machine.
    
You can increase the availability of your application by making use of availability sets. Each virtual machine that is assigned to the availability set is assigned a separate fault and update domain.

- **Fault domains** are used to define the group of virtual machines that share a common source and network switch. You can have up to 3 fault domains.

- **Update domains** are used to group virtual machines and physical hardware that can be rebooted at the same time. You can have up to 20 update domains.


> [!NOTE] Azure Container Apps
> Currently Azure Container Apps supports only images based on the Linux operating system.you can deploy containers based on both Windows and Linux-based operating systems on Azure Container Instances.
