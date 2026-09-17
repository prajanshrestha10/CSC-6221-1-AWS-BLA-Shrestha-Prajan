# CSC-6221-1 BLA - AWS Certified Machine Learning Associate Part 5

## 📌 BLA Number and Title
* **BLA Number:** BLA-05
* **Title:** AWS Certified Machine Learning Associate - Part 5: Kinesis Data Streams vs. Amazon MSK

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to compare and evaluate two core real-time data streaming technologies on AWS: Amazon Kinesis Data Streams and Amazon Managed Streaming for Apache Kafka (Amazon MSK). The lab focuses on understanding their shared capabilities, architectural differences, underlying scaling mechanics, ecosystem integration, and criteria for selecting the appropriate service for enterprise real-time data pipelines and machine learning workloads.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **Streaming Platforms:** Amazon Kinesis Data Streams, Amazon MSK (Managed Streaming for Apache Kafka)
* **Kafka Ecosystem:** Kafka Connect, Kafka Streams, ksqlDB, Apache Kafka open-source protocol
* **AWS Integrations:** AWS Lambda, Amazon S3, Amazon Redshift, Amazon Data Firehose, Kinesis Data Analytics
* **SDKs & APIs:** Kinesis Client Library (KCL), AWS SDKs, Standard Kafka Producer/Consumer APIs

---

## 💡 Concepts Learned
* **Shared Capabilities:** Both services provide fully managed, durable real-time data streaming with configurable data retention windows, enabling decoupled consumers (Lambda, S3, Redshift, ML pipelines) to process streams independently.
* **Amazon Kinesis Data Streams:**
  * AWS-native, proprietary streaming service built around fixed-capacity units called **shards**.
  * Supports provisioned capacity mode or automated on-demand scaling.
  * Offers configurable retention ranging from 24 hours up to 365 days.
  * Consumed natively via AWS SDKs, KCL, Lambda, or Kinesis Data Analytics with lower operational overhead.
* **Amazon MSK (Managed Streaming for Apache Kafka):**
  * Fully managed implementation of open-source **Apache Kafka**.
  * Speaks standard, non-proprietary Kafka protocols, ensuring zero vendor lock-in and seamless cloud portability.
  * Available in provisioned (broker-based) or MSK Serverless modes.
  * Compatible with open-source tools such as Kafka Connect, Kafka Streams, and ksqlDB.
* **Key Differences Matrix:**

| Feature | Kinesis Data Streams | Amazon MSK |
| :--- | :--- | :--- |
| **Underlying Tech** | AWS-native (proprietary) | Apache Kafka (open source) |
| **API / Protocol** | Kinesis API / AWS SDK | Standard Kafka protocol |
| **Scaling Mechanism** | Shards (manual or on-demand) | Brokers & partitions / MSK Serverless |
| **Ecosystem** | AWS-native (Lambda, Firehose) | Kafka Connect, Streams, ksqlDB |
| **Operational Overhead**| Low (fully abstracted) | Moderate (broker & cluster configuration) |
| **Portability** | AWS-bound | Cross-cloud & hybrid compatible |

---

## 🏗️ Architecture or Design Description
The architectural flow highlights how both streaming services ingest real-time data streams from diverse producers and fan out data to downstream analytics and machine learning consumers:


```

+-------------------------------------------------------+
|                     PRODUCERS                         |
|  (Applications, IoT Devices, Web Servers, Sensors)    |
+-------------------------------------------------------+
|
+------------------+------------------+
|                                     |
v                                     v
+-------------------------------+   +-------------------------------+
|  Kinesis Data Streams         |   |  Amazon MSK (Apache Kafka)    |
|  * Shard-based architecture   |   |  * Broker/Partition based     |
|  * AWS SDK / KCL              |   |  * Standard Kafka Protocol    |
+-------------------------------+   +-------------------------------+
|                                     |
+------------------+------------------+
|
v
+-------------------------------------------------------+
|                    CONSUMERS                          |
|  * AWS Lambda Functions / Real-Time ML Endpoints      |
|  * Amazon S3 (Data Lakes via Firehose)                |
|  * Amazon Redshift / OpenSearch                       |
|  * Kafka Streams / ksqlDB (MSK specific)              |
+-------------------------------------------------------+

```

---

## 📋 Major Steps Completed
1. Analyzed real-time streaming architectures on AWS and established baseline feature equivalencies between Kinesis and MSK.
2. Evaluated Kinesis Data Streams shard dynamics, read/write limits, and on-demand capacity management.
3. Examined Amazon MSK cluster provisioning, broker sizing, partition distribution, and MSK Serverless features.
4. Compared operational complexity, vendor lock-in risks, and ecosystem integrations across both streaming solutions.
5. Formulated workload decision frameworks for selecting between Kinesis Data Streams and Amazon MSK.

---

## ⚠️ Problems or Errors Encountered
* **Kinesis Shard Throttling (`ProvisionedThroughputExceededException`):** Occurred when write traffic exceeded 1 MB/s or 1,000 records/s per shard limit.
* **Kafka Consumer Offset Lags in MSK:** High partition count with under-provisioned consumers caused growing offset lag during traffic spikes.

---

## 🔧 How Those Problems Were Resolved
* **Kinesis Mitigation:** Switched Kinesis stream mode from Provisioned to **On-Demand**, allowing AWS to auto-scale shard counts, or performed manual shard splitting to distribute high-key volume.
* **MSK Mitigation:** Added parallel consumer instances matching partition count within the consumer group and reconfigured MSK broker instance types to increase throughput headroom.

---

## 📊 Results or Output
* Comprehensive decision framework mapping streaming requirements to the appropriate AWS service.
* Clear architectural guideline for choosing between native AWS simplicity (Kinesis) versus open-source ecosystem portability (MSK).

---

## 🤔 Lessons Learned / Reflection
Choosing between Kinesis Data Streams and Amazon MSK depends on team expertise, cloud strategy, and ecosystem dependencies. Kinesis is optimal for greenfield, AWS-native applications seeking minimal management overhead. Conversely, Amazon MSK is the superior choice when migrating existing Kafka workloads, leveraging tools like Kafka Connect/ksqlDB, or prioritizing multi-cloud portability.

---

## 🔗 YouTube Link(s)
* *https://youtu.be/CO10HtXQM2c*

---

## 💼 LinkedIn Post Link(s)
* *https://www.linkedin.com/feed/update/urn:li:activity:7506453174115966977/*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 5 Presentation Deck
* AWS Documentation: [Amazon Kinesis Data Streams Developer Guide](https://docs.aws.amazon.com/streams/)
* AWS Documentation: [Amazon MSK Developer Guide](https://docs.aws.amazon.com/msk/)
* Apache Kafka Documentation: [Apache Kafka Core Concepts](https://kafka.apache.org/documentation/)
