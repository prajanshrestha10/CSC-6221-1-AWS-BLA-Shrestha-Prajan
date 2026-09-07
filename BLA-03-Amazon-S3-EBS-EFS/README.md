# CSC-6221-1 BLA - AWS Certified Machine Learning Associate Part 3

## 📌 BLA Number and Title
* **BLA Number:** BLA-03
* **Title:** AWS Certified Machine Learning Associate - Part 3: AWS Storage Essentials (Amazon S3, EBS, and EFS)

---

## 🎯 Purpose of the Activity
The objective of this activity is to explore, compare, and implement the core cloud storage paradigms available in Amazon Web Services (AWS)—Object Storage (S3), Block Storage (EBS), and File Storage (EFS) and determine their appropriate application in modern cloud and machine learning architectures.

---

## 🛠️ AWS Services, Tools, Languages & Technologies Used
* **AWS Services:** Amazon S3, Amazon EBS, Amazon EFS, Amazon EC2
* **Protocols & Interfaces:** HTTP/HTTPS REST API, POSIX, Network File System (NFS)
* **Languages & Formats:** Bash / Shell, Markdown
and determine their appropriate application in modern cloud and machine learning architectu
---

## 💡 Concepts Learned
* **Object vs. Block vs. File Storage:** Understanding key structural differences, access paths, and scalability limits across cloud storage models.
* **Storage Durability & Availability:** Evaluating AWS availability metrics (e.g., S3's 11 9s durability).
* **Workload Matching:** Selecting storage solutions based on latency requirements, access frequency, concurrency, and cost efficiency.

---

## 📐 Architecture & Design Description
* **Amazon S3:** Standalone key-value object store accessible globally via REST APIs over HTTP/HTTPS.
* **Amazon EBS:** Block-level storage attached directly to a single EC2 instance within a specific Availability Zone (AZ) via low-latency virtual disk buses.
* **Amazon EFS:** Shared POSIX filesystem mounted concurrently across multiple EC2 instances via NFS protocol within or across Availability Zones.

---

## 📝 Major Steps Completed
1. Defined structural characteristics and access patterns for S3, EBS, and EFS.
2. Formulated a side-by-side feature comparison matrix mapping latency, concurrency, and pricing models.
3. Identified workload-specific decision rules for deploying block, object, or file storage in production environments.

---

## ⚠️ Problems or Errors Encountered
* **Cross-AZ Access Constraints:** Encountered volume attachment errors when attempting to mount an EBS volume to an EC2 instance located in a different Availability Zone.
* **Concurrent Write Bottlenecks:** Experienced file lock issues when multiple EC2 instances attempted simultaneous file updates using direct EBS storage without a shared filesystem layer.

---

## 🔧 How Problems Were Resolved
* **EBS AZ Lock:** Reconfigured deployment scripts to ensure the EC2 instance and EBS volume were provisioned in the exact same Availability Zone, or used EBS snapshots to replicate volumes across zones.
* **Concurrency Fix:** Migrated the shared workload from EBS to Amazon EFS using NFS mounts, enabling multi-instance read/write access.

---

## 📊 Results or Output
* A structured comparative framework evaluating S3, EBS, and EFS.
* A decision matrix detailing workload-to-service mapping for storage architecture optimization.

---

## 🧠 Lessons Learned / Reflection
Understanding the underlying access protocol (REST vs. Block vs. NFS) is crucial before provisioning storage in AWS. Choosing the wrong storage model leads to performance bottlenecks or inflated cloud expenditures.

---

## 🔗 Project Links
* **YouTube Video:** [Insert Link Here]
* **LinkedIn Post:** [Insert Link Here]

---

## 📚 References & Resources Used
* [AWS Storage Documentation](https://aws.amazon.com/storage/)
* [Amazon S3 User Guide](https://docs.aws.amazon.com/s3/)
* [Amazon EBS User Guide](https://docs.aws.amazon.com/ebs/)
* [Amazon EFS User Guide](https://docs.aws.amazon.com/efs/)
