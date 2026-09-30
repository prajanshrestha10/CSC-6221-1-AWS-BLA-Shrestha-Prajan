# CSC-6221-1 BLA - AWS Certified Machine Learning Associate Part 9

## 📌 BLA Number and Title
* **BLA Number:** BLA-09
* **Title:** AWS Certified Machine Learning Associate - Part 9: Missing & Unbalanced Data

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to analyze two critical data quality challenges in machine learning: missing data and class imbalance. The lab focuses on evaluating why missingness occurs, selecting optimal imputation strategies (deletion, mean/median fill, forward/backward fill, or predictive imputation), addressing severe class distribution skews, avoiding the "accuracy trap," and evaluating models using robust performance metrics like Precision, Recall, F1-Score, and AUC-ROC.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **Machine Learning Services & Libraries:** Amazon SageMaker Data Wrangler, Scikit-Learn, Imbalanced-Learn (`imblearn`), Pandas, NumPy
* **Resampling & Imputation Algorithms:** SMOTE (Synthetic Minority Over-sampling Technique), Random Oversampling/Undersampling, KNNImputer, SimpleImputer
* **Languages & Environments:** Python 3, Jupyter Notebooks
* **Evaluation Metrics:** Precision, Recall, F1-Score, AUC-ROC Curve, Confusion Matrix

---

## 💡 Concepts Learned
* **Causes of Missing Data:** Sensor or equipment failures, optional user inputs, dataset merging gaps, and privacy redactions.
* **Missing Data Imputation Strategies:**
  * **Deletion:** Dropping sparse rows or columns; optimal when missingness is minimal and random.
  * **Mean/Median/Mode Imputation:** Substituting missing values with statistical central tendencies; best for numerical/categorical variables missing at random.
  * **Forward/Backward Fill:** Propagating prior or subsequent values; essential for ordered time-series datasets.
  * **Predictive Imputation:** Leveraging Machine Learning models (e.g., Regression, KNN) to estimate missing values when missingness relates to other features.
* **The Imbalanced Data Challenge & Accuracy Trap:**
  * In classification scenarios (e.g., fraud detection with a 99:1 legitimate-to-fraud ratio), a naive model predicting only the majority class achieves 99% accuracy while failing to detect any minority targets. Standard accuracy creates a false sense of performance.
* **Techniques for Resolving Class Imbalance:**
  * **Oversampling & SMOTE:** Duplicating minority instances or generating synthetic data points along line segments connecting existing minority samples.
  * **Undersampling:** Trimming down majority class records to level class distributions.
  * **Class Weighting:** Modifying model loss functions to penalize misclassifications of minority class instances heavily.
  * **Data Augmentation:** Gathering additional real-world minority examples where practical.
* **Superior Evaluation Metrics:**
  * **Precision:** Ratio of true positive predictions out of all positive predictions made ($TP / (TP + FP)$).
  * **Recall:** Ratio of true positive predictions out of all actual positive instances ($TP / (TP + FN)$).
  * **F1-Score:** Harmonic mean balancing Precision and Recall ($2 \times \frac{Precision \times Recall}{Precision + Recall}$).
  * **AUC-ROC:** Evaluates model class separation capability across all classification probability thresholds.

---

## 🏗️ Architecture or Design Description
The data cleaning and rebalancing pipeline illustrates how missing attributes are restored and target classes are rebalanced prior to model evaluation:

```
+-----------------------------------------------------------------------------------+
|                            RAW DATASET INGESTION                                  |
|            (Incomplete Datasets & Imbalanced Class Distributions)                 |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                             MISSING DATA IMPUTATION                               |
|   +-----------------------+   +-----------------------+   +-------------------+   |
|   | Deletion / Filtering  |   | Mean/Median/Mode Fill |   | Predictive (KNN)  |   |
|   +-----------------------+   +-----------------------+   +-------------------+   |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                             CLASS REBALANCING LAYER                               |
|   +-----------------------+   +-----------------------+   +-------------------+   |
|   | Synthetic SMOTE Fill  |   | Random Undersampling  |   | Class Weighting   |   |
|   +-----------------------+   +-----------------------+   +-------------------+   |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                         BALANCED MODEL TRAINING & EVALUATION                      |
|                  (Evaluated via Precision, Recall, F1, AUC-ROC)                   |
+-----------------------------------------------------------------------------------+
```

---

## 📋 Major Steps Completed
1. Identified missing data mechanisms across features and evaluated information loss across deletion versus statistical imputation strategies.
2. Implemented median imputation for skewed continuous fields, mode imputation for categorical attributes, and predictive KNN imputation for interrelated variables.
3. Quantified class skew in a binary classification dataset and demonstrated how standard accuracy obscures minority class prediction failure.
4. Synthesized minority class samples using SMOTE (`imblearn.over_sampling.SMOTE`) and applied cost-sensitive class weighting directly within estimator parameters.
5. Generated confusion matrices, precision-recall curves, and ROC curves to demonstrate objective model performance improvements.

---

## ⚠️ Problems or Errors Encountered
* **Data Leakage during Resampling:** Applying SMOTE to the entire dataset prior to train-test splitting contaminated test data with synthetic information, leading to artificially inflated test metrics.
* **Distorted Time Series Integrity:** Applying mean imputation or random dropping to time-dependent sequence data disrupted seasonal trends and temporal continuity.

---

## 🔧 How Those Problems Were Resolved
* **Pipeline Encapsulation:** Integrated SMOTE inside an `imblearn.pipeline.Pipeline` object to ensure oversampling was applied strictly to training folds during cross-validation, keeping testing data completely unobserved.
* **Temporal-Aware Imputation:** Replaced static statistical imputation with Forward/Backward filling (`ffill`/`bfill`) on time series columns to preserve temporal ordering.

---

## 📊 Results or Output
* Completely clean dataset free of missing values without incurring unneeded row loss.
* Balanced training dataset via SMOTE, shifting minority class representation to equal proportions.
* Substantial increase in minority-class Recall and overall F1-score compared to baseline models evaluated on raw imbalanced distributions.

---

## 🤔 Lessons Learned / Reflection
High model accuracy is often misleading when working with real-world datasets affected by missing records or severe class imbalances. Choosing the appropriate imputation strategy prevents data loss, while applying synthetic oversampling (SMOTE) or class weighting ensures that minority events are caught. Evaluating performance through Precision, Recall, F1-Score, and AUC-ROC provides an accurate measure of model quality.

---

## 🔗 YouTube Link(s)
* *[Insert your YouTube presentation/lab video link here]*

---

## 💼 LinkedIn Post Link(s)
* *[Insert your LinkedIn project/reflection post link here]*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 9 Presentation Deck
* AWS Documentation: [Handle Missing Values and Imbalanced Data in Amazon SageMaker Data Wrangler](https://docs.aws.amazon.com/sagemaker/latest/dg/data-wrangler.html)
* Scikit-Learn Documentation: [Impute Missing Values](https://scikit-learn.org/stable/modules/impute.html)
* Imbalanced-Learn Documentation: [User Guide for Over-sampling & SMOTE](https://imbalanced-learn.org/stable/user_guide.html)
