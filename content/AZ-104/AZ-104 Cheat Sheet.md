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
 

- The Log Analytics workspace and the Recovery Services Vault don’t need to be in the same location when it comes to the storage of reports.
- The Recovery Services Vault and the Azure Storage Account need to be in the same region.
- When moving from Read-Access Geo-redundant storage to Zone-redundant storage, you first need to change the replication type to Locally-redundant storage.
- In a Sync Group, you can have only one cloud endpoint
- Virtual network and the Network Security Group need to be in the same region.
- For accessing the file share, port 445 needs to be open.
- nginx by default listens for HTTP requests on port 80
- When a new VM is created in Azure, a public address is assigned to it by default with the SKU type Standard
- Inbound NAT rules are used for port forwarding.