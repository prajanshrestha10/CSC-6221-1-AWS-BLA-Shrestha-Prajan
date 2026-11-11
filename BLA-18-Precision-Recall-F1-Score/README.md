# CSC-6221-1 BLA - Precision, Recall & F1-Score

## 📌 BLA Number and Title
* **BLA Number:** BLA-18
* **Title:** AWS Certified Machine Learning Associate - Part 18: Precision, Recall & F1-Score (Building Real Intuition for Classification Metrics)

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to explore classification evaluation metrics, specifically Precision, Recall, F1-Score, and the parameterized $F_\beta$ family. The lab focuses on analyzing the trade-offs between precision and recall using a practical spam filter scenario, understanding why harmonic means are required over simple averages, evaluating multi-class averaging methods (Macro, Micro, and Weighted), and configuring custom metric optimization targets within Amazon SageMaker algorithms like Linear Learner and Automatic Model Tuning.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **AWS Machine Learning Platform:** Amazon SageMaker (Linear Learner, Automatic Model Tuning, Hyperparameter Optimization Objectives)
* **Classification Evaluation Metrics:** Precision, Recall (Sensitivity / True Positive Rate), F1-Score, $F_\beta$-Score ($F_{0.5}, F_{2}$), Macro / Micro / Weighted Averaging
* **Languages & Frameworks:** Python 3, Scikit-Learn (`precision_score`, `recall_score`, `f1_score`, `fbeta_score`, `classification_report`), Pandas, NumPy

---

## 💡 Concepts Learned
* **Precision (Trustworthiness of Positive Predictions):**
  * *Question:* When the model predicts the positive class, how often is it actually right?
  * *Formula:* $\frac{TP}{TP + FP}$
  * *Focus:* Measures sensitivity to False Positives (false alarms). Crucial when false alarms are high-cost (e.g., spam filtering burying legitimate emails).
* **Recall (Detection Rate / Sensitivity):**
  * *Question:* Out of all actual positive cases in reality, how many did the model catch?
  * *Formula:* $\frac{TP}{TP + FN}$
  * *Focus:* Measures sensitivity to False Negatives (misses). Crucial when missing positive cases is dangerous or high-cost (e.g., medical diagnostics, fraud detection).
* **The Precision-Recall Trade-Off:**
  * *Conservative Threshold (High Threshold):* Only flags the most certain cases $\rightarrow$ Precision reaches $100\%$, but Recall plummets.
  * *Aggressive Threshold (Low Threshold):* Flags almost every case $\rightarrow$ Recall reaches $100\%$, but Precision plummets due to false alarms.
  * *Balance:* Classification thresholds must be dynamically adjusted depending on business risk tolerance.
* **F1-Score (The Harmonic Mean):**
  * *Formula:* $F1 = 2 \times \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}} = \frac{2TP}{2TP + FP + FN}$
  * *Why Harmonic Mean?* Unlike an arithmetic average (which can yield artificially high scores when one metric is near zero and the other is $100\%$), the harmonic mean severely penalizes extreme imbalances, requiring both precision and recall to be high for a strong score.
* **$F_\beta$-Score (Customizing Metric Weighting):**
  * *Formula Parameter ($\beta$):* Controls how much more weight is placed on Recall relative to Precision.
  * *$F_{0.5} (\beta = 0.5)$:* Weights Precision higher than Recall. Best for spam filters or recommendations where false alarms are costly.
  * *$F_1 (\beta = 1.0)$:* Weights Precision and Recall equally.
  * *$F_2 (\beta = 2.0)$:* Weights Recall higher than Precision. Best for disease screening or safety checks where misses are costly.
* **Multi-Class Evaluation Strategies:**
  * *Macro Averaging:* Calculates unweighted metrics per class and takes a plain average. Treats every class equally, making it optimal for evaluating performance on rare classes in imbalanced data.
  * *Micro Averaging:* Pools total True Positives, False Positives, and False Negatives across all classes first to calculate a single overall score.
  * *Weighted Averaging:* Calculates metrics per class and averages them weighted by the support (number of true instances) of each class.
* **SageMaker Tuning & Model Selection Integration:**
  * *SageMaker Linear Learner:* Allows selecting the best model artifact during training based on criteria like F-beta, precision at a target recall, or recall at a target precision (e.g., maintain $\ge 90\%$ recall while maximizing precision).
  * *Automatic Model Tuning:* Supports defining validation precision, recall, or F-beta as the primary objective metric for hyperparameter optimization jobs.

---

## 🏗️ Architecture or Design Description
The classification metric decision and optimization pipeline illustrates how raw model output probabilities map to threshold decisions and guide SageMaker model selection:

