# CSC-6221-1 BLA - Processing, Training & Deployment: The Core SageMaker AI Workflow

## 📌 BLA Number and Title
* **BLA Number:** BLA-12
* **Title:** AWS Certified Machine Learning Associate - Part 12: Processing, Training & Deployment (The Core SageMaker AI Workflow)

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to examine the core end-to-end workflow within Amazon SageMaker AI, focusing on how data processing jobs, managed training workflows, and production deployment mechanisms integrate together using Amazon S3 as the central storage hub. The lab explores containerized processing scripts, training input modes, multi-variant deployment strategies, and automated MLOps pipelines.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **AWS Machine Learning & Analytics Services:** Amazon SageMaker (Processing Jobs, Training Jobs, Model Endpoints, Pipelines), Amazon S3, AWS Glue, Amazon EMR, Amazon SageMaker Data Wrangler
* **Frameworks & Containers:** Scikit-Learn, Apache Spark, PyTorch, TensorFlow, Built-in Algorithms (XGBoost)
* **Monitoring & Operations:** Amazon CloudWatch, SageMaker Model Registry
* **Languages & Environments:** Python, Jupyter Notebooks

---

## 💡 Concepts Learned
* **The Big Picture Workflow:** Amazon S3 serves as the central hub where raw data is stored, processed, trained, and saved before being deployed to live endpoints for inference.
* **Data Processing Jobs:** Running custom scripts or containerized environments (Scikit-Learn, Spark) on managed instances to perform data cleaning, feature engineering, train/test splitting, and model evaluation.
* **Choosing a Processing Tool:** Selecting between custom Processing Jobs, point-and-click Data Wrangler, serverless AWS Glue ETL, or large-scale Amazon EMR clusters based on workload volume and complexity.
* **Training Job Mechanics:** Pointing to S3 training data, selecting container images/instances, executing distributed training, and exporting model artifacts (`model.tar.gz`) back to S3 while streaming logs to CloudWatch.
* **Training Input Modes:** 
  * *File Mode:* Copies data locally before training begins.
  * *FastFile Mode:* Streams data on demand.
  * *Pipe Mode:* Streams data straight into the algorithm for maximum throughput.
* **Deployment Architecture:** Structured in three distinct steps: creating the Model artifact, setting up the Endpoint Configuration (instance types, counts, variants), and launching the live HTTPS Endpoint.
* **Advanced Endpoint Management:** Utilizing Auto Scaling, Production Variants for A/B testing, Multi-Model Endpoints to host multiple rare models efficiently, and safe rollouts (blue/green or canary deployments).
* **Automating with SageMaker Pipelines:** Enforcing reproducible MLOps workflows through a repeatable 5-stage pipeline: Process $\rightarrow$ Train $\rightarrow$ Evaluate $\rightarrow$ Register $\rightarrow$ Deploy.

---

## 🏗️ Architecture or Design Description
The architectural topology highlights how Amazon S3 connects each sequential stage of the core SageMaker workflow:

```
+-----------------------------------------------------------------------------------+
|                        CENTRAL STORAGE HUB (Amazon S3)                            |
+-----------------------------------------------------------------------------------+
           |                                             |
           v                                             v
+-----------------------+                     +-----------------------+
|  1. PROCESSING JOB    |                     |   2. TRAINING JOB     |
|  * Cleans & Transforms|-------------------->|  * Learns from data   |
|  * Train/Test Split   |                     |  * Saves model.tar.gz |
+-----------------------+                     +-----------------------+
                                                         |
                                                         v
+-----------------------------------------------------------------------------------+
|                           3. LIVE ENDPOINT & INFERENCE                            |
|             (Endpoint Configuration + Model Artifact + HTTPS Address)             |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                        4. AUTOMATED MLOPS (SageMaker Pipelines)                   |
|                 (Process -> Train -> Evaluate -> Register -> Deploy)              |
+-----------------------------------------------------------------------------------+
```

---

## 📋 Major Steps Completed
1. Configured an Amazon S3 bucket layout to store raw datasets, intermediate processing results, and final model artifacts.
2. Executed a SageMaker Processing Job using a pre-built Scikit-Learn container to clean data and execute train/test splits.
3. Initiated a managed training job using an algorithm container, configuring input modes and logging metrics to CloudWatch.
4. Established a production endpoint by defining the model artifact, endpoint configuration, and instance count.
5. Implemented production variant traffic splitting for A/B testing and configured Auto Scaling policies.
6. Built an automated MLOps workflow using SageMaker Pipelines to evaluate model performance prior to model registry sign-off.

---

## ⚠️ Problems or Errors Encountered
* **High Data Transfer Overhead in Training:** Copying massive datasets locally via File mode caused unnecessary initialization delays and excessive disk input/output bottlenecks.
* **Unmonitored Endpoint Latency Spikes:** Sudden traffic surges caused request throttling on static single-instance inference endpoints.

---

## 🔧 How Those Problems Were Resolved
* **Input Mode Optimization:** Switched training input configurations from File mode to Pipe mode, allowing algorithms to stream data directly and eliminating bulk copy delays.
* **Dynamic Scaling Configuration:** Enabled SageMaker Auto Scaling policies on the endpoint configuration to automatically provision additional inference instances during traffic peaks and scale down during off-peak hours.

---

## 📊 Results or Output
* Fully integrated processing, training, and deployment pipeline leveraging Amazon S3 as the central data backbone.
* Production-ready endpoint supporting auto-scaling and safe rollout deployment strategies.

---

## 🤔 Lessons Learned / Reflection
Mastering the core SageMaker workflow requires understanding how S3 ties independent operations together. By decoupling data processing, distributed training, and live inference into specialized managed jobs, engineers can optimize compute costs, select appropriate input streaming modes, and automate production lifecycles seamlessly through SageMaker Pipelines.

---

## 🔗 YouTube Link(s)
* *https://youtu.be/Gy30wD0FycE*

---

## 💼 LinkedIn Post Link(s)
* *https://www.linkedin.com/posts/prajan-shrestha-7858a11b4_excited-to-share-part-12-of-my-aws-machine-share-7516159870363131904-dJUD/*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 12 Presentation Deck
* AWS Documentation: [Amazon SageMaker Developer Guide - Processing, Training, and Deployment](https://docs.aws.amazon.com/sagemaker/latest/dg/whatis.html)
