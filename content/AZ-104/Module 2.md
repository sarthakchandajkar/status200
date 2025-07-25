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

![[MAAD.png]]

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

## Microsoft Entra ID vs Microsoft Active Directory Domain Services

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

![[AADS.png]]

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

| <font color="#92cddc">User account</font> | <font color="#92cddc">Description</font>                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Cloud identity**                        | A user account with a _cloud identity_ is defined only in Microsoft Entra ID. This type of user account includes administrator accounts and users who are managed as part of your organization. A cloud identity can be for user accounts defined in your Microsoft Entra organization, and also for user accounts defined in an external Microsoft Entra instance. When a cloud identity is removed from the primary directory, the user account is deleted. |
| **Directory-synchronized identity**       | User accounts that have a _directory-synchronized identity_ are defined in an on-premises Active Directory. A synchronization activity occurs via [[Microsoft Entra Connect]] to bring these user accounts in to Azure. The source for these accounts is Windows Server Active Directory.                                                                                                                                                                     |
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

![[Administrative Units.png]]
- restrict administrative scope

### Things to consider when working with administrative units

- **Consider management tools**
- **Consider role requirements in the Azure portal**
- **Consider scope of administrative units**

## Configure subscriptions

### Identify Azure Regions

- **Region**
	- geographical area on the planet containing at least one, but potentially multiple datacenters.
	- The datacenters are in close proximity and networked together with a low-latency network.
	- West US, Canada Central, West Europe, Australia East, and Japan West.
	- Azure is generally available in more than 60 regions in 140 countries
	- more global regions than any other cloud provider.
	- provide you with the flexibility and scale needed to bring applications closer to your users.
	- preserve data residency and offer comprehensive compliance and resiliency options for customers.

- **Regional Pairs**
	- Azure regions are paired with another region within the same geography to make a _regional pair_ (or _paired regions_).
	- support always-on availability of Azure resources used by your infrastructure.

| Characteristic                    | Description                                                                                                                                                                                                                                                                                                                |
| --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Physical isolation**            | Azure prefers at least 300 miles of separation between datacenters in a regional pair. This principle isn't practical or possible in all geographies. Physical datacenter separation reduces the likelihood of natural disasters, civil unrest, power outages, or physical network outages affecting both regions at once. |
| **Platform-provided replication** | Some services like Geo-Redundant Storage provide automatic replication to the paired region.                                                                                                                                                                                                                               |
| **Region recovery order**         | During a broad outage, recovery of one region is prioritized out of every pair. Applications that are deployed across paired regions are guaranteed to have one of the regions recovered with priority.                                                                                                                    |
| **Sequential updates**            | Planned Azure system updates are rolled out to paired regions sequentially (not at the same time). Rolling updates minimizes downtime, reduces bugs, and logical failures in the rare event of a bad update.                                                                                                               |
| **Data residency**                | Regions reside within the same geography as their enabled set (except for the Brazil South and Singapore regions).                                                                                                                                                                                                         |

### Things to consider when using regions and regional pairs

- **Consider resource and region deployment**.
- **Consider service support by region**
- **Consider services that don't require regions**
- **Consider exceptions to region pairing**
- **Consider benefits of data residency**

### Find regions for your business geography

