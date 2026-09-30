# CSC-6221-1 BLA - AWS Certified Machine Learning Associate Part 8

## 📌 BLA Number and Title
* **BLA Number:** BLA-08
* **Title:** AWS Certified Machine Learning Associate - Part 8: Feature Engineering & the Curse of Dimensionality

---

## 🎯 Purpose of the Activity
The primary purpose of this activity is to explore essential feature engineering techniques, understand how poor feature representation negatively impacts model performance ("garbage in, garbage out"), and analyze the Curse of Dimensionality. The lab focuses on learning how to transform raw data into informative features while employing dimensionality reduction, feature selection, and regularization strategies to prevent model degradation, overfitting, and high computational costs.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **Machine Learning Services & Libraries:** Amazon SageMaker Data Wrangler, Scikit-Learn, Pandas, NumPy
* **Core Algorithms & Techniques:** Principal Component Analysis (PCA), L1 (Lasso) / L2 (Ridge) Regularization, One-Hot Encoding, Min-Max Scaling, Standard Scaling
* **Languages & Environments:** Python 3, Jupyter Notebooks
* **Visualization Tools:** Matplotlib, Seaborn

---

## 💡 Concepts Learned
* **Feature Engineering Overview:** Leveraging domain knowledge to create, transform, or select input features for machine learning models. Feature quality often dictates performance more than algorithm selection ("garbage in, garbage out").
* **Key Feature Engineering Techniques:**
  * **Feature Creation:** Deriving new attributes from existing variables (e.g., extracting day-of-week from timestamps).
  * **Transformation & Scaling:** Rescaling numerical values onto comparable ranges (e.g., normalization/standardization).
  * **Encoding:** Mapping categorical strings into numerical formats (e.g., One-Hot Encoding, Label Encoding).
  * **Feature Selection:** Filtering out noisy, irrelevant, or redundant features.
* **The Curse of Dimensionality:** As features (dimensions) grow, the feature space volume expands exponentially, causing data points to become extremely sparse.
* **Impacts of High Dimensionality:**
  * **Data Sparsity:** Requires exponentially more training data to achieve sufficient statistical coverage.
  * **Loss of Distance Meaning:** Distance metrics (e.g., Euclidean distance in KNN or K-Means) deteriorate as points become uniformly distant from one another.
  * **Overfitting Risk:** Models tend to fit noise rather than true underlying patterns.
  * **Increased Computational Cost:** Substantially higher memory and training runtime requirements.
* **Mitigation Strategies:**
  * **Feature Selection:** Removing redundant or uninformative variables via correlation analysis or feature importance scores.
  * **Dimensionality Reduction:** Compressing high-dimensional feature spaces while preserving variance using techniques like Principal Component Analysis (PCA).
  * **Regularization:** Applying L1/L2 penalties during training to suppress less useful feature weights.

---

## 🏗️ Architecture or Design Description
The architectural pipeline demonstrates how raw input features are systematically engineered, reduced, and fed into downstream machine learning models:

```
+-----------------------------------------------------------------------------------+
|                              RAW DATASET INGESTION                                |
|             (Numerical Attributes, Categorical Features, Timestamps)              |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                           FEATURE ENGINEERING LAYER                               |
|   +-------------------+   +-------------------+   +---------------------------+   |
|   |  Feature Creation |   | Encoding (One-Hot)|   | Scaling / Normalization   |   |
|   +-------------------+   +-------------------+   +---------------------------+   |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                        DIMENSIONALITY CONTROL LAYER                               |
|   +---------------------------------------+   +-------------------------------+   |
|   |   Feature Selection (Correlation/Scores)|   | PCA (Dimensionality Reduction)|   |
|   +---------------------------------------+   +-------------------------------+   |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                     OPTIMIZED MODEL TRAINING & REGULARIZATION                     |
|                   (Amazon SageMaker / Scikit-Learn + L1/L2)                       |
+-----------------------------------------------------------------------------------+
```

---

## 📋 Major Steps Completed
1. Executed data preprocessing steps including One-Hot Encoding for categorical variables and feature scaling for continuous numerical attributes.
2. Created composite interaction terms and extracted datetime components from raw timestamp columns.
3. Demonstrated the Curse of Dimensionality by tracking the exponential expansion of the feature space relative to constant data sample sizes.
4. Applied Principal Component Analysis (PCA) to compress high-dimensional feature sets into orthogonal components while retaining key variance.
5. Evaluated model accuracy and training performance before and after applying feature selection, PCA, and L1/L2 regularization penalties.

---

## ⚠️ Problems or Errors Encountered
* **Multicollinearity & Overfitting:** One-Hot Encoding high-cardinality categorical variables generated thousands of sparse columns, causing model overfitting and poor generalization.
* **Distance Metric Degradation:** Distance-based models (such as K-Means) failed to form meaningful clusters when raw, unscaled high-dimensional features were supplied directly.

---

## 🔧 How Those Problems Were Resolved
* **Cardinality Reduction & Feature Selection:** Grouped rare categories into broader bins before encoding and used L1 regularization (Lasso) alongside PCA to trim zero-importance feature dimensions.
* **Standardization & PCA Pipelines:** Applied standard scaling (`StandardScaler`) prior to PCA transformation, ensuring all features contributed equally to variance calculations and restoring meaningful distance calculations.

---

## 📊 Results or Output
* Cleaned, encoded, and standardized dataset optimized for machine learning training.
* Significant reduction in feature dimensions via PCA while maintaining over 90%+ explained variance.
* Improved model generalization with reduced training times and lower evaluation error rates.

---

## 🤔 Lessons Learned / Reflection
More features do not automatically equate to better models. Unchecked feature creation rapidly triggers the Curse of Dimensionality, leading to data sparsity, noise fitting, and computational bottlenecks. Successful machine learning relies on striking a balance—using feature engineering to craft meaningful inputs while leveraging feature selection, PCA, and regularization to keep dimensions lean and effective.

---

## 🔗 YouTube Link(s)
* *[Insert your YouTube presentation/lab video link here]*

---

## 💼 LinkedIn Post Link(s)
* *[Insert your LinkedIn project/reflection post link here]*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 8 Presentation Deck
* AWS Documentation: [Feature Engineering with Amazon SageMaker Data Wrangler](https://docs.aws.amazon.com/sagemaker/latest/dg/data-wrangler.html)
* Scikit-Learn Documentation: [Preprocessing and Dimensionality Reduction](https://scikit-learn.org/stable/modules/decomposition.html)
