# CSC-6221-1 BLA - AWS Certified Machine Learning Associate Part 4

## 📌 BLA Number and Title
* **BLA Number:** BLA-04
* **Title:** AWS Certified Machine Learning Associate - Part 4: Amazon Data Firehose & Streaming Data

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to explore real-time streaming data ingestion using Amazon Data Firehose (formerly Kinesis Data Firehose). The lab focuses on capturing continuous data streams from various AWS sources, applying serverless transformations, buffering records, and automatically delivering batches to cloud storage, data warehouses, or analytics destinations without managing underlying server infrastructure.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **Streaming Services:** Amazon Data Firehose, Amazon Kinesis Data Streams
* **Compute & Transformation:** AWS Lambda
* **Sources & Producers:** CloudWatch Logs & Events, AWS IoT, Direct SDK/API PUT requests
* **Destinations & Storage:** Amazon S3 (Data Lakes), Amazon Redshift (Data Warehouses), Amazon OpenSearch, Splunk, Generic HTTP Endpoints
* **Formats & Processing:** Apache Parquet, Data Compression, GZIP/Encryption

---

## 💡 Concepts Learned
* **Amazon Data Firehose Architecture:** A fully managed, serverless delivery service that captures, optionally transforms, buffers, compresses, encrypts, and delivers streaming data.
* **4-Step Streaming Workflow:**
  1. **Capture:** Ingests streaming records from Kinesis Data Streams, IoT, CloudWatch, or Direct API calls.
  2. **Transform:** Uses inline AWS Lambda functions to reformat, filter, or enrich data on the fly.
  3. **Buffer:** Accumulates incoming records based on configurable size or time thresholds (whichever limit is reached first).
  4. **Deliver:** Automatically converts formats (e.g., JSON to Parquet), compresses, encrypts, and delivers data to designated sinks.
* **Firehose vs. Kinesis Data Streams:**
  * **Data Firehose:** Fully managed delivery service requiring no consumer code or infrastructure management.
  * **Kinesis Data Streams:** Custom streaming platform requiring manual consumer development and scaling management for direct processing control.
* **Common Industry Use Cases:** Streaming ETL pipelines into S3 data lakes, real-time log/event analytics, high-volume IoT sensor ingestion, and feeding real-time ML feature pipelines.

---

## 🏗️ Architecture or Design Description
The real-time streaming pipeline follows an automated ingestion, processing, and delivery workflow:


```

+--------------------------+
|      Data Sources        |
| * Kinesis Data Streams   |
| * Direct PUT (SDK/API)   |
| * CloudWatch Logs        |
| * AWS IoT Core           |
+--------------------------+
|
v
+-----------------------------------------------------------------------------------+
|                              Amazon Data Firehose                                 |
|                                                                                   |
|  [ 1. Capture ] ---> [ 2. Transform ] ---> [ 3. Buffer ] ---> [ 4. Deliver ]      |
|                        (AWS Lambda)       (Size/Time)        (Format/Encrypt)    |
+-----------------------------------------------------------------------------------+
|
+-------------------------------+-------------------------------+
|                               |                               |
v                               v                               v
+------------------+           +------------------+           +------------------+
|    Amazon S3     |           | Amazon Redshift  |           | Amazon OpenSearch|
|   (Data Lake)    |           |   (Warehouse)    |           | (Search/Splunk)  |
+------------------+           +------------------+           +------------------+

```

---

## 📋 Major Steps Completed
1. Evaluated real-time streaming mechanics and compared Amazon Data Firehose against Kinesis Data Streams.
2. Configured automatic data format conversion from incoming raw JSON into Apache Parquet before S3 storage delivery.

---

## ⚠️ Problems or Errors Encountered
* **High Latency / Micro-Batch Delays:** Noticed that data delivery was lagging by up to 60 seconds when incoming traffic volume was low.
* **Lambda Transformation Timeout:** AWS Lambda functions timed out during peak traffic spikes while attempting to parse and reformat large batches of records.

---

## 🔧 How Those Problems Were Resolved
* **Buffer Threshold Adjustment:** Decreased the buffer time threshold (e.g., from 300 seconds to 60 seconds) and lowered buffer size settings to ensure near-real-time streaming delivery during low-traffic periods.
* **Lambda Optimization & Batch Size Tuning:** Increased the AWS Lambda function memory/timeout allocation and lowered the max record batch size sent to Lambda by Firehose to prevent processing timeouts.

---

## 📊 Results or Output
* Fully automated, serverless streaming ETL pipeline delivering compressed Parquet files directly to Amazon S3.

---

## 🤔 Lessons Learned / Reflection
Amazon Data Firehose simplifies building cloud data ingestion pipelines by abstracting away consumer management, scaling, and server maintenance. Converting raw JSON streams directly into optimized columnar formats like Apache Parquet inside Firehose significantly improves downstream query speed and cuts storage costs across AWS data lakes.

---

## 🔗 YouTube Link(s)
* *https://youtu.be/XqCcaRz2DOE*

---

## 💼 LinkedIn Post Link(s)
* *https://www.linkedin.com/feed/update/urn:li:activity:7506437503596535808/*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 4 Presentation Deck
* AWS Documentation: [Amazon Data Firehose Developer Guide](https://docs.aws.amazon.com/firehose/)
* AWS Documentation: [Kinesis Data Streams vs. Data Firehose](https://aws.amazon.com/kinesis/data-firehose/)
