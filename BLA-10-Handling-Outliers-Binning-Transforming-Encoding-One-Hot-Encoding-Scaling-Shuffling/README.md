# CSC-6221-1 BLA - Data Preparation Techniques

## 📌 BLA Number and Title
* **BLA Number:** BLA-10
* **Title:** AWS Certified Machine Learning Associate - Part 10: Data Preparation Techniques (Outliers, Binning, Transforming, Encoding, Scaling & Shuffling)

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to explore and implement comprehensive data preparation and preprocessing techniques essential for machine learning model performance. The lab focuses on detecting and handling outliers, binning continuous data, correcting skewed distributions via transformations, encoding categorical text into numeric formats, scaling features to comparable ranges, and shuffling rows to prevent positional bias.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **Machine Learning Services & Libraries:** Amazon SageMaker Data Wrangler, Scikit-Learn, Pandas, NumPy
* **Core Techniques:** Z-Score & IQR Outlier Detection, Equal-Width & Quantile Binning, Log/Square Root/Box-Cox Transformations, Label & One-Hot Encoding, Min-Max Normalization & Z-Score Standardization, Row Shuffling
* **Languages & Environments:** Python 3, Jupyter Notebooks
* **Visualization Tools:** Matplotlib, Seaborn, Box Plots, Histograms

---

## 💡 Concepts Learned
* **Handling Outliers:** Identifying data points that sit far from the rest using the Z-Score method ($\vert{}z\vert{} > 3$) or IQR method ($Q1 - 1.5 \times IQR$ to $Q3 + 1.5 \times IQR$). Options include removal, capping/Winsorizing, transforming, or retaining them if they represent valuable signals (e.g., fraudulent transactions).
* **Binning:** Grouping continuous variables into discrete buckets using equal-width ranges or quantiles to reduce noise, soften outliers, and capture non-linear patterns.
* **Transforming:** Applying mathematical operations like Logarithmic, Square Root, or Box-Cox transformations to correct heavy right-skewed distributions and pull extreme values closer.
* **Encoding:** Converting text categories into numbers. Label/Ordinal encoding assigns single integers when a clear order exists, while One-Hot encoding treats unordered categories equally by creating binary columns for each category.
* **Scaling:** Adjusting numeric features to comparable ranges. Normalization (Min-Max) squeezes values between 0 and 1 (vital for KNN, SVM, neural networks), while Standardization (Z-Score) centers data around a mean of 0 with a standard deviation of 1. Scalers must be fit only on training data to prevent data leakage.
* **Shuffling:** Randomizing row positions before train-validation splits to ensure fair learning and eliminate position-based patterns (with the exception of time series data where temporal order matters).

---

## 🏗️ Architecture or Design Description
The standard sequential data preparation pipeline illustrates the recommended order of preprocessing operations:

```
+-----------------------------------------------------------------------------------+
|                              RAW DATASET INGESTION                                |
|        (Raw Attributes, Skewed Distributions, Text Labels, Outliers)              |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                            1. OUTLIER INVESTIGATION                               |
|                     (Detect via Z-Score / IQR -> Remove or Cap)                   |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                            2. FEATURE TRANSFORMATION                              |
|                     (Apply Log, Square Root, or Box-Cox for Skew)                 |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                                  3. BINNING                                       |
|                    (Group Continuous Data into Quantile / Width Buckets)          |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                                  4. ENCODING                                      |
|                  (Apply One-Hot Encoding or Label Encoding for Text)              |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                                  5. SCALING                                       |
|               (Min-Max Normalization or Z-Score Standardization on Train Only)    |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                                  6. SHUFFLING                                     |
|              (Randomize Row Order for Fair Splits - Exclude Time Series)          |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                       FULLY PREPARED DATASET FOR MODEL TRAINING                   |
+-----------------------------------------------------------------------------------+
```

---

## 📋 Major Steps Completed
1. Inspected numerical columns for anomalies using Z-Score and Interquartile Range (IQR) boundary checks.
2. Applied log and square root transformations to flatten right-skewed feature distributions.
3. Implemented quantile and equal-width binning strategies on continuous numerical attributes.
4. Converted categorical text columns into numerical representations using One-Hot Encoding to avoid false ordinal assumptions.
5. Scaled continuous features using Min-Max scaling and Z-score standardization, ensuring scalers were fitted strictly on training subsets.
6. Shuffled dataset records prior to split validation to prevent positional learning.

---

## ⚠️ Problems or Errors Encountered
* **Data Leakage during Scaling:** Fitting the StandardScaler or MinMaxScaler across the entire dataset prior to splitting contaminated training metrics with test distribution characteristics.
* **Dimensionality Explosion via One-Hot Encoding:** Encoding a high-cardinality categorical column generated hundreds of sparse new columns, slowing down training and increasing memory overhead.

---

## 🔧 How Those Problems Were Resolved
* **Pipeline Encapsulation:** Configured Scikit-Learn `Pipeline` objects to ensure scaling parameters were computed exclusively on training folds and subsequently applied to validation/test sets.
* **Cardinality Filtering:** Grouped infrequent categories into a generic "Other" bucket and dropped redundant binary dummy columns to keep feature dimensionality manageable.

---

## 📊 Results or Output
* Cleaned, transformed, and normalized dataset free of extreme skew and scaling bias.
* Fair and randomized train/validation splits optimized for stable model convergence.

---

## 🤔 Lessons Learned / Reflection
Data preparation is not a rigid checklist but a thoughtful, sequential process. Blindly deleting outliers can discard vital anomaly signals, while failing to isolate scaler fitting leads to subtle data leakage that ruins generalization. Proper transformation, encoding, and scaling lay an honest foundation for high-performing machine learning models.

---

## 🔗 YouTube Link(s)
* *https://youtu.be/Un2YOX6TyrM*

---

## 💼 LinkedIn Post Link(s)
* *https://www.linkedin.com/feed/update/urn:li:activity:7515965883303944192/*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 10 Presentation Deck
* AWS Documentation: [Data Preparation with Amazon SageMaker Data Wrangler](https://docs.aws.amazon.com/sagemaker/latest/dg/data-wrangler.html)
* Scikit-Learn Documentation: [Preprocessing Data](https://scikit-learn.org/stable/modules/preprocessing.html)
