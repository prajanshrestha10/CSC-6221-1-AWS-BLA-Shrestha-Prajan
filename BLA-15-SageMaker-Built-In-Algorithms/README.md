# CSC-6221-1 BLA - SageMaker Built-In Algorithms

## 📌 BLA Number and Title
* **BLA Number:** BLA-15
* **Title:** AWS Certified Machine Learning Associate - Part 15: SageMaker Built-In Algorithms (Ready-to-Use Machine Learning, Without the Training Code)

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to explore Amazon SageMaker's ready-to-use built-in algorithms, which eliminate the need to write custom training code for standard machine learning patterns. The lab focuses on classifying supervised, unsupervised, text, forecasting, and vision algorithms, configuring data formats (such as RecordIO-protobuf and CSV), matching specific business problems to the appropriate algorithm, and evaluating when to use built-in algorithms versus custom scripts or SageMaker JumpStart.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **AWS Machine Learning Platform:** Amazon SageMaker, SageMaker JumpStart, Automatic Model Tuning
* **Supervised Algorithms:** XGBoost, Linear Learner, K-Nearest Neighbors (k-NN), Factorization Machines
* **Unsupervised & Anomaly Algorithms:** K-Means, Principal Component Analysis (PCA), Random Cut Forest, Latent Dirichlet Allocation (LDA), Neural Topic Model, IP Insights
* **Text, Forecasting & Vision Algorithms:** BlazingText, Seq2Seq, DeepAR, Image Classification, Object Detection
* **Storage & Data Formats:** Amazon S3, CSV, RecordIO-protobuf
* **Languages & Frameworks:** Python, Jupyter Notebooks

---

## 💡 Concepts Learned
* **What Are Built-In Algorithms?** Pre-implemented, highly optimized machine learning algorithms packaged by AWS into Docker containers, enabling users to train models without writing custom training code while supporting distributed training on large datasets.
* **Supervised Algorithms (Learning from Labels):**
  * *XGBoost:* Gradient boosted trees; a top choice for tabular regression and classification.
  * *Linear Learner:* Linear models for regression and classification; fast and serves as a strong baseline.
  * *k-NN:* Predicts outcomes based on the closest examples in the training data.
  * *Factorization Machines:* Designed for sparse datasets, such as recommendation engines and click prediction.
* **Unsupervised & Anomaly Detection Algorithms (Finding Structure):**
  * *K-Means:* Groups similar points into clusters (e.g., customer segmentation).
  * *PCA:* Reduces feature dimensionality while retaining maximum variance.
  * *Random Cut Forest:* Detects anomalies and outliers (e.g., fraudulent transactions, sensor spikes).
  * *LDA & Neural Topic Model:* Discovers underlying topics across document collections.
  * *IP Insights:* Flags suspicious behavior around IP addresses.
* **Text, Forecasting & Vision Algorithms:**
  * *BlazingText:* Generates word embeddings and performs fast text classification.
  * *Seq2Seq:* Transforms input sequences into output sequences (translation, summarization).
  * *DeepAR:* Time-series forecasting that learns from many related time series simultaneously.
  * *Computer Vision:* Handles image classification, object detection, and semantic segmentation.
* **Algorithm Selection Guidelines:**
  * Predicting a number or category from tabular data $\rightarrow$ **XGBoost / Linear Learner**.
  * Grouping similar items without labels $\rightarrow$ **K-Means**.
  * Managing high-dimensional features $\rightarrow$ **PCA**.
  * Detecting unusual data points $\rightarrow$ **Random Cut Forest**.
  * Forecasting future time-series values $\rightarrow$ **DeepAR**.
* **Built-In vs. Custom Code vs. JumpStart:**
  * *Built-In Algorithm:* Best when facing a standard problem and needing a quick, optimized start.
  * *Custom Script or Container:* Required when implementing specialized logic or custom model architectures.
  * *SageMaker JumpStart:* Ideal for starting from pre-trained foundation models.

---

## 🏗️ Architecture or Design Description
The structured workflow for training and deploying a SageMaker built-in algorithm demonstrates the pipeline from algorithm selection to endpoint hosting:

```
+-----------------------------------------------------------------------------------+
|                        1. DATA PREPARATION (Amazon S3)                            |
|             (Format data into CSV or RecordIO-protobuf, store in S3)              |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                          2. ALGORITHM SELECTION & CONFIG                          |
|         (Pick Built-In Container -> Set Hyperparameters -> Configure Instance)    |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                          3. MANAGED TRAINING & TUNING                             |
|              (Automatic Model Tuning -> Train Model -> Save to S3)                |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                           4. HOSTING & INFERENCE ENDPOINT                         |
|                 (Deploy trained model artifact to a live endpoint)                |
+-----------------------------------------------------------------------------------+
```

---

## 📋 Major Steps Completed
1. Formulated machine learning problem statements and matched them to appropriate SageMaker built-in algorithms (e.g., XGBoost for tabular data, DeepAR for forecasting).
2. Processed and formatted training datasets into CSV and RecordIO-protobuf formats, uploading them to Amazon S3 buckets.
3. Configured training jobs by selecting pre-built algorithm container images, instance types, and initial hyperparameter bounds.
4. Integrated Automatic Model Tuning with built-in algorithms to optimize hyperparameters across parallel training trials.
5. Deployed trained models to production inference endpoints and evaluated their predictive performance.

---

## ⚠️ Problems or Errors Encountered
* **Data Format Mismatch (`RecordIO-protobuf` Errors):** Attempting to pass raw unstructured CSV files directly into algorithms optimized exclusively for RecordIO-protobuf caused training job initialization failures.
* **GPU Instance Resource Allocation Failures:** Selecting CPU instances for image classification and computer vision training jobs resulted in prolonged training times and memory bottlenecks.

---

## 🔧 How Those Problems Were Resolved
* **Data Serialization & Pipe Mode:** Converted input datasets into the required RecordIO-protobuf serialization format using conversion scripts and leveraged SageMaker Pipe mode to stream data efficiently from S3.
* **Instance Type Alignment:** Updated training configuration settings to provision GPU-backed EC2 instances (e.g., `p3` or `g4dn` families) for vision models while retaining cost-effective CPU instances for tabular algorithms like XGBoost.

---

## 📊 Results or Output
* High-performance machine learning models trained rapidly without writing underlying training code.
* Optimized inference endpoints hosting specialized algorithms ranging from anomaly detection to time-series forecasting.

---

## 🤔 Lessons Learned / Reflection
SageMaker built-in algorithms drastically accelerate the machine learning development lifecycle by providing pre-packaged, highly optimized containers for common modeling tasks. Rather than writing custom training scripts from scratch, practitioners can focus on proper data preparation, format serialization, and hyperparameter tuning to achieve production-grade performance quickly.

---

## 🔗 YouTube Link(s)
* *[Insert your YouTube presentation/lab video link here]*

---

## 💼 LinkedIn Post Link(s)
* *[Insert your LinkedIn project/reflection post link here]*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 15 Presentation Deck
* AWS Documentation: [Amazon SageMaker Built-In Algorithms](https://docs.aws.amazon.com/sagemaker/latest/dg/algos.html)
