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

- Locally redundant storage (LRS)
- Zone redundant storage (ZRS)
- Geo-redundant storage (GRS)
- Geo-zone-redundant storage (GZRS)




