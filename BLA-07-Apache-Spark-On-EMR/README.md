# CSC-6221-1 BLA - AWS Certified Machine Learning Associate Part 7

## 📌 BLA Number and Title
* **BLA Number:** BLA-07
* **Title:** AWS Certified Machine Learning Associate - Part 7: Apache Spark on Amazon EMR

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to examine Apache Spark as a high-performance, in-memory distributed data processing engine and evaluate the operational and architectural benefits of running Spark workloads on Amazon EMR (Elastic MapReduce). The lab focuses on deconstructing Spark's execution architecture, contrasting in-memory computing with legacy disk-bound MapReduce, leveraging EMR for decoupled S3 storage, and building scalable ETL, streaming, and ML pipelines.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **Big Data & Analytics Engine:** Apache Spark, Spark SQL, Spark Streaming, MLlib (Machine Learning Library), GraphX
* **Cloud Platform & Deployment:** Amazon EMR (EMR on EC2, EMR Serverless, EMR on EKS)
* **Storage & Metadata:** Amazon S3 (EMRFS decoupled storage), AWS Glue Data Catalog
* **Developer Tools & Analytics:** EMR Studio, Jupyter Notebooks, Amazon Athena, Amazon CloudWatch
* **Languages Supported:** Python (PySpark), Scala, Java, R, SQL
* **Compute Options:** EC2 On-Demand Instances, EC2 Spot Instances

---

## 💡 Concepts Learned
* **Apache Spark Overview:** An open-source, multi-language, general-purpose distributed processing engine that handles batch, streaming, SQL queries, machine learning, and graph processing in a single unified architecture.
* **Performance Advantage over MapReduce:**
  * *Traditional MapReduce:* Writes intermediate transformation results to disk between steps, making iterative workflows slow despite high reliability.
  * *Apache Spark:* Retains intermediate datasets in RAM across processing pipeline steps, accessing disk only when necessary, resulting in significantly higher speed.
* **Spark Distributed Architecture:**
  * **Driver Program:** Coordinates the job execution, builds the logical plan, and splits user code into discrete parallel tasks.
  * **Cluster Manager:** Allocates underlying compute resources across cluster nodes (e.g., YARN, Kubernetes).
  * **Executors:** Distributed worker processes that execute tasks and store cached data directly in RAM.
* **Why Run Spark on Amazon EMR:**
  * *Zero Infrastructure Overhead:* EMR automatically provisions, configures, and tunes clusters without manual setup.
  * *Decoupled Compute & Storage:* Reads and writes data directly to/from Amazon S3, allowing persistent storage to exist independently of cluster lifecycle.
  * *Cost Optimization:* Supports EC2 Spot Instances for fault-tolerant workloads and automated instance group scaling based on memory/CPU pressure.
* **Primary Use Cases:** Large-scale batch ETL pipelines, real-time streaming analytics, feature engineering and model training via MLlib, and interactive data exploration using EMR Studio Notebooks.

---

## 🏗️ Architecture or Design Description
The architectural topology shows how EMR orchestrates Apache Spark components over decoupled Amazon S3 storage and managed AWS catalog services:

```
+-----------------------------------------------------------------------------------+
|                               AMAZON EMR CLUSTER                                  |
|                                                                                   |
|  +-----------------------------------------------------------------------------+  |
|  |                           DRIVER PROGRAM (Primary)                          |  |
|  |            * Coordinates jobs, constructs DAG, splits tasks                 |  |
|  +-----------------------------------------------------------------------------+  |
|                                         |                                         |
|                               v                   v                               |
|                  +---------------------+ +---------------------+                  |
|                  |   CLUSTER MANAGER   | |   EMR STUDIO /      |                  |
|                  | (YARN / EKS / EMR)  | | JUPYTER NOTEBOOK    |                  |
|                  +---------------------+ +---------------------+                  |
|                                         |                                         |
|         +-------------------------------+-------------------------------+         |
|         |                                                               |         |
|         v                                                               v         |
|  +-----------------------------------+                   +---------------------+  |
|  |            EXECUTOR 1             |                   |     EXECUTOR 2      |  |
|  |  * Tasks run in RAM               |                   | * Tasks run in RAM  |  |
|  |  * In-Memory Data Cache           |                   | * In-Memory Cache   |  |
|  +-----------------------------------+                   +---------------------+  |
+---------------------------------------+-------------------------------------------+
                                        |
                   +--------------------+--------------------+
                   v                                         v
+---------------------------------------+   +---------------------------------------+
|          AWS GLUE DATA CATALOG        |   |       DECOUPLED STORAGE (EMRFS)       |
|     * Central Schema / Metadata       |   |       Amazon S3 (Data Lake)           |
+---------------------------------------+   +---------------------------------------+
```

---

## 📋 Major Steps Completed
1. Compared the in-memory execution model of Apache Spark against disk-bound MapReduce architectures.
2. Configured PySpark application scripts utilizing Spark SQL and DataFrame APIs for dataset transformations.
3. Provisioned an Amazon EMR cluster with Spark pre-installed and mapped EMRFS to read raw input data directly from S3.
4. Established interactive exploration using EMR Studio Jupyter Notebooks connected to the live EMR cluster.
5. Configured Auto-scaling policies and introduced EC2 Spot Instances for Task node groups to lower processing costs.

---

## ⚠️ Problems or Errors Encountered
* **`OutOfMemoryError` (Java Heap Space / Container Overhead):** High-volume joins and unaggregated PySpark operations caused executor nodes to crash due to insufficient memory allocation.
* **Spot Instance Termination Interruption:** Sudden reclaim of EC2 Spot Task nodes caused transient job delays when task progress was lost mid-transformation.

---

## 🔧 How Those Problems Were Resolved
* **Memory & Partition Tuning:** Increased `spark.executor.memory` and `spark.driver.memory` allocations in EMR configuration, and repartitioned large DataFrames using `.repartition()` to balance memory load evenly across all executors.
* **Fault-Tolerant Node Layout:** Kept Primary (Master) and Core nodes on On-Demand EC2 instances while restricting Spot Instances strictly to stateless Task node groups, allowing Spark to automatically reassign failed tasks to surviving executors without job failure.

---

## 📊 Results or Output
* High-speed, in-memory data processing pipeline running PySpark on Amazon EMR.
* Cost-effective cluster architecture leveraging decoupled Amazon S3 storage and Spot instance Task nodes for batch ETL execution.

---

## 🤔 Lessons Learned / Reflection
Apache Spark on Amazon EMR represents a massive upgrade over traditional Hadoop MapReduce by maintaining intermediate application data in RAM rather than continually writing to physical disk. Combining Spark's unified engine (SQL, MLlib, Streaming) with EMR's managed provisioning and decoupled S3 storage provides a production-grade analytics platform that scales dynamically without operational cluster management overhead.

---

## 🔗 YouTube Link(s)
* *https://youtu.be/EkGvCyhW_mA*

---

## 💼 LinkedIn Post Link(s)
* *https://www.linkedin.com/feed/update/urn:li:activity:7511576150406742016/*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 7 Presentation Deck
* AWS Documentation: [Apache Spark on Amazon EMR](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/EMR_Spark.html)
* Apache Spark Documentation: [Apache Spark Overview](https://spark.apache.org/docs/latest/)
