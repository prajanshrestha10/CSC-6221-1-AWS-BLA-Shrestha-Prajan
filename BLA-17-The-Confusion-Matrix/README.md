# CSC-6221-1 BLA - The Confusion Matrix

## 📌 BLA Number and Title
* **BLA Number:** BLA-17
* **Title:** AWS Certified Machine Learning Associate - Part 17: The Confusion Matrix (How a Classifier Is Right and Wrong)

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to examine the mechanics of classification evaluation using the Confusion Matrix and its derived performance metrics. The lab focuses on deconstructing the four fundamental outcomes (True Positives, True Negatives, False Positives, and False Negatives), calculating key metrics like Precision, Recall, Specificity, and F1-Score, avoiding the "Accuracy Trap" in imbalanced datasets, adjusting classification thresholds via ROC curves, and interpreting multi-class matrices in Amazon SageMaker.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **AWS Machine Learning Platform:** Amazon SageMaker (Autopilot model reports, Model Monitor model quality checks)
* **Evaluation Frameworks & Metrics:** Confusion Matrix, Accuracy, Precision, Recall (Sensitivity), Specificity, F1-Score, ROC Curve, AUC
* **Languages & Environments:** Python, Jupyter Notebooks, Scikit-Learn (`confusion_matrix`, `classification_report`, `roc_auc_score`)

---

## 💡 Concepts Learned
* **What Is a Confusion Matrix?** A tabular layout comparing model predictions against actual reality. Rows represent actual classes, while columns represent predicted classes.
* **The Four Core Outcomes:**
  * **True Positive (TP):** Correctly predicted positive outcome (e.g., flagged fraud and it was actual fraud).
  * **True Negative (TN):** Correctly predicted negative outcome (e.g., passed a legitimate transaction and it was legitimate).
  * **False Positive (FP / Type I Error):** False alarm (e.g., flagged as fraud, but it was legitimate).
  * **False Negative (FN / Type II Error):** Missed detection (e.g., passed as legitimate, but it was actual fraud).
* **Derived Performance Metrics:**
  * *Accuracy:* Overall correctness ratio ($\frac{TP + TN}{Total}$).
  * *Precision:* Out of all positive predictions, how many were correct ($\frac{TP}{TP + FP}$).
  * *Recall (Sensitivity):* Out of all actual positives, how many were caught ($\frac{TP}{TP + FN}$).
  * *Specificity:* Out of all actual negatives, how many were passed ($\frac{TN}{TN + FP}$).
  * *F1-Score:* Harmonic mean balancing Precision and Recall ($2 \times \frac{Precision \times Recall}{Precision + Recall}$).
* **The Accuracy Trap:** High accuracy can mask a completely useless model when classes are severely imbalanced (e.g., a lazy model predicting "not fraud" 99% of the time achieves 99% accuracy with 0% recall).
* **Choosing the Right Metric Based on Error Costs:**
  * *Optimize Recall:* When missing real cases is costly (e.g., disease screening, fraud detection).
  * *Optimize Precision:* When false alarms are costly (e.g., spam filters hiding legitimate emails).
  * *Use F1-Score:* When a balance of both errors is required.
  * *Use Accuracy:* When classes are balanced and error costs are equal.
* **Thresholds & the ROC Curve:** Lowering the classification threshold increases Recall while decreasing Precision; raising it increases Precision while decreasing Recall. The ROC curve plots the True Positive Rate against the False Positive Rate across all thresholds, summarized by AUC.
* **Multi-Class Matrices in SageMaker:** Expands the grid to $N \times N$, where the diagonal represents correct predictions and off-diagonal cells highlight misclassifications. Row normalization helps compare imbalanced classes in SageMaker Autopilot reports and Model Monitor checks.

---

## 🏗️ Architecture or Design Description
The evaluation pipeline maps model prediction probabilities through classification thresholds into a confusion matrix and downstream decision metrics:
```
+-----------------------------------------------------------------------------------+
|                        MODEL PREDICTION PROBABILITIES                             |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                     CLASSIFICATION THRESHOLD APPLICATION                          |
|                  (Default = 0.5; Adjustable for Recall/Precision)                 |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                            THE CONFUSION MATRIX GRID                              |
|         +-----------------------+-----------------------+                         |
|         |    True Positive (TP) |   False Negative (FN) |                         |
|         +-----------------------+-----------------------+                         |
|         |   False Positive (FP) |    True Negative (TN) |                         |
|         +-----------------------+-----------------------+                         |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                        PERFORMANCE METRICS & ROC EVALUATION                       |
|           (Precision, Recall, F1-Score, Specificity, AUC-ROC Curve)               |
+-----------------------------------------------------------------------------------+
```
---

## 📋 Major Steps Completed
1. Generated confusion matrices for binary and multi-class classification models to separate correct predictions from error types.
2. Calculated Accuracy, Precision, Recall, Specificity, and F1-Score manually and programmatically using confusion matrix cell counts.
3. Demonstrated the limitations of standard accuracy by evaluating a baseline "lazy model" against an imbalanced dataset.
4. Adjusted classification probability thresholds to optimize recall versus precision based on business error costs.
5. Plotted ROC curves and computed AUC metrics to evaluate model discrimination across all decision thresholds.
6. Interpreted multi-class confusion matrices and normalized row percentages within SageMaker Autopilot and Model Monitor reports.

---

## ⚠️ Problems or Errors Encountered
* **Misleading Model Validation:** Relying solely on validation accuracy reported 99.4% performance, obscuring the fact that the model missed critical positive minority instances (high false negatives).
* **Threshold Mismatch:** Default classification thresholds (0.5) yielded unacceptable false alarm rates in high-cost fraud detection scenarios.

---

## 🔧 How Those Problems Were Resolved
* **Metric Realignment:** Shifted evaluation protocols away from raw accuracy toward **Recall**, **Precision**, and **F1-Score** to reflect true model utility.
* **Threshold Tuning:** Lowered the classification probability threshold to increase detection sensitivity (Recall) and catch high-risk positive events.

---

## 📊 Results or Output
* Comprehensive confusion matrix evaluation revealing true positive capture rates and specific error distributions (False Positives vs. False Negatives).
* Threshold-optimized classifier configured for maximum recall in high-risk detection environments.

---

## 🤔 Lessons Learned / Reflection
Accuracy alone is a dangerous metric for evaluating classifiers, especially when dealing with imbalanced datasets. The confusion matrix provides complete visibility into model behavior by breaking down results into True Positives, True Negatives, False Positives, and False Negatives. By selecting the appropriate metric (Precision, Recall, or F1-Score) and tuning classification thresholds to match error costs, practitioners build honest, reliable machine learning solutions.

---

## 🔗 YouTube Link(s)
* *[Insert your YouTube presentation/lab video link here]*

---

## 💼 LinkedIn Post Link(s)
* *[Insert your LinkedIn project/reflection post link here]*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 17 Presentation Deck
* AWS Documentation: [Amazon SageMaker Model Monitor Quality Metrics](https://docs.aws.amazon.com/sagemaker/latest/dg/model-monitor.html)
* Scikit-Learn Documentation: [Metrics and Confusion Matrix Evaluation](https://scikit-learn.org/stable/modules/model_evaluation.html)
