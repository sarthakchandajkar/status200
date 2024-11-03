---
title: Module 2
aliases:
  - "AZ-104: Manage identities and governance in Azure"
draft: false
tags:
  - AZ-104
  - Cloud
  - Microsoft
author:
  - Sarthak Chandajkar
---
# Microsoft Active Directory Domain Services (AD DS)

- directory service that provides the methods for storing directory data, such as user accounts and passwords.
- makes this data available to network users, administrators, and other devices and services.
- runs as a service on Windows Server, referred to as a domain controller.

# Microsoft Entra ID

- PaaS
- helps in providing secure access to cloud based resources for individuals/organizations by:
	- Configuring access to applications
	- Configuring single sign-on (SSO) to cloud-based SaaS applications
	- Managing users and groups
	- Provisioning users
	- Enabling federation between organizations
	- Providing an identity management solution
	- Identifying irregular sign-in activity
	- Configuring multi-factor authentication
	- Extending existing on-premises Active Directory implementations to Microsoft Entra ID
	- Configuring Application Proxy for cloud and local applications
	- Configuring Conditional Access for users and devices

![[Pasted image 20241031144415.png]]

## Microsoft Entra Tenants

- multi tenant by design
- ensure isolation between its individual directory instances
- one Azure subscription associated to one MS Entra tenant.
- grant permissions to resources in Azure Subscriptions via [[RBAC]]
- assigned default Domain Name System (DNS) with a unique prefix.

> [!NOTE]
> You can associate the same Microsoft Entra tenant with multiple Azure subscriptions. This allows you to use the same users, groups, and applications to manage resources across multiple Azure subscriptions.

## Microsoft Entra Schema

- fewer objects than AD DS
- no definition of the computer class
- Does have a device class
- Does not include the [[Organizational Unit (OU)]] class

## Microsoft Entra ID vs Microsoft Active Directory Doman Services

| <font color="#92cddc">**Feature**</font> | <font color="#92cddc">**Active Directory Domain Services (AD DS)**</font>                                          | <font color="#92cddc">**Microsoft Entra ID**</font>                                                           |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------- |
| **Primary Purpose**                      | Directory service                                                                                                  | Identity solution for internet-based applications                                                             |
| **Structure**                            | Hierarchical, X.500-based                                                                                          | Flat structure, multi-tenant                                                                                  |
| **Protocols for Queries**                | [[Lightweight Delivery Access Protocol (LDAP)]]                                                                    | REST API over HTTP and HTTPS                                                                                  |
| **Authentication Protocol**              | [[Kerberos]]                                                                                                       | [[SAML]], [[WS-Federation]], [[OpenID Connect]] and [[OAuth]]                                                 |
| **Network Protocols**                    | Primarily [[DNS]]                                                                                                  | HTTP (port 80) and HTTPS (port 443)                                                                           |
| **Management Units**                     | [[Organizational Unit (OU)]] and [[Group Policy Objects (GPOs)]]                                                   | None (flat structure with no OUs or GPOs)                                                                     |
| **Trust Relationships**                  | Supports trusts between domains for delegated management                                                           | Federated with third-party services (e.g., Facebook)                                                          |
| **Deployment Flexibility**               | Can be deployed on Azure VMs for scalability and availability, but this does not integrate with Microsoft Entra ID | Designed specifically for cloud applications; not equivalent to deploying an Active Directory domain on Azure |
| **Computer Objects**                     | Includes computer objects for devices joined to the AD DS domain                                                   | No computer objects                                                                                           |

> [!NOTE] Note
> Deploying AD DS on an Azure virtual machine requires one or more extra Azure data disks because you shouldn't use drive C for AD DS storage. These disks are needed to store the AD DS database, logs, and the sysvol folder. The Host Cache Preference setting for these disks must be set to None.

## Compare Microsoft Entra ID P1 and P2 plans (Tentative)

| **<font color="#92cddc">Feature</font>** | <font color="#92cddc">**Microsoft Entra ID P1**</font>                                  | <font color="#92cddc">**Microsoft Entra ID P2**</font>                                                                                             |
| ---------------------------------------- | --------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Self-service Group Management**        | Available                                                                               | Available                                                                                                                                          |
| **Advanced Security Reports & Alerts**   | Available, with machine learning-based insights                                         | Available                                                                                                                                          |
| **Multi-factor Authentication (MFA)**    | Available, works with on-premises applications and Microsoft cloud services             | Available                                                                                                                                          |
| **Microsoft Identity Manager (MIM)**     | Licensing included, integrates for hybrid identity solutions                            | Licensing included                                                                                                                                 |
| **Service Level Agreement (SLA)**        | 99.9% availability                                                                      | 99.9% availability                                                                                                                                 |
| **Password Reset with Writeback**        | Available, follows AD on-premises password policy                                       | Available                                                                                                                                          |
| **Cloud App Discovery**                  | Available, helps discover frequently used cloud applications                            | Available                                                                                                                                          |
| **Conditional Access**                   | Available, based on device, group, or location                                          | Available                                                                                                                                          |
| **Microsoft Entra Connect Health**       | Available, provides insights on alerts, performance, usage patterns, and configurations | Available                                                                                                                                          |
| **Microsoft Entra ID Protection**        | Not included                                                                            | Included, offers user risk policies, sign-in policies, and behavioral monitoring                                                                   |
| **Privileged Identity Management (PIM)** | Not included                                                                            | Included, allows for secure management of privileged users, with workflows for temporary and permanent access configurations                       |
| **Primary Use Case**                     | Identity management with essential security and access management features              | Enhanced security and identity protection, particularly suitable for environments with sensitive or high-stakes administrative access requirements |
| **Trial Availability**                   | Available                                                                               | Available                                                                                                                                          |
| **Included with Microsoft EMS**          | Yes                                                                                     | Yes                                                                                                                                                |

