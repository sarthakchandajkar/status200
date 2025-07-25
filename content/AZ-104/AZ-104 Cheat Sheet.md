---
title: AZ-104 Cheat Sheet
aliases:
  - AZ-104 Cheat Sheet
draft: false
tags:
  - AZ-104
author:
  - Sarthak Chandajkar
---
 
# Important points

- The Log Analytics workspace and the Recovery Services Vault don’t need to be in the same location when it comes to the storage of reports.
- The Recovery Services Vault and the Azure Storage Account need to be in the same region.
- When moving from Read-Access Geo-redundant storage to Zone-redundant storage, you first need to change the replication type to Locally-redundant storage.
- In a Sync Group, you can have only one cloud endpoint
- Virtual network and the Network Security Group need to be in the same region.
- For accessing the file share, port 445 needs to be open.
- nginx by default listens for HTTP requests on port 80
- When a new VM is created in Azure, a public address is assigned to it by default with the SKU type Standard
- Inbound NAT rules are used for port forwarding.
- When it comes to storage accounts , they need to be in the same location as the Azure Recovery Services vault. And when it comes to a Log Analytics workspace, they can be in any location.
- For each different location for the virtual machine, you need a separate Recovery services vault. The Recovery Services vault is location dependent.
- Disks with Azure Disk Encryption are not supported with Azure Backup vault.
- You can deploy containers based on both Windows and Linux-based operating systems on Azure Container Instances.
- Currently Azure Container Apps supports only images based on the Linux operating system.
- We need to have a rule in the NSG at both the subnet and network interface level to allow RDP traffic.
- Health Probe -> Load balancing Rule.
- For Traffic Analytics , we need to enable NSG flow logs.
- When enabling replication for objects, the source storage account must have the following requirements. It must be either a General Purpose V2 or a Premium Block Blob account , It must have versioning enabled, It must have change feed enabled
- A **read-only lock** restricts modifications to a resource but still allows read operations and certain administrative actions, such as moving the resource. This is because moving a resource in Azure does not inherently modify its configuration—it only updates its metadata to associate it with a different resource group.


# Final checks

- Storage account tier list and access levels
- File shares
- Container services
- Default Ports assignments
- Redundancy Tiers
- Purge Protection
- Same and different regions requirements.
- User Defined Routes
- Network Watcher
- Az copy
---
# Important Ports
- Azure Bastion: 443
- Azure File share: 445

--- 
# Revision

- Section Quizzes
- Practice Test 1 and 2
- Review topics of incorrect questions
- Breeze though slides
