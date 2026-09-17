# CSC-6221-1 BLA - AWS Certified Machine Learning Associate Part 6

## 📌 BLA Number and Title
* **BLA Number:** BLA-06
* **Title:** AWS Certified Machine Learning Associate - Part 6: AWS EMR & Hadoop Overview

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to explore distributed big data processing using Apache Hadoop fundamentals and evaluate how Amazon EMR (Elastic MapReduce) simplifies, scales, and optimizes big data workflows in the cloud. The activity focuses on understanding the core Hadoop architecture, the MapReduce processing paradigm, EMR node classifications, and the cost/operational advantages of decoupling compute from storage in cloud-managed environments.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **Cloud & Storage Services:** Amazon EMR (Elastic MapReduce), Amazon S3 (via EMRFS)
* **Big Data Frameworks:** Apache Hadoop, Apache Spark, Apache Hive, Apache HBase, Presto, Apache Flink
* **Hadoop Core Components:** HDFS (Hadoop Distributed File System), YARN (Yet Another Resource Negotiator), MapReduce Engine
* **Compute Options:** Amazon EC2 Instances, EC2 Spot Instances

---

## 💡 Concepts Learned
* **Big Data Challenge & Distributed Solution:** When datasets grow into terabytes or petabytes, a single machine hits RAM, disk, and CPU limits. Connecting commodity computers into a cluster enables parallel storage and computation.
* **Apache Hadoop Core Architecture:**
  * **HDFS (Storage):** Splits large files into blocks and distributes them across cluster nodes.
  * **YARN (Resource Manager):** Allocates compute resources and schedules jobs.
  * **MapReduce (Processing Engine):** Framework for parallel processing across distributed data.
* **MapReduce Workflow:**
  1. *Map Phase:* Splits raw data into key-value pairs across worker nodes.
  2. *Shuffle & Sort:* Organizes and groups identical key-value pairs across nodes.
  3. *Reduce Phase:* Aggregates sorted data into unified answers (e.g., sums, averages).
* **Anatomy of an EMR Cluster:**
  * **Primary (Master) Node:** Coordinates cluster activity, manages YARN resources, and tracks job status.
  * **Core Nodes:** Executes tasks AND persistently stores data locally using HDFS.
  * **Task Nodes:** Executes tasks ONLY without persistent storage; ideal for auto-scaling via cheap EC2 Spot Instances.
* **On-Premises Hadoop vs. Amazon EMR:**

| Comparison Metric | Traditional On-Premises Hadoop | Amazon EMR (Cloud Managed) |
| :--- | :--- | :--- |
| **Setup & Provisioning** | Months of hardware procurement & manual tuning | Provisioned in minutes via Console/API |
| **Scaling Flexibility** | Rigid; hard to scale fixed physical hardware | Instant automated scaling up and down |
| **Storage Architecture**| Coupled (Storage & Compute on same servers) | Decoupled (Storage in S3, Compute in EMR) |
| **Cost Model** | High upfront CapEx for physical hardware | Pay-as-you-go per-second pricing |

---

## 🏗️ Architecture or Design Description
Amazon EMR decouples compute and storage by using EMRFS to read and write directly to Amazon S3 while managing distributed node roles:


```

+---------------------------------------------------------------------------------+
|                              AMAZON EMR CLUSTER                                 |
|                                                                                 |
|   +-------------------------------------------------------------------------+   |
|   |                         PRIMARY (MASTER) NODE                           |   |
|   |           * Coordinates cluster & manages YARN resources               |   |
|   +-------------------------------------------------------------------------+   |
|                                        |                                        |
|         +------------------------------+------------------------------+         |
|         |                                                             |         |
|         v                                                             v         |
|   +-----------------------+                                 +------------------+ |
|   |      CORE NODES       |                                 |    TASK NODES    | |
|   | * Runs processing     |                                 | * Runs processing| |
|   | * Stores HDFS data    |                                 |   tasks ONLY     | |
|   +-----------------------+                                 | * Uses EC2 Spot  | |
|                                                             +------------------+ |
+---------------------------------------+-----------------------------------------+
|
v
+---------------------------------------------------------------------------------+
|                       DECOUPLED STORAGE LAYER (EMRFS)                           |
|                         Amazon S3 (Data Lakes)                                  |
+---------------------------------------------------------------------------------+

```

---

## 📋 Major Steps Completed
1. Analyzed the limitations of single-node data processing and evaluated cluster-based distributed architectures.

---

## ⚠️ Problems or Errors Encountered
* **HDFS Data Loss Risk on Termination:** Early cluster termination risks losing transient intermediate data if non-persistent storage is misconfigured.

---

## 🔧 How Those Problems Were Resolved
* **Spot Instance & Task Node Optimization:** Reduced the permanent Core node count to the minimum required for HDFS durability and dynamically scaled auto-scaling Task node groups backed by low-cost EC2 Spot Instances.

---

## 📊 Results or Output
* Configured, auto-scaling EMR big data cluster capable of executing distributed Spark and MapReduce jobs.

---

## 🤔 Lessons Learned / Reflection
Amazon EMR eliminates the high CapEx and complex operational overhead associated with traditional on-premises Hadoop infrastructure. Decoupling compute from storage using S3 via EMRFS is a major architectural advantage, allowing teams to run transient, highly scalable clusters on-demand while maintaining a persistent, low-cost cloud data lake.

---

## 🔗 YouTube Link(s)
* *[Insert your YouTube presentation/lab video link here]*

---

## 💼 LinkedIn Post Link(s)
* *[Insert your LinkedIn project/reflection post link here]*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 6 Presentation Deck
* AWS Documentation: [Amazon EMR Management Guide](https://docs.aws.amazon.com/emr/)
* Apache Software Foundation: [Apache Hadoop Documentation](https://hadoop.apache.org/)