## Microsoft Entra Domain Services

- provides domain services such as Group Policy management, domain joining, and Kerberos authentication to your Microsoft Entra tenant
- fully compatible with locally deployed AD DS
- use them without deploying and managing additional domain controllers in the cloud
- utilize organizational credentials in both on-premises AD DS and in Microsoft Entra Domain Services
- migrate applications that use LDAP, NTLM, or the Kerberos protocols from your on-premises infrastructure to the cloud

![[Pasted image 20241101191507.png]]

### Benefits

- no need to manage, update and monitor domain controllers
- no need to deploy and manage Active Directory replication
- no need to have Domain Admins or Enterprise Admins groups for domains that Entra ID manages

### Limitations

- Only the base computer Active Directory object is supported.
- It’s not possible to extend the schema for the Microsoft Entra Domain Services domain.
- The organizational unit (OU) structure is flat and nested OUs aren't currently supported.
- There’s a built-in Group Policy Object (GPO), and it exists for computer and user accounts.
- It’s not possible to target OUs with built-in GPOs. Additionally, you can't use Windows Management Instrumentation filters or security-group filtering.

--- 
# Configure Users and Group Accounts

### User Accounts supported by Entra ID

| <font color="#92cddc">User account</font> | <font color="#92cddc">Description</font>                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Cloud identity**                        | A user account with a _cloud identity_ is defined only in Microsoft Entra ID. This type of user account includes administrator accounts and users who are managed as part of your organization. A cloud identity can be for user accounts defined in your Microsoft Entra organization, and also for user accounts defined in an external Microsoft Entra instance. When a cloud identity is removed from the primary directory, the user account is deleted. |
| **Directory-synchronized identity**       | User accounts that have a _directory-synchronized identity_ are defined in an on-premises Active Directory. A synchronization activity occurs via Microsoft Entra Connect to bring these user accounts in to Azure. The source for these accounts is Windows Server Active Directory.                                                                                                                                                                         |
| **Guest user**                            | _Guest user_ accounts are defined outside Azure. Examples include user accounts from other cloud providers, and Microsoft accounts like an Xbox LIVE account. The source for guest user accounts is Invited user. Guest user accounts are useful when external vendors or contractors need access to your Azure resources.                                                                                                                                    |

### When choosing user accounts:
- Consider where users are defined
- Consider support for external contributors
- Consider a combination of user accounts

### Manage user accounts

- Az portal
- Microsoft 365 Admin Center
- Microsoft Intune admin console
- Azure CLI

## Create Bulk user accounts

- Only Global administrators or User administrators have privileges to create and delete user accounts in the Azure portal.
- To complete bulk create or delete operations, the admin fills out a comma-separated values (CSV) template of the data for the user accounts.
- Bulk operation templates can be downloaded from the <span style="background:#ff4d4f">Microsoft Entra admin center</span>.
- Bulk lists of user accounts can be downloaded.

###  Things to consider when creating user accounts

- **Consider naming conventions**
- **Consider using initial passwords**
- **Consider strategies for minimizing errors**

## Create Group Accounts

- Security Groups: manage member and computer access to shared resources for a group of users
- **Microsoft 365 groups**: provide collaboration opportunities. Group members have access to a shared mailbox, calendar, files, SharePoint site, and more

### Things to consider when adding group members

| <font color="#92cddc">Access rights</font> | <font color="#92cddc">Description</font>                                                                                                                                                                                                                                                                                                                                                                                  |
| ------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Assigned**                               | Add specific users as members of a group, where each user can have unique permissions.                                                                                                                                                                                                                                                                                                       |
| **Dynamic user**                           | Use dynamic membership rules to automatically add and remove group members. When member attributes change, Azure reviews the dynamic group rules for the directory. If the member attributes meet the rule requirements, the member is added to the group. If the member attributes no longer meet the rule requirements, the member is removed.                                             |
| **Dynamic device**                         | (_Security groups only_) Apply dynamic group rules to automatically add and remove devices in security groups. When device attributes change, Azure reviews the dynamic group rules for the directory. If the device attributes meet the rule requirements, the device is added to the security group. If the device attributes no longer meet the rule requirements, the device is removed. |

## Create administrative units

- restrict administrative scope

### Things to consider when working with administrative units

- **Consider management tools**
- **Consider role requirements in the Azure portal**
- **Consider scope of administrative units**
