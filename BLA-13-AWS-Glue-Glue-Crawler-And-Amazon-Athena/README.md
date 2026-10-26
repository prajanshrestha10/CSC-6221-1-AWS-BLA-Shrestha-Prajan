# CSC-6221-1 BLA - AWS Glue, Crawlers & Athena: Discover, Transform & Query Your Data

## 📌 BLA Number and Title
* **BLA Number:** BLA-13
* **Title:** AWS Certified Machine Learning Associate - Part 13: AWS Glue, Crawlers & Athena (Discover, Transform & Query Your Data)

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to explore serverless data integration and interactive query services on AWS using AWS Glue, Glue Crawlers, the Glue Data Catalog, and Amazon Athena. The lab focuses on discovering raw data formats in Amazon S3, inferring schemas automatically, executing serverless ETL transformations, and running high-performance SQL queries directly against cloud storage while optimizing cost efficiency.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **Data Integration & Catalog Services:** AWS Glue, Glue Data Catalog, Glue Crawlers, Glue ETL Jobs, Glue Studio
* **Interactive Query Engine:** Amazon Athena (Built on open-source Trino engine)
* **Storage & Formats:** Amazon S3, CSV, JSON, Apache Parquet, ORC
* **Languages & Scripting:** PySpark, Scala, Standard SQL

---

## 💡 Concepts Learned
* **The Big Picture Data Flow:** Raw files (CSV, JSON, Parquet) reside in Amazon S3 $\rightarrow$ Glue Crawlers scan and infer schemas $\rightarrow$ Glue Data Catalog stores metadata table definitions $\rightarrow$ Amazon Athena queries the files using standard SQL.
* **What is AWS Glue?** A fully managed, serverless data integration service that makes it easy to discover, prepare, and move data for analytics and machine learning without managing underlying infrastructure, operating on a pay-as-you-go pricing model.
* **The Glue Data Catalog:** A centralized metadata repository containing databases and table definitions (columns, data types, S3 paths, file formats). It stores metadata only—the actual data stays in S3—and is shared across multiple services like Athena, EMR, Redshift Spectrum, and Glue ETL.
* **Glue Crawlers:** Automated workers that point to data stores (S3 paths, JDBC databases, DynamoDB), classify formats using built-in classifiers, infer schemas, and automatically create or update table definitions and partitions in the Data Catalog on demand or on a schedule.
* **Glue ETL Jobs:** Serverless Spark jobs that execute PySpark or Scala code on managed workers to perform Extract, Transform, Load tasks (e.g., converting CSV to Parquet, cleaning data, joining datasets, preparing ML features). Glue Studio provides a visual drag-and-drop interface for building these workflows.
* **Amazon Athena:** An interactive, serverless query service enabling standard SQL queries directly on data stored in S3. It charges based on the volume of data scanned per query.
* **Athena Cost & Performance Optimization Strategies:**
  * *Use Columnar Formats:* Formats like Parquet or ORC allow Athena to read only the specific columns requested by a query.
  * *Partition Data:* Organizing data into folder hierarchies (e.g., by date) allows queries to skip irrelevant folders.
  * *Compress Files:* Shrinking file sizes reduces the total bytes scanned.
  * *Avoid `SELECT *`:* Explicitly declare required columns to minimize data scan costs.

---

## 🏗️ Architecture or Design Description
The serverless data discovery, cataloging, and querying architecture illustrates how AWS Glue and Amazon Athena interact with Amazon S3:

```
+-----------------------------------------------------------------------------------+
|                           DATA LAKE STORAGE (Amazon S3)                           |
|                         (Raw CSV, JSON, Parquet Files)                            |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                         AWS GLUE DISCOVERY & TRANSFORMATION                       |
|   +-----------------------+     +-----------------------+     +---------------+   |
|   |      Glue Crawler     |---->|   Glue Data Catalog   |<- --| Glue ETL Jobs |   |
|   | (Scans S3 & infers schema)| | (Stores Table Metadata|     | (PySpark/Scala)|  |
|   +-----------------------+     +-----------------------+     +---------------+   |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                         AMAZON ATHENA QUERY ENGINE                                |
|          (Interactive Serverless SQL Queries -> Results Saved back to S3)         |
+-----------------------------------------------------------------------------------+
```

---

## 📋 Major Steps Completed
1. Uploaded unstructured and semi-structured raw datasets (CSV and JSON) into designated Amazon S3 buckets.
2. Configured and executed a Glue Crawler to scan the S3 data store, classify file formats, and infer column data types.
3. Inspected the generated table definitions, database groupings, and partition projections inside the central Glue Data Catalog.
4. Created and scheduled a Glue ETL job using Glue Studio to clean data, join datasets, and convert raw CSV formats into partitioned Apache Parquet files.
5. Executed interactive ad-hoc SQL queries in Amazon Athena referencing the Glue Data Catalog tables and analyzed data scan metrics.

---

## ⚠️ Problems or Errors Encountered
* **High Athena Query Costs:** Running broad `SELECT *` queries over unpartitioned CSV files scanned the entire dataset, resulting in high query costs and slow execution times.
* **Schema Drift and Missing Partitions:** Newly added data files dropped into S3 with modified column names caused crawler failures and partition mismatch errors in Athena.

---

## 🔧 How Those Problems Were Resolved
* **Format & Partition Optimization:** Converted raw CSV files into columnar **Parquet** format using Glue ETL jobs and partitioned datasets by date (`year/month/day`), ensuring Athena queries scanned only relevant data blocks.
* **Crawler Scheduling & Classifier Updates:** Configured Glue Crawlers to run on automated schedules and updated custom classifiers to correctly handle schema evolution and new data partitions.

---

## 📊 Results or Output
* Fully automated serverless data discovery pipeline cataloging S3 data sources without infrastructure management.
* High-performance, low-cost SQL query capability in Amazon Athena leveraging columnar compression and partitioning.

---

## 🤔 Lessons Learned / Reflection
AWS Glue and Amazon Athena provide a powerful, serverless analytics stack that eliminates the need to manage database servers for data lakes. By combining Glue Crawlers and Data Catalogs for metadata management with Athena's pay-per-scan query model, organizations can transition raw files into query-ready data assets efficiently and cost-effectively.

---

## 🔗 YouTube Link(s)
* *[Insert your YouTube presentation/lab video link here]*

---

## 💼 LinkedIn Post Link(s)
* *[Insert your LinkedIn project/reflection post link here]*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 13 Presentation Deck
* AWS Documentation: [What is AWS Glue?](https://docs.aws.amazon.com/glue/latest/dg/what-is-glue.html)
* AWS Documentation: [Amazon Athena User Guide](https://docs.aws.amazon.com/athena/latest/ug/what-is.html)
