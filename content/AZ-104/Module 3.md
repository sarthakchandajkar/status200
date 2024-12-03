---
title: Module 3
aliases:
  - Module 3
draft: false
tags:
  - AZ-104
  - Cloud
  - Microsoft
author:
  - Sarthak Chandajkar
---

# AZ-104: Implement and manage storage in Azure

## Azure Storage

- cloud storage solution
- modern data storage solution
- scalable object store for data objects such as files, messages, tables etc
- Services:
	- File System Service
	- Messaging Store
	- NoSQL store
	- Developers: Web, mobile/desktop apps
	- IaaS VMs
	- PaaS Cloud Services

| Category                 | Description                                                                                                                                                                                            | Storage examples                                                                                                                                                                                                                                                                                                                       |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Virtual machine data** | Virtual machine data storage includes disks and files. Disks are persistent block storage for Azure IaaS virtual machines. Files are fully managed file shares in the cloud.                           | Storage for virtual machine data is provided through Azure managed disks. Data disks are used by virtual machines to store data like database files, website static content, or custom application code. The number of data disks you can add depends on the virtual machine size. Each data disk has a maximum capacity of 32,767 GB. |
| **Unstructured data**    | Unstructured data is the least organized. Unstructured data may not have a clear relationship. The format of unstructured data is referred to as _nonrelational_.                                      | Unstructured data can be stored by using [[Azure Blob Storage]] and [[Azure Data Lake]] Storage. Blob Storage is a highly scalable, REST-based cloud object store. Azure Data Lake Storage is the [[Hadoop Distributed File System (HDFS)]] as a service.                                                                              |
| **Structured data**      | Structured data is stored in a relational format that has a shared schema. Structured data is often contained in a database table with rows, columns, and keys. Tables are an autoscaling NoSQL store. | Structured data can be stored by using Azure Table Storage, Azure Cosmos DB, and Azure SQL Database. Azure Cosmos DB is a globally distributed database service. Azure SQL Database is a fully managed database-as-a-service built on SQL.                                                                                             |
																	[Source](https://learn.microsoft.com/en-us/training/modules/configure-storage-accounts/2-implement-azure-storage)

## Types

1. Standard
2. Premium


> [!NOTE] Storage Account Coversion
> You can't convert a Standard storage account to a Premium storage account or vice versa. You must create a new storage account with the desired type and copy data, if applicable, to a new storage account.

## Things to consider before using Azure Storage

- **Consider durability and availability**
- **Consider secure access**
- **Consider scalability**
- **Consider manageability**
- **Consider data accessibility**


--- 
# Azure Storage Services

- ### **Azure Blob Storage (containers)**:
	- A massively scalable object store for text and binary data.
	- Optimized for storing massive amounts of unstructured or _nonrelational_ data, such as text or binary data
	- **Objects**:  can be accessed anywhere over HTTP/HTTPS
	- **User and client applications**: access blobs via URLs, the [[Azure Storage REST API]], Azure PowerShell, the Azure CLI, or an [[Azure Storage client library]].
	- Ideal for: 
		- Serving images or documents directly to a browser.
		- Storing files for distributed access.
		- Streaming video and audio.
		- Storing data for backup and restore, disaster recovery, and archiving.
		- Storing data for analysis by an on-premises or Azure-hosted service.


> [!NOTE] Azure Blob Storage
> You can access data from Azure Blob Storage [by using the NFS protocol](https://learn.microsoft.com/en-us/training/modules/access-data-azure-blob-storage-multiple-protocols/4-access-data-azure-blob-storage-nfs-protocol).

    
- ### **Azure Files**:
	- Managed file shares for cloud or on-premises deployments.
	- setup high available network file shares.
	- Protocols used:  [[SMB]], [[NFS]]
	- REST interface, storage client libraries

- ### **Azure Queue Storage**:  
	- A messaging store for reliable messaging between application components.
	- up to 64KB in size. 

- ### **Azure Table Storage**:
	- A service that stores non-relational structured data (also known as structured NoSQL data).
	- schemaless
	- [[Azure Cosmos DB Table API]]


## Things to consider before using Azure Storage Services

- **Consider storage optimization for massive data**
- **Consider storage with high availability**
- **Consider storage for messages**
- **Consider storage for structured data**

--- 

# Storage Account Types

- all encrypted using [[SSE]] for data at rest.

| Storage account                                                                                                       | Supported services                                                                        | Recommended usage                                                                                                                                                                                                                                                                   |
| --------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [**Standard** **general-purpose v2**](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-upgrade) | Blob Storage (including Data Lake Storage), Queue Storage, Table Storage, and Azure Files | Standard storage account for most scenarios, including blobs, file shares, queues, tables, and disks (page blobs).                                                                                                                                                                  |
| [**Premium** **block blobs**](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-block-blob-premium)  | Blob Storage (including Data Lake Storage)                                                | Premium storage account for block blobs and append blobs. Recommended for applications with high transaction rates. Use Premium block blobs if you work with smaller objects or require consistently low storage latency. This storage is designed to scale with your applications. |
| [**Premium** **file shares**](https://learn.microsoft.com/en-us/azure/storage/files/storage-how-to-create-file-share) | Azure Files                                                                               | Premium storage account for file shares only. Recommended for enterprise or high-performance scale applications. Use Premium file shares if you require support for both Server Message Block (SMB) and NFS file shares.                                                            |
| [**Premium** **page blobs**](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-pageblob-overview)    | Page blobs only                                                                           | Premium high-performance storage account for page blobs only. Page blobs are ideal for storing index-based and sparse data structures, such as operating systems, data disks for virtual machines, and databases.                                                                   |

--- 

# Replication Strategies

###  Locally redundant storage (LRS)
- lowest cost
- least durable
- Replicas unrecoverable if datacenter level disaster occurs.
- Use Case:
	- data that can be reconstructed easily
	- live feed data that changes continuously, hence storing it is not essential.
	- Organization Data Governance requirements. 

### Zone redundant storage
- Data replicated over *three* storage clusters in one region.
- Each cluster separated physically; separate [[Availability Zone|availability zone]].
- Each zone is autonomous.
- can access and manage your data if a zone becomes unavailable.
- Low latency and excellent performance.
- Not available in all regions.


> [!NOTE] Changing to ZRS from another strategy
>  Changing to ZRS from another data replication option requires the physical data movement from a single storage stamp to multiple stamps within a region.

### Geo-redundant storage
- replication to a secondary region.(>100miles than current location).
- high durability even during regional outage.
- available to be read only if Microsoft initiates a failover from the primary to secondary region.
- 99.99999999999999% **(16 9's) durability**
- Two types of GRS:
	- **GRS** replicates your data to another data center in a secondary region. The data is available to be read only if Microsoft initiates a failover from the primary to secondary region.
	- **Read-access geo-redundant storage** (RA-GRS) is based on GRS. RA-GRS replicates your data to another data center in a secondary region, and also provides you with the option to read from the secondary region. With RA-GRS, you can read from the secondary region regardless of whether Microsoft initiates a failover from the primary to the secondary.
-  is first replicated with locally redundant storage
- committed to the primary location and replicated by using LRS
- update is then replicated asynchronously to the secondary region by using GRS. secondary region uses LRS.
- primary and secondary regions manage replicas across separate [[Fault Domains]] and upgrade domains within a [[Storage Scale Unit]].

### Geo-zone redundant storage
- High availability of zone-redundant storage with protection from regional outages by geo-redundant storage.
- Replication: 3 [[Availability Zone|AZ]] in primary region and secondary geographic region.
- Read and write data if an availability zone becomes unavailable or is unrecoverable.
- Durable during a complete regional outage or during a disaster in which the primary region isn't recoverable.
- 99.99999999999999% (16 9's) durability.
- Scalable.
- **RA-GZRS**: enable read access to data in the secondary region with read-access geo-zone-redundant storage (RA-GZRS).

| Node in data center unavailable                                                              | Entire data center unavailable                                                | Region-wide outage                                             | Read access during region-wide outage |
| -------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- | -------------------------------------------------------------- | ------------------------------------- |
| - **LRS**  <br>- **ZRS**  <br>- **GRS**  <br>- **RA-GRS**  <br>- **GZRS**  <br>- **RA-GZRS** | - **ZRS**  <br>- **GRS**  <br>- **RA-GRS**  <br>- **GZRS**  <br>- **RA-GZRS** | - **GRS**  <br>- **RA-GRS**  <br>- **GZRS**  <br>- **RA-GZRS** | - **RA-GRS**  <br>- **RA-GZRS**       |

--- 
# Accessing Storage

- Endpoint: subdomain + domain.
- Example: To access the _myblob_ data in the _mycontainer_ location in your storage account, we use the following URL address:

`//`**`mystorageaccount`**`.blob.core.windows.net/`**`mycontainer`**`/`**`myblob`**.

### Custom domains
- to access blob data
- Two ways to configure Custom Domains:
	- **Direct mapping**:
		- enable a custom domain for a subdomain to an Azure storage account
		- create a `CNAME` record that points from the subdomain to the Azure storage account.
	- **Intermediary domain mapping**
		- when domain already in use within Azure.
		- may cause minor downtime while domain is being verified.
		- Solution: using `asverify` intermediary domain to validate the domain.
			- permit Azure to recognize your custom domain without modifying the DNS record for the domain. After you modify the DNS record for the domain, your domain is mapped to the blob endpoint with no downtime.
- The following example shows how a domain in use is mapped to an Azure storage account in the DNS with the `asverify` intermediary domain:
	- `CNAME` record: **`asverify`**`.blobs.contoso.com`
	- Intermediate `CNAME` record: **`asverify`**`.contosoblobs.blob.core.windows.net`

> [!NOTE] Azure Storage
> Azure Storage doesn't currently provide native support for HTTPS with custom domains. You can implement an Azure Content Delivery Network (CDN) to access blobs by using custom domains over HTTPS.

## Secure Storage Endpoints
- Firewalls and Virtual Networks
- Access one or more public IP ranges
- Subnets and virtual networks must exist in the same Azure region or region pair as your storage account.
---
# Azure Blob Storage
- storing large amounts of unstructured object data
- Object/Container Storage
- store any type of text or binary

![[Azure Blob Storage.png]]


### Considerations before using Blob Storage

- Browser uploads
- Distributed access
- Streaming data
- Archiving and recovery
- Application access

- Blob must be stored in a container resource.
- Container stores unlimited blobs
- Storage account can have unlimited containers
- Configure [[PAL|Public Access Levels]].
- Command to create blob container: `New-AzStorageContainer`

---
# Blob Access Tiers

![[Access tiers.png]]

|Comparison|Hot access tier|Cool access tier|Cold access tier|Archive access tier|
|---|---|---|---|---|
|**Availability**|99.9%|99%|99%|99%|
|**Availability (RA-GRS reads)**|99.99%|99.9%|99.9%|99.9%|
|**Latency (time to first byte)**|milliseconds|milliseconds|milliseconds|hours|
|**Minimum storage duration**|N/A|30 days|90 days|180 days|


## Blob lifecycle management rules
- rich rule-based policy for GPv2 and Blob Storage accounts.
- lifecycle policy rules to transition your data to the appropriate access tiers.
- set expiration times for the end of a data set's lifecycle.

### Lifecycle Management
- Transition blobs to a cooler storage tier (Hot to Cool, Hot to Archive, Cool to Archive) to optimize for performance and cost.
- Delete blobs at the end of their lifecycles.
- Define rule-based conditions to run once per day at the Azure storage account level.
- Apply rule-based conditions to containers or a subset of blobs.
- **Use the if-then block**:
	- *if* Base blobs were created/modified more than *14* (days ago) *then*:
		1. Move to cool storage.
		2. Move to archive storage.
		3. Delete the blob

--- 
# Blob Object Replication
- copies blobs in a container asynchronously as per configured rule.
- Contents that are copied include: 
	- blob contents
	- blob metadata & properties
	- data associated with blob

![[Blob Object Replication.png]]

- Blob versioning enabled in source and destination accounts.
- Does no support [[Blob Snapshots]].
- Works in Hot, Cold and Cool tiers.
- Replication policy has to be created to specify source & destination storage accounts.
- Policy should have one or more rules.

### Considerations
- Latency reductions.
- Efficiency of compute workloads.
- Data distribution.
- Cost benefits.

## Types of blobs
- **Block blobs(Default)**
	- blocks of data.
	- storing text and binary data in the cloud.
	- Example: files, images and videos.
- **Append blobs**
	- similar to block blobs.
	- optimized for _append_ operations.
	- Example: logging scenarios, data increases with logging.
- **Page blobs**
	- up to *8TB* in size.
	- read/write operations.
	- Example: Virtual Machines uses page blobs for operating system disks and data disks.


> [!NOTE] Blob Types
>  After you create a blob, you can't change its type.


## Upload tools
- Azure Storage Explorer
- AzCopy
- [[Azure Data Box Disk]]
- Azure Import/Export

## Blob Storage Pricing
- Performance tiers
- Data access costs
- Transaction costs
- Geo-replication data transfer costs
- Outbound data transfer costs
- Changes to the storage tier

--- 
# Azure Storage Security

## Security Strategies
- Encryption: [[Azure Storage Encryption]]
- Authentication:
	- Microsoft Entra ID 
	- [[Azure RBAC]]
- Data in transit
	- Client side encryption
	- HTTPS
	- [[SMB 3.0]]
- Disk Encryption:
	- Azure Disk Encryption
- [[Shared Access Signatures]]
- Authorization

|Authorization strategy|Description|
|---|---|
|**Microsoft Entra ID**|Microsoft Entra ID is Microsoft's cloud-based identity and access management service. With Microsoft Entra ID, you can assign fine-grained access to users, groups, or applications by using role-based access control.|
|**Shared Key**|Shared Key authorization relies on your Azure storage account access keys and other parameters to produce an encrypted signature string. The string is passed on the request in the Authorization header.|
|**Shared access signatures**|A SAS delegates access to a particular resource in your Azure storage account with specified permissions and for a specified time interval.|
|**Anonymous access to containers and blobs**|You can optionally make blob resources public at the container or blob level. A public container or blob is accessible to any user for anonymous read access. Read requests to public containers and blobs don't require authorization.|
[Source](https://learn.microsoft.com/en-us/training/modules/configure-storage-security/2-review-strategies)

--- 
# [[Shared Access Signatures]]

--- 

$$
 URI = Azure Storage Resource + SAS token
$$

| Parameter           | Example                                                                                            | Description                                                                                                                                                                                                                                                                                                               |     |
| ------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --- |
| **Resource URI**    | `https://myaccount.`**`blob`**`.core.windows.net/` `?restype=`**`service`** `&amp;comp=properties` | Defines the Azure Storage endpoint and other parameters. This example defines an endpoint for Blob Storage and indicates that the SAS applies to service-level operations. When the URI is used with `GET`, the Storage properties are retrieved. When the URI is used with `SET`, the Storage properties are configured. |     |
| **Storage version** | **`sv`**`=2015-04-05`                                                                              | For Azure Storage version 2012-02-12 and later, this parameter indicates the version to use. This example indicates that version 2015-04-05 (April 5, 2015) should be used.                                                                                                                                               |     |
| **Storage service** | **`ss`**`=bf`                                                                                      | Specifies the Azure Storage to which the SAS applies. This example indicates that the SAS applies to Blob Storage and Azure Files.                                                                                                                                                                                        |     |
| **Start time**      | `st=2015-04-29T22%3A18%3A26Z`                                                                      | (Optional) Specifies the start time for the SAS in UTC time. This example sets the start time as April 29, 2015 22:18:26 UTC. If you want the SAS to be valid immediately, omit the start time.                                                                                                                           |     |
| **Expiry time**     | `se=2015-04-30T02%3A23%3A26Z`                                                                      | Specifies the expiration time for the SAS in UTC time. This example sets the expiry time as April 30, 2015 02:23:26 UTC.                                                                                                                                                                                                  |     |
| **Resource**        | **`sr`**`=b`                                                                                       | Specifies which resources are accessible via the SAS. This example specifies that the accessible resource is in Blob Storage.                                                                                                                                                                                             |     |
| **Permissions**     | **`sp`**`=rw`                                                                                      | Lists the permissions to grant. This example grants access to read and write operations.                                                                                                                                                                                                                                  |     |
| **IP range**        | `sip=168.1.5.60-168.1.5.70`                                                                        | Specifies a range of IP addresses from which a request is accepted. This example defines the IP address range 168.1.5.60 through 168.1.5.70.                                                                                                                                                                              |     |
| **Protocol**        | **`spr`**`=https`                                                                                  | Specifies the protocols from which Azure Storage accepts the SAS. This example indicates that only requests by using HTTPS are accepted.                                                                                                                                                                                  |     |
| **Signature**       | `sig=F%6GRVAZ5Cdj2Pw4tgU7Il` `STkWgn7bUkkAg8P6HESXwmf%4B`                                          | Specifies that access to the resource is authenticated by using an HMAC signature. The signature is computed over a string-to-sign with a key by using the SHA256 algorithm, and encoded by using Base64 encoding.                                                                                                        |     |


## Azure Storage Encryption

- Protects data at rest.
- Encrypted automatically, decrypted automatically before retrieval.
- Transparent to users.
- Encrypted through 256-bit advanced encryption standard (AES) encryption.
- Available for new and existing accounts.

## Customer Managed Keys

- Custom made keys are flexible and reliable.
- Create, disable, audit, rotate and define access for keys.
- Account and key vault must be in the same region but can be in different subscriptions.
- **Configuration**:
	- Encryption type
	- Encryption key

## [Azure Storage Security Best Practices](https://learn.microsoft.com/en-us/training/modules/configure-storage-security/7-apply-best-practices)
---

# Azure Files

- shared storage for applications by using the industry standard [[Server Message Block]] and [[NFS]]
- stores data as true directory objects in file shares.
- 



