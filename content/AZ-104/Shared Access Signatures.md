---
title: Shared Access Signatures
aliases:
  - Shared Access Signatures
draft: false
tags:
  - AZ-104
  - Cloud
author:
  - Sarthak Chandajkar
---
# What are Shared Access Signatures?
- URI: Uniform resource identifier.
- grants access rights to Azure Storage Services.
- helps sharing resources without compromising account keys.
- granular control over type of access.(Read/Write/Delete)
- account-level SAS can delegate access to multiple Azure Storage services.
- time interval of validity can be specified

# Types of SAS
- **Account level SAS**: delegates access to resources in one or more Azure Storage services.
- **Service level SAS**: - delegates access to a resource in only one Azure Storage service.


> [!NOTE] Stored Access Policy
> SAPs can be used to group SAS and other restrictions. Helpful when using a service-level SAS on the server side.

# Settings in SAS:
- **Signing method**: Choose the signing method: Account key or User delegation key.
- **Signing key**: Select the signing key from your list of keys.
- **Permissions**: Select the permissions granted by the SAS, such as read or write.
- **Start and Expiry date/time**: Specify the time interval for which the SAS is valid. Set the start time and the expiry time.
- **Allowed IP addresses**: (Optional) Identify an IP address or range of IP addresses from which Azure Storage accepts the SAS.
- **Allowed protocols**: (Optional) Select the protocol over which Azure Storage accepts the SAS.



