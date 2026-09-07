# CSC-6221-1 BLA - AWS Certified Machine Learning Associate Part 2

## 📌 BLA Number and Title
* **BLA Number:** BLA-02
* **Title:** AWS Certified Machine Learning Associate - Part 2: Data Fundamentals & Architecture

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to explore data structures, properties, and architectures essential for building cloud-based AWS Machine Learning pipelines. This includes evaluating data types, understanding the 3 V's of data, comparing Data Warehouses, Lakes, and Lakehouses, analyzing connectivity protocols (JDBC vs. ODBC), and examining optimized storage file formats such as Apache Parquet and Apache Avro for analytics and model training.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **Storage & Management:** Amazon S3, AWS Lake Formation
* **Analytics & Warehousing:** Amazon Redshift, Redshift Spectrum, Amazon Athena
* **Streaming & Compute:** Amazon Kinesis, Amazon MSK (Managed Streaming for Apache Kafka), AWS Glue, Amazon EMR
* **Databases & Formats:** Amazon DynamoDB, Apache Parquet, Apache Avro, Apache Iceberg, Apache Spark, CSV, JSON
* **Connectivity & Visualization:** JDBC, ODBC, Amazon QuickSight

---

## 💡 Concepts Learned
* **Data Categorization:** Structured (predefined tabular schemas), Semi-Structured (JSON/XML tags without rigid schemas), and Unstructured (raw images, audio, PDFs lacking predefined models).
* **The 3 V's of Data:** Volume (scale/quantity), Velocity (speed of generation/streaming), and Variety (diverse formats).
* **Data Architectures:**
  * **Data Warehouse:** Schema-on-write, ETL-driven, structured data focus (Amazon Redshift).
  * **Data Lake:** Schema-on-read, ELT-driven, centralized multi-format storage (Amazon S3 + AWS Lake Formation).
  * **Data Lakehouse:** Hybrid approach offering ACID compliance and unified governance across S3 data lakes and warehouse engines.
  * **Data Mesh:** Decentralized organizational paradigm treating data as a product managed by domain teams.
* **Connectivity Protocols:** JDBC (Platform-independent, JVM/Language-dependent for Glue/Spark on EMR) vs. ODBC (Platform-dependent C/C++ base for OS clients/BI tools like QuickSight).
* **Storage Formats:**
  * **CSV/JSON:** Text-based row formats; human-readable but slow and verbose at scale.
  * **Apache Avro:** Row-based binary storage embedded with JSON schema; optimized for write-heavy streaming (Kafka/Kinesis).
  * **Apache Parquet:** Columnar binary format utilizing predicate pushdown to skip irrelevant data; cuts query execution time and reduces Amazon Athena/Redshift scanning costs.

---

## 🏗️ Architecture or Design Description
The architecture illustrates an end-to-end Data Lakehouse system integrating disparate data streams into unified analytical consumption layers:


```

+-------------------+      +-------------------+      +---------------------+      +---------------------+      +---------------------+
|   Data Sources    |      |  Ingestion Layer  |      |    Storage Layer    |      | Metadata/Governance |      |  Consumption Layer  |
|                   |      |                   |      |                     |      |        Layer        |      |                     |
| * Structured Data | ---> | * Batch (ETL)     | ---> | * Data Lake (S3)    | ---> | * Metadata Caching  | ---> | * BI & Reports      |
| * Semi-Structured |      | * Streaming       |      | * Open Formats      |      | * Indexing          |      | * Data Science      |
| * Unstructured    |      |   (Kinesis/MSK)   |      |   (Parquet/Avro)    |      | * Transaction Mgmt  |      | * Machine Learning  |
+-------------------+      +-------------------+      +---------------------+      +---------------------+      +---------------------+
|                            |
+------------ APIs ----------+
(SQL APIs & DataFrames)

```

---

## 📋 Major Steps Completed
1. Categorized enterprise data types and evaluated their impact on Machine Learning pipelines.
2. Mapped the 3 V's (Volume, Velocity, Variety) to scalable AWS storage and streaming solutions.
3. Differentiated Data Warehouse, Data Lake, Data Lakehouse, and Data Mesh design patterns.
4. Compared JDBC and ODBC database connection drivers across AWS ML ecosystem tools.
5. Analyzed data ingestion mechanisms across raw logs, REST APIs, and real-time streaming services.
6. Evaluated trade-offs between text-based (CSV/JSON), binary row-based (Avro), and binary columnar (Parquet) formats.

---

## ⚠️ Problems or Errors That Can Encounter
* **High Query Costs and Latency in Athena:** Querying large datasets stored in raw CSV format resulted in long processing times and high scan charges on Amazon Athena due to full table scans.

---

## 🔧 How Those Problems Can Be Resolved
* **Conversion to Apache Parquet:** Converted raw text datasets into Apache Parquet format using AWS Glue, leveraging columnar compression and predicate pushdown to reduce data scanning by up to 90%+ and lower costs.

---

## 📊 Results or Output
* Complete architectural understanding of cloud data pipelines for AWS Machine Learning.
* Formatted comparison tables for data architectures, connectivity drivers, and storage file formats.
* Updated repository documentation reflecting Part 2 concepts.

---

## 🤔 Lessons Learned / Reflection
Selecting the correct file format and storage architecture directly dictates performance and cost efficiency in AWS ML engineering. While row-oriented binary formats like Apache Avro excel in write-heavy real-time ingestion, columnar formats like Apache Parquet are far superior for high-throughput batch querying and feature extraction in model training pipelines.

---

## 🔗 YouTube Link(s)
* *https://www.youtube.com/watch?v=78eDVTPEd44*

---

## 💼 LinkedIn Post Link(s)
* *https://www.linkedin.com/feed/update/urn:li:activity:7502520592122720257/*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 2 Presentation Deck
* AWS Documentation: [Building Data Lakes and Analytics on AWS](https://aws.amazon.com/big-data/datalakes-and-analytics/)
* Apache Parquet Documentation: [Apache Parquet Overview](https://parquet.apache.org/)

```
