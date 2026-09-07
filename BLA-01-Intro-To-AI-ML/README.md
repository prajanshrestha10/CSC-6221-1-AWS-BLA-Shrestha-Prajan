# CSC-6221-1 BLA - AWS Certified Machine Learning Associate Part 1

## 📌 BLA Number and Title
* **BLA Number:** BLA-01
* **Title:** AWS Certified Machine Learning Associate - Part 1: AI and ML | Understanding the Basics

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to introduce the core foundations of Artificial Intelligence (AI) and Machine Learning (ML), contrast ML with traditional programming paradigms, explore various ML learning approaches (Supervised, Unsupervised, and Reinforcement Learning), and examine how AWS services like Amazon SageMaker streamline the machine learning lifecycle in production environments.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **Cloud Services:** Amazon SageMaker, AWS Infrastructure Services
* **AI/ML Domains:** Artificial Intelligence, Machine Learning, Deep Learning, Generative AI (LLMs like ChatGPT, Claude)
* **Documentation & Presentation Tools:** PDF Presentation, Markdown, GitHub, Git

---

## 💡 Concepts Learned
* **AI vs. ML vs. Deep Learning:** AI is the overarching goal of building intelligent systems. ML is the data-driven method to achieve AI. Deep Learning uses multi-layered neural networks for complex patterns.
* **Programming Paradigm Shift:** Traditional programming relies on explicit rules (`Rules + Data → Answers`), whereas Machine Learning discovers rules from historical data (`Data + Answers → Rules`).
* **Machine Learning Lifecycle:** A 4-stage iterative process involving Data Collection, Model Training, Model Evaluation, and Production Deployment.
* **ML Paradigms:** 
  * **Supervised Learning:** Training with labeled data (e.g., price prediction, spam detection).
  * **Unsupervised Learning:** Finding structure in unlabeled data (e.g., customer segmentation).
  * **Reinforcement Learning:** Learning via trial-and-error reward mechanisms (e.g., robotics, gaming).
* **Generative AI:** Modern LLMs capable of writing/summarizing text, generating media, and creating/explaining code.

---

## 🏗️ Architecture or Design Description
The architecture of a typical cloud-based Machine Learning pipeline using Amazon SageMaker follows an end-to-end lifecycle:


```

+------------------+     +-------------------+     +---------------------+     +--------------------+
|   Prepare &      | --> |  Build & Train    | --> |  Tune & Evaluate    | --> |  Deploy at Scale   |
|   Label Data     |     |  Models           |     |  Performance        |     |  (Endpoint API)    |
+------------------+     +-------------------+     +---------------------+     +--------------------+
^                                                                                |
+-------------------------- Continuous Retraining Loop --------------------------+

```

---

## 📋 Major Steps Completed
1. Defined the fundamental definitions and real-world applications of Artificial Intelligence.
2. Differentiated Machine Learning workflows from traditional rule-based software engineering.
3. Categorized the three core types of ML: Supervised, Unsupervised, and Reinforcement Learning.
4. Analyzed industry-specific use cases across Healthcare, Finance, Retail, Transportation, and Manufacturing.
5. Examined Generative AI capabilities and its impact on the modern technology landscape.
6. Mapped end-to-end ML lifecycle steps directly to AWS infrastructure and Amazon SageMaker capabilities.

---

## ⚠️ Problems or Errors Encountered
* **Authentication Error on Git Push:** When attempting to push local changes to GitHub over HTTPS using standard account password credentials, Git returned an authentication failure:
  `remote: Invalid username or token. Password authentication is not supported for Git operations.`

---

## 🔧 How Those Problems Were Resolved
* **Personal Access Token (PAT) Implementation:** Generated a classic Personal Access Token with `repo` permissions from GitHub Developer Settings and used the token string in place of the account password during terminal authentication.

---

## 📊 Results or Output
* Completed presentation deck summarizing the core concepts for Part 1 of the AWS Certified Machine Learning Associate module.
* Structured study notes covering key ML paradigms, workflows, and AWS SageMaker integration.
* Fully configured and synchronized GitHub repository with project documentation.

---

## 🤔 Lessons Learned / Reflection
Understanding the transition from traditional rule-based logic to data-driven Machine Learning is foundational for designing modern cloud architectures. Leveraging managed services like Amazon SageMaker significantly reduces operational overhead by eliminating the need to provision and manage physical hardware for model training and deployment.

---

## 🔗 YouTube Link
* *https://www.youtube.com/watch?v=ObG43JXZj6c*

---

## 💼 LinkedIn Post Link
* *https://www.linkedin.com/feed/update/urn:li:activity:7502506242817445888/*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Course Materials
* AWS Documentation: [Amazon SageMaker Overview](https://aws.amazon.com/sagemaker/)
* Presentation Deck: *AI & Machine Learning - Understanding the Basics (Part 1)*