```

+----------------------------------------------------------------------------------------------------+
|                                  RAW MODEL PREDICTION PROBABILITIES                                |
+----------------------------------------------------------------------------------------------------+
|
v
+----------------------------------------------------------------------------------------------------+
|                                  DYNAMIC THRESHOLD SELECTION SLIDER                                |
|  [Low Threshold: High Recall / Low Precision] <---> [High Threshold: High Precision / Low Recall]  |
+----------------------------------------------------------------------------------------------------+
|
v
+----------------------------------------------------------------------------------------------------+
|                                      CONFUSION MATRIX OUTCOMES                                     |
|               (True Positives, False Positives, False Negatives, True Negatives)                   |
+----------------------------------------------------------------------------------------------------+
|
v
+----------------------------------------------------------------------------------------------------+
|                                     HARMONIC METRIC EVALUATION                                     |
|          +------------------------+  +------------------------+  +---------------------+           |
|          |  F0.5 (Precision-heavy)|  |   F1 (Equal Balance)   |  | F2 (Recall-heavy)   |           |
|          +------------------------+  +------------------------+  +---------------------+           |
+----------------------------------------------------------------------------------------------------+
|
v
+----------------------------------------------------------------------------------------------------+
|                              SAGEMAKER AUTOMATIC MODEL TUNING / SELECTION                          |
|                  (Optimize objective: Precision at Target Recall OR Maximize F-Beta)               |
+----------------------------------------------------------------------------------------------------+

```

---

## 📋 Major Steps Completed
1. Formulated a spam filter binary classification scenario ($200$ total emails: $40$ actual spam, $160$ legitimate) to calculate base confusion matrix outcomes ($TP=30$, $FN=10$, $FP=20$, $TN=140$).
2. Computed exact baseline metrics: Precision ($60\%$), Recall ($75\%$), and F1-Score ($66.7\%$).
3. Demonstrated the precision-recall trade-off by adjusting prediction probability thresholds from conservative ($100\%$ precision / $2.5\%$ recall) to extreme aggressive ($20\%$ precision / $100\%$ recall).
4. Compared arithmetic averages against harmonic means to illustrate why F1 penalizes single-metric skew.
5. Implemented $F_\beta$ evaluation functions ($F_{0.5}$ and $F_2$) to shift metric priority based on business risk.
6. Evaluated multi-class predictions using Macro, Micro, and Weighted averaging strategies across imbalanced target classes.
7. Configured SageMaker Linear Learner hyperparameters to select top-performing models using `precision_at_target_recall` criteria and set up SageMaker Automatic Model Tuning jobs.

---

## ⚠️ Problems or Errors Encountered
* **Skrewed Overall Accuracy on Imbalanced Multi-Class Data:** Micro and weighted average metrics gave an artificially optimistic view of model quality, masking severe misclassification rates on rare minority classes.
* **Sub-Optimal Default Thresholding in Deployment:** Relying on the default $0.5$ classification threshold led to unacceptable false negative rates for high-risk detection workloads.

---

## 🔧 How Those Problems Were Resolved
* **Macro Metric Adoption:** Switched multi-class validation reporting to **Macro-averaged F1-Score**, forcing equal evaluation weight across all classes regardless of sample size.
* **Target-Based SageMaker Tuning:** Configured SageMaker Linear Learner with `binary_classifier_model_selection_criteria = "precision_at_target_recall"` and specified `target_recall = 0.90`, enabling automatic threshold tuning to guarantee required sensitivity.

---

## 📊 Results or Output
* Intuitive metric evaluation pipeline capable of dynamically balancing Precision, Recall, and $F_\beta$ scores.
* Optimized SageMaker tuning setup configured to maximize model precision while enforcing a strict baseline threshold for recall.

---

## 🤔 Lessons Learned / Reflection
Precision and Recall exist in a natural trade-off driven by classification threshold selection. Evaluating models using arithmetic averages is misleading because it ignores extreme performance imbalances; harmonic metrics like the F1-Score (and parameterized $F_\beta$ variants) provide a much more honest assessment. In production environments using Amazon SageMaker, aligning hyperparameter tuning objectives with specific metric targets—such as maximizing precision at a fixed recall threshold—ensures that models meet real-world operational requirements.

---

## 🔗 YouTube Link(s)
* *[Insert your YouTube presentation/lab video link here]*

---

## 💼 LinkedIn Post Link(s)
* *[Insert your LinkedIn project/reflection post link here]*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 18 Presentation Deck
* AWS Documentation: [Amazon SageMaker Linear Learner Algorithm - Model Selection Parameters](https://docs.aws.amazon.com/sagemaker/latest/dg/linear-learner.html)
* Scikit-Learn Documentation: [Precision-Recall and F-measure Metrics](https://scikit-learn.org/stable/modules/model_evaluation.html#precision-recall-f-measure-metrics)
