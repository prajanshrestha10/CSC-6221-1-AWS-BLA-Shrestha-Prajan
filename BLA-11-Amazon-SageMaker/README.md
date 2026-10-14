# CSC-6221-1 BLA - Amazon SageMaker

## 📌 BLA Number and Title
* **BLA Number:** BLA-11
* **Title:** AWS Certified Machine Learning Associate - Part 11: Amazon SageMaker (Build, Train & Deploy ML Models, Fully Managed)

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to explore Amazon SageMaker (also known as Amazon SageMaker AI) as a fully managed machine learning platform that covers the entire ML lifecycle from data preparation to production deployment and monitoring. The lab focuses on leveraging SageMaker tools for building, training, tuning, deploying, and automating scalable machine learning workflows without managing underlying server infrastructure.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **AWS Machine Learning Platform:** Amazon SageMaker (Studio, Data Wrangler, Feature Store, Ground Truth, Autopilot, JumpStart, Canvas, Model Monitor, Clarify, Model Registry, Pipelines)
* **Compute & Storage Integrations:** Amazon S3, AWS IAM, Amazon CloudWatch
* **Frameworks & Algorithms:** XGBoost, PyTorch, Custom Containers
* **Languages & Environments:** Python, Jupyter Notebooks

---

## 💡 Concepts Learned
* **Fully Managed ML Platform:** SageMaker abstracts away server maintenance, scaling, and infrastructure provisioning, allowing practitioners to focus entirely on model development.
* **The Machine Learning Lifecycle:**
  * **Prepare:** Cleaning and labeling data using tools like Data Wrangler and Ground Truth.
  * **Build:** Exploring and writing code inside web-based environments like SageMaker Studio.
  * **Train:** Fitting models using managed training jobs, built-in algorithms, or custom frameworks.
  * **Tune:** Improving model performance automatically using hyperparameter tuning and managed spot training.
  * **Deploy:** Serving predictions via Real-Time Endpoints, Serverless Inference, Asynchronous Inference, or Batch Transform.
  * **Monitor:** Tracking data drift, model bias, and versioning through Model Monitor, Clarify, and Model Registry.
* **Inference Options:**
  * *Real-Time Endpoints:* Always-on, low-latency predictions (ideal for fraud detection).
  * *Serverless Inference:* Scales automatically to zero during idle periods for bursty workloads.
  * *Asynchronous Inference:* Queues requests for large payloads and long processing times.
  * *Batch Transform:* Processes predictions over entire datasets without maintaining a running endpoint.
* **Accelerated Shortcuts:**
  * *Autopilot:* Automated AutoML that tests various algorithms and settings.
  * *JumpStart:* Hub of pretrained foundation models and ready-made solutions.
  * *Canvas:* No-code, point-and-click interface for business analysts.

---

## 🏗️ Architecture or Design Description
The SageMaker MLOps lifecycle pipeline architecture illustrates how data flows through managed AWS components from preparation to inference and monitoring:

```
+-----------------------------------------------------------------------------------+
|                        1. PREPARE & BUILD (SageMaker Studio)                      |
|           (Data Wrangler, Feature Store, Ground Truth Data Labeling)              |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                          2. TRAIN & TUNE (Managed Jobs)                           |
|        (Amazon S3 Data Input -> XGBoost/PyTorch/Spot Instances -> Model Output)   |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                       3. DEPLOY INFERENCE (Prediction Options)                    |
|   +-------------------+  +-------------------+  +-----------------------------+   |
|   | Real-Time Endpoint|  | Serverless/Async  |  | Batch Transform (S3 to S3)  |   |
|   +-------------------+  +-------------------+  +-----------------------------+   |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                         4. MONITOR & AUTOMATE (MLOps)                             |
|           (Model Monitor, Clarify Bias Detection, Model Registry, Pipelines)      |
+-----------------------------------------------------------------------------------+
```

---

## 📋 Major Steps Completed
1. Provisioned a SageMaker Studio environment and utilized Data Wrangler for visual data inspection and feature transformation.
2. Configured and executed a managed training job pointing to training datasets stored in Amazon S3.
3. Implemented Automatic Model Tuning to optimize hyperparameters and reduce training costs using Managed Spot Training.
4. Deployed a trained model to a Real-Time Endpoint and evaluated alternative deployment options including Serverless and Batch Transform.
5. Established monitoring pipelines using Model Monitor and Clarify to track data drift and ensure model fairness.

---

## ⚠️ Problems or Errors Encountered
* **High Infrastructure Costs on Idle Endpoints:** Leaving real-time inference endpoints running continuously during development incurred unnecessary hourly charges.
* **Hyperparameter Tuning Bottlenecks:** Running extensive hyperparameter searches manually consumed excessive time and compute resources.

---

## 🔧 How Those Problems Were Resolved
* **Deployment Optimization:** Switched non-production development endpoints to Serverless Inference or deleted idle endpoints when not in active testing, relying on Batch Transform for offline evaluations.
* **Automated Tuning:** Leveraged SageMaker's built-in Automatic Model Tuning capability to execute parallel trials efficiently and automatically shut down underperforming training jobs.

---

## 📊 Results or Output
* Fully operational end-to-end MLOps pipeline covering data preparation, managed training, automated tuning, and model deployment.
* Cost-effective inference endpoints tailored to specific latency and traffic patterns.

---

## 🤔 Lessons Learned / Reflection
Amazon SageMaker successfully eliminates the operational burden of managing underlying machine learning infrastructure by providing an integrated, fully managed platform for the entire ML lifecycle. By combining robust MLOps tools like Model Monitor and Pipelines with developer shortcuts like Autopilot and JumpStart, teams can build, test, and scale production-grade machine learning solutions rapidly and cost-effectively.

---

## 🔗 YouTube Link(s)
* *https://youtu.be/WKyTeoDDTYg*

---

## 💼 LinkedIn Post Link(s)
* *https://www.linkedin.com/feed/update/urn:li:activity:7516154498197671936/*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 11 Presentation Deck
* AWS Documentation: [Amazon SageMaker Developer Guide](https://docs.aws.amazon.com/sagemaker/latest/dg/whatis.html)