- By Geography: Search [Azure regions](https://azure.microsoft.com/global-infrastructure/geographies/#geographies) by geography.|
- By product: Search [Azure products](https://azure.microsoft.com/global-infrastructure/services/) by region or geography.
- Paired regions: Search for [paired regions](https://learn.microsoft.com/en-us/azure/best-practices-availability-paired-regions#azure-cross-region-replication-pairings-for-all-geographies) and exceptions.

## Implement Azure Subscriptions

- Subscription: logical unit of Azure services that's linked to an Azure account
- Account: n identity in Microsoft Entra ID or a directory that's trusted by Microsoft Entra ID, such as a work or school account.

### Things to consider when using subscriptions

- **Consider the types of Azure accounts required**
- **Consider multiple subscriptions**
- **Consider a dedicated shared services subscription**
- **Consider access to resources**

###  Obtain an Azure subscription

- Enterprise Agreement
- Microsoft Reseller
- Microsoft Partner
- Personal Free Account

### Identify Azure subscription usage

- Free
- Pay as you go
- EA
- Student

### Things to consider when choosing Azure subscriptions

- **Consider trying Azure for free**
- **Consider paying monthly for used services**
- **Consider using an Azure Enterprise Agreement**
- **Consider supporting Azure for students**

## Implement Microsoft Cost Management

- provides support for administrative billing tasks
- manage billing access to costs.
- monitor and control Azure spending
- optimize your Azure resource usage

### Things to know about Microsoft Cost Management

- shows organizational cost and usage patterns with advanced analytics
- Costs are based on negotiated prices and factor in reservation and Azure Hybrid Benefit discounts
- Predictive analytics are also available.
- Reports in Microsoft Cost Management show the usage-based costs consumed by Azure services and third-party Marketplace offerings. Collectively, the reports show your internal and external costs for usage and Azure Marketplace charges. The reports help you understand your spending and resource use, and can help find spending anomalies. Charges, such as reservation purchases, support, and taxes might not be visible in reports.
- The product uses Azure management groups, budgets, and recommendations to show clearly how your expenses are organized and how you might reduce costs.
- You can use the Azure portal or various APIs for export automation to integrate cost data with external systems and processes. Automated billing data export and scheduled reports are also available.

### Things to consider when using Microsoft Cost Management

- **Consider cost analysis**
- **Consider budget options**
- **Consider recommendations**
	- View cost optimization recommendations to see potential usage inefficiencies.
	- Act on a recommendation to modify your Azure resource use and implement a more cost-effective option.
	- Verify the new action to make sure the change has the desired effect.
- **Consider exporting cost management data**
	-  Set a daily scheduled export in comma-separated-value (CSV) format and store the data files in Azure storage.
	- Access your exported data from your external system.

## Apply resource tagging

- sorting, searching, managing, and doing analysis on your resources
- Each resource tag consists of a name and a value

For example : 
		- Tag name: `Server`
		- Value: `Production` or `Deployment`
- tag name remains constant for all resources that have the tag applied
- tag value can be selected from a defined set of values, or unique for a specific resource instance
- resource or resource group can have a maximum of <span style="background:#ff4d4f">50</span> tag name/value pairs
- Tags applied to a resource group aren't inherited by the resources in the resource group

### Things to consider when using resource tags

- **Consider searching on tag data**
- **Consider finding related resources**
- **Consider grouping billing data**
- **Consider creating tags with PowerShell or the Azure CLI**


> [!NOTE] Resource Tags Usage
> **You can apply tags to your Azure resources, resource groups, and subscriptions**, but not to management groups.


## Apply Cost Savings

| Cost saving               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Reservations**          | Save money by paying ahead. You can pay for one year or three years of virtual machine, SQL Database compute capacity, Azure Cosmos DB throughput, or other Azure resources. Pre-paying allows you to get a discount on the resources you use. Reservations can significantly reduce your virtual machine, SQL database compute, Azure Cosmos DB, or other resource costs up to 72% on pay-as-you-go prices. Reservations provide a billing discount and don't affect the runtime state of your resources. |
| **Azure Hybrid Benefits** | Access pricing benefits if you have a license that includes<font color="#4bacc6"> _Software Assurance_</font>. Azure Hybrid Benefits helps maximize the value of existing on-premises Windows Server or SQL Server license investments when migrating to Azure. There's an Azure Hybrid Benefit Savings Calculator to help you determine your savings.                                                                                                                                                     |
| **Azure Credits**         | Use the monthly credit benefit to develop, test, and experiment with new solutions on Azure. As a Visual Studio subscriber, you could use Microsoft Azure at no extra charge. With your monthly Azure credit, Azure is your personal sandbox for development and testing.                                                                                                                                                                                                                                  |
| **Azure regions**         | Compare pricing across regions. Pricing can vary from one region to another, even in the US. Double check the pricing in various regions to see if you can save by selecting a different region for your subscription.                                                                                                                                                                                                                                                                                     |
| **Budgets**               | Apply the budgeting features in Microsoft Cost Management to help plan and drive organizational accountability. With budgets, you can account for the Azure services you consume or subscribe to during a specific period. Monitor spending over time and inform others about their spending to proactively manage costs. Use budgets to compare and track spending as you analyze costs.                                                                                                                  |
| **Pricing Calculator**    | The [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) provides estimates in all areas of Azure, including compute, networking, storage, web, and databases.                                                                                                                                                                                                                                                                                                                            |

--- 

# Confiure Azure Policy

- [Azure Policy](https://azure.microsoft.com/services/azure-policy/) is a service in Azure that enables you to create, assign, and manage policies to control or audit your resources. These policies enforce different rules over your resource configurations so the configurations stay compliant with corporate standards.

## Create Management Groups

- _Management groups_ provide a governance scope above subscriptions. When you organize subscriptions into management groups, the governance conditions that you apply cascade by inheritance to all associated subscriptions.

- Management groups give you enterprise-grade management at scale, no matter what type of subscriptions you might have. However, all subscriptions within a single management group must trust the same Microsoft Entra tenant.

- For example, you can apply a policy to a management group that limits the regions available for virtual machine (VM) creation. This policy would be applied to all nested management groups, subscriptions, and resources to allow VM creation only in authorized regions.


### Things to know about Management Groups

- By default, all new subscriptions are placed under the top-level management group, or _root group_.
    
- All subscriptions within a management group automatically inherit the conditions applied to that management group.
    
- A management group tree can support up to six levels of depth.
    
- Azure role-based access control authorization for management group operations isn't enabled by default.

![[Management Groups.png]]

### Things to consider when using management groups

- **Consider custom hierarchies and groups**
- **Consider policy inheritance**
- **Consider compliance rules**
- **Consider cost reporting**

- A management group has a directory unique identifier (ID) and a display name

## Implement Azure policies

- service in Azure that you can use to create, assign, and manage policies.
- use policies to enforce rules on your resources to meet corporate compliance standards and service level agreements.
- runs evaluations and scans on your resources to make sure they're compliant.

### Things to know about Azure Policy

|Advantage|Description|
|---|---|
|**Enforce rules and compliance**|Enable built-in policies, or build custom policies for all resource types. Support real-time policy evaluation and enforcement, and periodic or on-demand compliance evaluation.|
|**Apply policies at scale**|Apply policies to a management group with control across your entire organization. Apply multiple policies and aggregate policy states with policy initiative. Define an exclusion scope.|
|**Perform remediation**|Conduct real-time remediation, and remediation on your existing resources.|
|**Exercise governance**|Implement governance tasks for your environment:  <br>- Support multiple engineering teams (deploying to and operating in the environment)  <br>- Manage multiple subscriptions  <br>- Standardize and enforce how cloud resources are configured  <br>- Manage regulatory compliance, cost control, security, and design consistenc|

### Things to consider when using Azure Policy

- **Consider deployable resources**
- **Consider location restrictions**
- **Consider rules enforcement**
- **Consider inventory audits**

- **_Policy Definition_** describes the compliance conditions for a resource, and the actions to complete when the conditions are met.
- **_Initiative Definition_**: One or more policy definitions are grouped into an _initiative definition_, to control the scope of your policies and evaluate the compliance of your resources.

![[Initiative Definition.png]]

## The four steps to create an Azure Policy

1. Create policy definitions
2. Create an initiative definition
3. Scope the initiative definition
4. Determine compliance

## Create Policy Definitions

- access built in policy definitions
	- **Allowed virtual machine size SKUs**
	- **Allowed locations**
	- **Configure Azure Device Update for IoT Hub accounts to disable public network access**
- or create your own definitions
- or import definitions from other resources

## Create Initiative Definitions

- the definition uses the specific JSON format required by Azure
- use build in definitions in Azure Policy. Examples are:
	- **Audit machines with insecure password security settings**
	- **Configure Windows machines to run [[Azure Monitor Agent]] and associate them to a Data Collection Rule**
	- **Configure [[Azure Defender]] to be enabled on SQL servers**

## Scoping Initiative Definitions

- affected subscriptions
- affected resource groups

--- 

# Manage users and groups in Microsoft Entra ID

![[AD vs EntraID.png]]

These cloud services uses MS Entra ID:
- Microsoft Azure
- Microsoft 365
- Microsoft Intune
- Microsoft Dynamics 365


> [!NOTE] Subscription to Entra ID Relation
> A subscription is associated with a **single Microsoft Entra directory**. Multiple subscriptions can trust the same directory, but a subscription can only trust one directory.

- Users and groups to multiple subscriptions. This allows the user to create, control, and access resources in the subscription. When you add a user to a subscription, the user must be known to the associated directory.

![[MS Entra ID.png]]

## User Definition in Microsoft Entra ID

- **Cloud identities**
- **Directory-synchronized identities**
- **Guest users**

## Adding Users

- Syncing an on-premises Windows Server Active Directory
	- Using [[Microsoft Entra Connect]]
	- most enterprise customers add users to the directory
	- Advantage: SSO

- Using the Azure portal
- Using the command line
	- When adding lots of users
	- Use the `New-MgUser` or `az ad user create` command
	- add users in bulk using CSV files using [[Connect-MgGraph]]

```Powershell
# Create a password profile value
$PasswordProfile = @{ Password = "<Password>" }

# Create the new user
New-MgUser -DisplayName "Abby Brown" -PasswordProfile $PasswordProfile -MailNickName "AbbyB" -UserPrincipalName "AbbyB@contoso.com" -AccountEnabled

```

```Azure CLI
az ad user create --display-name "Abby Brown" --password "<password>" --user-principal-name "AbbyB@contoso.com" --force-change-password-next-login true --mail-nickname "AbbyB"
```

- Other options
	- Microsoft Graph API
	- Microsoft 365 Admin Center
	- Microsoft Intune Admin console


## Types of Groups in Microsoft Entra ID

| Security Groups                                                                    | Microsoft 365 Groups                                                                                                         |
| ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Common, manage member and computer access to shared resources for a group of users | provide collaboration opportunities by giving members access to a shared mailbox, calendar, files, SharePoint site, and more |

### Membership Types

1. **Assigned (static)**. The group will contain specific users or groups that you select.
    
2. **Dynamic user**. You can create rules based on characteristics to enable attribute-based dynamic memberships for groups. For example, if a user’s department is Sales, that user will be dynamically assigned to the Sales group.
    
    You can use security groups for either devices or users, but you can only use Microsoft 365 Groups for user groups. If the user's department changes in the future, they're automatically removed from the group. This feature requires a Microsoft Entra ID P1 license.
    
3. **Dynamic device**. You can create rules based on characteristics to enable attribute-based dynamic memberships for groups. For example, if a user’s device is associated with the Service department, that device will be dynamically assigned to the Service group.


#### Script Group Creating: Using the `New-MgGroup` command

```Powershell
New-MgGroup
-Description "Marketing" 
-DisplayName "Marketing" 
-MailNickName "Marketing"
-SecurityEnabled 
-MailEnabled:$False
```

## Use roles to control resource access

### Built-in roles for Azure Resources (uses PowerShell)

1. Owner
	- Has full access to all resources, including the right to delegate access to others.
2. Contributor
	- create and manage resources. Cannot grant access to others
3. Reader
	- view existing resources

### Role definitions
- A role definition in Azure is a collection of permissions with a name that you can assign to a user, group, or application.
- set of properties in a *JSON* file
- Name, Id, Description
- **Actions**: allowable permissions
- **NotActions**: denied permissions
- Scope
- `Get-AzRoleDefinition Owner`
- Format of `Actions`/`NotActions`: `{Company}.{ProviderName}/{resourceType}/{action}`

|Name|Description|
|---|---|
|`Id`|Unique identifier for the role, assigned by Azure|
|`IsCustom`|True if a custom role, False if a built-in role|
|`Description`|A readable description of the role|
|`Actions []`|Allowed permissions; `*` indicates all|
|`NotActions []`|Denied permissions|
|`DataActions []`|Specific allowed permissions as applied to data, for example `Microsoft.Storage/storageAccounts/blobServices/containers/blobs/read`|
|`NotDataActions []`|Specific denied permissions as applied to data.|
|`AssignableScopes []`|Scopes where this role applies; `/` indicates global, but can reach into a hierarchical tree|

|Built-in Role|Actions|NotActions|
|---|---|---|
|Owner (allow all actions)|`*`|-|
|Contributor (allow all actions except writing or deleting role assignments)|`*`|`Microsoft.Authorization/*/Delete, Microsoft.Authorization/*/Write, Microsoft.Authorization/elevateAccess/Action`|
|Reader (allow all read actions)|`*/read`|-|

## Contributor JSON format:

```json
{
  "Name": "Contributor",
  "Id": "b24988ac-6180-42a0-ab88-20f7382dd24c",
  "IsCustom": false,
  "Description": "Lets you manage everything except access to resources.",
  "Actions": [
    "*"
  ],
  "NotActions": [
    "Microsoft.Authorization/*/Delete",
    "Microsoft.Authorization/*/Write",
    "Microsoft.Authorization/elevateAccess/Action"
  ],
  "DataActions": [],
  "NotDataActions": [],
  "AssignableScopes": [
    "/"
  ]
}
```

## Assignable Scopes

- specifies the scopes (subscriptions, resource groups, or resources) within which the role is available for assignment.
- helps in avoiding clustering of the UX for other subscriptions/resource groups.

## Create roles

- Az Portal
- Az Powershell
- Az Graph API

--- 

- Azure Resources can be secured by using [[Azure RBAC]]

> [!warning] R to RG
> A resource can be bound to only one resource group. 
> A resource group can have multiple resources.

- Users can change their passwords if they forget it by using [[SSPR]] in Microsoft Entra ID.

