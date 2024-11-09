---
title: ETL
aliases: 
draft: false
tags:
  - Data
  - DataEngineering
  - Python
  - SQL
  - Airflow
  - DataFactory
  - Status200
  - "#Java"
  - "#Scala"
author:
  - Sarthak Chandajkar
---
# **What is ETL?** 
 
 - data integration process
 - commonly used in Data Engineering/Data Analysis
 - collecting data -> transforming in usable form -> load to destination system for analysis
 - **ETL Pipelines**: essential for making raw data accessible, actionable and valuable for the purpose of decision making.

# **E: Extract**

- collecting data from sources
- essential as data is gathered from multiple sources like databases, applications and files.
- **Goal**: Bring data in all different formats(structured ,semi-structured, unstructured) together from different systems.
- Important to collect the data without any alteration.
- Examples of Data Sources:
	- **Relational Databases**: MySQL, PostgreSQL, MS SQL Server.
	- **NoSQL Databases**: MongoDB, Cassandra, or DynamoDB.
	- **Flat Files**: CSV, JSON, XML, or Parquet files.
	- **APIs**: Data retrieved from third-party services via RESTful APIs.
	- **Cloud Services**: Data from cloud platforms like AWS, Azure, or Google Cloud Storage.


## **Extraction Methods**

- **Full Extraction**: all data extracted
- **Incremental Extraction**: recent/changed data extracted; based in timestamp of [[CDC]].
- **Real-Time Extraction**: continuos extraction


# **T: Transform**

- essential to making the extracted data useful.
- manipulation/cleaning of raw data to fit the purpose.
- making the data suitable to anlayze

## **Transformation Steps**

1. **Data Cleaning**
2. **Data Mapping**
3. **Data Aggregation**
4. **Normalization or Denormalization**
5. **Enrichment**
6. **Data Formatting**

## Transformation Methods

- [[Batch Transformation]]
- [[Real-Time Transformation]]

## L: Load

- loading data to target systems for analysis
- Examples for target systems
	- [[Data Warehouse]]
	- [[Data Lakes]]
	- [[Relational Databases]]
	- [[NoSQL Databases]]

### Strategies

- **Full Load**: Loading the entire transformed dataset into the target system. This can be costly in terms of time and resources for large datasets.
- **Incremental Load**: Loading only the data that has changed or been added since the last load, which is more efficient for large datasets.
- **Real-Time Load**: Continuously loading data as it is transformed, typically seen in real-time analytics systems.

--- 

# Tools and Technologies

## Frameworks

- [[Airflow]]
- **Apache Nifi**: Data integration tool for automating data flow between systems.
- **AWS Glue**: Managed ETL service in AWS that automates much of the data preparation work.
- [[Azure Data Factory]]: Cloud-based ETL service for orchestrating and automating data flows.
- **Talend**: A powerful ETL tool with a graphical interface for building data pipelines.
- **Pentaho**: Data integration tool that provides ETL capabilities, along with analytics and reporting.
---

### **Benefits of ETL**

- **Data Consolidation**: ETL allows you to aggregate data from disparate sources into a single, unified system, making it easier to analyze and derive insights.
- **Data Quality**: Through the transformation step, ETL can ensure that the data is clean, accurate, and consistent.
- **Scalability**: ETL systems can scale to handle growing amounts of data efficiently.
- **Time Efficiency**: Automated ETL processes reduce the time needed for data preparation, freeing up time for analysis.

---

### **Challenges of ETL**

- **Data Quality Issues**: If the source data is incomplete or incorrect, it will impact the accuracy of insights derived from the transformed data.
- **Performance**: Complex transformations and large data volumes can slow down ETL processing. Optimizing ETL pipelines for performance is essential.
- **Complexity**: As the number of data sources and transformations increases, managing ETL pipelines becomes increasingly complex.
- **Real-Time Processing**: Implementing real-time ETL pipelines requires more sophisticated infrastructure and technology (e.g., Apache Kafka, stream processing).

---

### **ETL vs. ELT (Extract, Load, Transform)**

An alternative to ETL is the **ELT** (Extract, Load, Transform) process, where data is loaded into the destination system first, and then transformed. This approach is more common when working with **cloud-based** systems and data lakes, where data can be transformed within the storage environment itself.

- **ETL**: Transformation happens before the data is loaded into the target system.
- **ELT**: Data is loaded first, and then transformation happens inside the target system.