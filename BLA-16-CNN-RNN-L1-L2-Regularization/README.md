# CSC-6221-1 BLA - CNN, RNN & Regularization

## 📌 BLA Number and Title
* **BLA Number:** BLA-16
* **Title:** AWS Certified Machine Learning Associate - Part 16: CNN, RNN & Regularization (Two Network Types and the L1/L2 Technique)

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to examine two specialized neural network architectures—Convolutional Neural Networks (CNNs) and Recurrent Neural Networks (RNNs)—alongside core regularization techniques used to prevent overfitting. The lab focuses on understanding grid-based spatial feature extraction via CNNs, sequence-based temporal memory management via RNNs (including LSTMs and GRUs), and contrasting L1 (Lasso) versus L2 (Ridge) regularization penalties.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **AWS Machine Learning Platform:** Amazon SageMaker, Automatic Model Tuning
* **Neural Network & Algorithm Types:** Convolutional Neural Networks (CNN), Recurrent Neural Networks (RNN), LSTM, GRU, DeepAR, Seq2Seq, Image Classification, Object Detection
* **Regularization Techniques:** L1 Regularization (Lasso / Alpha), L2 Regularization (Ridge / Weight Decay / Lambda), Dropout, Early Stopping
* **Languages & Frameworks:** Python, Jupyter Notebooks

---

## 💡 Concepts Learned
* **Convolutional Neural Networks (CNNs):** Designed for grid-like data (mostly images). Core operations include:
  * *Input Image:* Pixel value grids.
  * *Convolution:* Filters slide across the image to detect edges, shapes, and complex objects automatically.
  * *Pooling:* Shrinks data dimensionality while retaining the strongest signals.
  * *Fully Connected Layer:* Makes final classification decisions (e.g., cat vs. dog).
  * *Parameter Sharing:* Reuses the same filters across the entire image, drastically reducing required weight parameters.
* **Recurrent Neural Networks (RNNs):** Designed for sequences where order matters (text, speech, time series). 
  * *Architecture:* Reads inputs one word or time point at a time, updating a hidden state (memory) and passing it forward to produce predictions.
  * *The Memory Problem:* Long sequences suffer from the vanishing gradient problem where memory fades.
  * *LSTM & GRU:* Incorporates specialized gates to decide what information to keep or forget, allowing networks to retain context over longer sequences.
* **CNN vs. RNN Comparison:**
  * *CNN:* Grid-like data / images $\rightarrow$ Filters slide across input (SageMaker: Image Classification, Object Detection).
  * *RNN:* Sequential data / text / time series $\rightarrow$ Memory carried from step to step (SageMaker: DeepAR, Seq2Seq).
* **Regularization Principles:** Combines loss error with a complexity penalty ($Loss = Error + \lambda \times penalty$) to discourage large weights, producing simpler models that generalize better to unseen validation and test data.
* **L1 vs. L2 Regularization:**
  * *L1 (Lasso):* Adds an absolute weight penalty ($\lambda \times \sum |w|$). Pushes some weights to exactly zero, providing built-in feature selection and sparse models.
  * *L2 (Ridge / Weight Decay):* Adds a squared weight penalty ($\lambda \times \sum w^2$). Shrinks all weights smoothly toward zero without eliminating them entirely.
* **Regularization in Practice:**
  * *Linear Learner & XGBoost:* Built-in hyperparameters support both L1 (`alpha`) and L2 (`lambda`) penalties.
  * *Dropout:* Randomly deactivates neurons during training to prevent co-adaptation.
  * *Early Stopping:* Terminates training automatically when validation error stops improving.

---

## 🏗️ Architecture or Design Description
The architectural comparison pipeline illustrates how spatial inputs route through CNN filters versus sequential inputs processing through RNN memory cells:
```
+-----------------------------------------------------------------------------------+
|                            INPUT DATA CATEGORIZATION                              |
+-----------------------------------------------------------------------------------+
             |                                                 |
             v                                                 v
+---------------------------------------+     +-------------------------------------+
|        CNN (Spatial / Grids)          |     |       RNN (Sequential / Time)       |
|  * Input Image Grid                   |     |  * Word / Time Step Input           |
|  * Convolution Layers (Filters)       |     |  * Hidden State (Memory / LSTM)     |
|  * Pooling & Fully Connected Layers   |     |  * Step-by-Step Predictions         |
+---------------------------------------+     +-------------------------------------+
             |                                                 |
             +-------------------------------+-----------------+
                                             |
                                             v
+-----------------------------------------------------------------------------------+
|                       REGULARIZATION & LOSS OPTIMIZATION                          |
|         ($Loss = Error + \lambda \times \text{Penalty}$ [L1/L2 / Dropout])         |
+-----------------------------------------------------------------------------------+
```
---

## 📋 Major Steps Completed
1. Configured convolutional neural network layers for spatial feature extraction and image classification tasks.
2. Implemented recurrent neural network structures using LSTM and GRU memory gates to process sequence and time-series data.
3. Evaluated comparative use cases distinguishing spatial grid problems (CNNs) from ordered sequence problems (RNNs).
4. Applied L1 and L2 regularization penalties within model training configurations to control parameter complexity and combat overfitting.
5. Implemented early stopping and dropout layers, tuning hyperparameters via SageMaker automatic model tuning.

---

## ⚠️ Problems or Errors Encountered
* **Vanishing Gradients in Long RNN Sequences:** Standard RNN architectures failed to retain long-term dependencies over extended time-series sequences during backpropagation.
* **Severe Overfitting on Training Data:** Highly complex models achieved near-zero training error but failed to generalize on unseen validation datasets due to unconstrained weight growth.

---

## 🔧 How Those Problems Were Resolved
* **Gated Architecture Adoption:** Replaced standard RNN nodes with Long Short-Term Memory (LSTM) and Gated Recurrent Unit (GRU) cells, utilizing internal gates to regulate gradient flow over long horizons.
* **Regularization Tuning:** Integrated L2 weight decay (`lambda`) and L1 sparsity penalties (`alpha`) into the model loss function, and applied early stopping to halt training prior to divergence.

---

## 📊 Results or Output
* Robust neural network models optimized for image classification (CNN) and time-series forecasting (RNN/DeepAR).
* Improved model generalization and test accuracy achieved through controlled L1/L2 regularization and early stopping.

---

## 🤔 Lessons Learned / Reflection
Choosing the right neural network architecture depends entirely on data structure: CNNs excel at extracting spatial hierarchies from grid-like images, while RNNs (enhanced by LSTMs and GRUs) preserve temporal memory across ordered sequences. Coupled with proper L1/L2 regularization to penalize excess complexity, these architectures deliver stable, generalizable machine learning solutions.

---

## 🔗 YouTube Link(s)
* *https://youtu.be/0Jb3nkLDHqg*

---

## 💼 LinkedIn Post Link(s)
* *https://www.linkedin.com/feed/update/urn:li:activity:7525722539092758528/*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 16 Presentation Deck
* AWS Documentation: [Amazon SageMaker Built-In Algorithms and Deep Learning Frameworks](https://docs.aws.amazon.com/sagemaker/latest/dg/algos.html)
