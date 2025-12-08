---
title: "Week 5 Worklog"

weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---


### Week 5 Objectives:

* Gain a deep understanding of **Amazon S3** — object storage model, key features, and use cases.  
* Practice **hosting a static website** on S3: enable the feature, configure public access, test, and optimize performance.  
* Learn how to **secure buckets** (Block Public Access, IAM policy, Bucket Policy) while allowing public access for specific objects when necessary.  
* Perform advanced management operations: **Versioning**, **S3 Transfer Acceleration**, **S3 Batch / S3 Replication (cross-region replication)**, and **object migration**.  
* Understand how to **clean up resources** to avoid unwanted costs and follow S3 best practices.

---

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference |
| --- | ----- | ----------- | ---------------- | ----------- |
| 2 | **Environment setup & basic theory** <br>&emsp; + Overview of S3: object, bucket, key, region, storage class (STANDARD, IA, GLACIER). <br>&emsp; + Durability & availability (11 nines). <br>&emsp; + Use cases (static website, backup, data lake). | 2025-10-06 | 2025-10-06 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3 | **Create an S3 bucket & enable Static Website Hosting** <br>&emsp; + Create a bucket (naming rules, region selection). <br>&emsp; + Upload index.html / error.html files. <br>&emsp; + Enable static website hosting and test the endpoint. | 2025-10-07 | 2025-10-07 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4 | **Configure Block Public Access & Bucket Policy** <br>&emsp; + Understand Block Public Access at account and bucket levels. <br>&emsp; + Configure Bucket Policy to allow public access only for index.html. <br>&emsp; + Test browser access and validate security. | 2025-10-08 | 2025-10-08 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4 | **Optimize performance & advanced security** <br>&emsp; + Compare S3 + CloudFront vs S3 Transfer Acceleration vs AWS Amplify Hosting. <br>&emsp; + Enable S3 Transfer Acceleration and test with curl from multiple regions. <br>&emsp; + (Optional) Create a CloudFront distribution for HTTPS + CDN. <br>&emsp; + Monitor via CloudWatch and track costs. | 2025-10-09 | 2025-10-09 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6 | **Versioning, Lifecycle & Replication + Resource cleanup** <br>&emsp; + Enable bucket versioning, test overwrite and restore old versions. <br>&emsp; + Set lifecycle rules to transition objects to IA/Glacier. <br>&emsp; + Configure Cross-Region Replication (CRR), create IAM replication role. <br>&emsp; + Move/copy/sync objects across buckets or regions. <br>&emsp; + Clean up resources: delete test objects, disable acceleration, remove CloudFront (if any), delete test bucket. | 2025-10-10 | 2025-10-10 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Week 4 Achievements:

**Configuration and basic operations:**
- Set up and configured **AWS CLI** to work with Amazon S3 (Access Key, Secret Key, default Region).  
- Verified connection and configuration using:  
  - `aws configure list`  
  - `aws s3 ls` to list existing buckets.  
  - `aws s3api list-buckets` for detailed information.  
- Created and deleted buckets via CLI:  
  - `aws s3 mb s3://bucket-name`  
  - `aws s3 rb s3://bucket-name --force`  

**Static Website Hosting Practice:**
- Created a new bucket, uploaded `index.html` and `error.html`.  
- Enabled **Static Website Hosting** and successfully accessed the website through the public endpoint.  
- Verified 403/404 errors and ensured error.html was correctly displayed.  

**Security and Access Management:**
- Enabled and disabled **Block Public Access** at both account and bucket levels to understand behavior.  
- Configured **Bucket Policy** to allow only index.html to be publicly accessible.  
- Tested public/private object access for permission validation.  

**Data Management and Performance Optimization:**
- Enabled **Versioning** on the bucket, uploaded multiple object versions, and restored older ones.  
- Configured **Lifecycle Rules** to automatically move infrequently accessed data to IA or Glacier.  
- Enabled **S3 Transfer Acceleration** and measured upload speed differences across regions using `curl`.  

**Advanced Operations and Data Movement:**
- Configured **Cross-Region Replication (CRR)** to copy objects to a different region, understood IAM Role requirements (Replication Role).  
- Practiced CLI operations:  
  - `aws s3 cp`, `aws s3 mv`, `aws s3 sync` for moving and syncing data between buckets.  
- Verified successful replication in the destination bucket.  

**Cleanup & Cost Optimization:**
- Deleted test objects, disabled Transfer Acceleration and CloudFront (if used).  
- Deleted unused test buckets to prevent additional charges.  
- Compiled **best practices** for cost and security:  
  - Avoid public buckets entirely.  
  - Use Versioning + Lifecycle Rules for recovery and cost reduction.  
  - Use **S3 Storage Lens** and **CloudWatch Budgets** to monitor and control costs.

---

### Notes:

- **Never make the entire bucket public**; use **Bucket Policy** to expose only specific objects.  
- **Enable Block Public Access** at the account level by default.  
- **Use Versioning + Lifecycle Rules** to prevent data loss and reduce cost.  
- **Use CloudFront** or **Amplify Hosting** for HTTPS, CDN, and modern static site deployment.  
- **Monitor costs** using CloudWatch and S3 Storage Lens.  
- **Delete carefully** when Versioning is enabled—remove all versions and delete markers before deleting a bucket.  

---

### Summary of Knowledge Gained:

- Operate **Amazon S3** at a production level: hosting, security, cost optimization, versioning, and replication.  
- Choose the right tool for static website hosting: **Amplify (recommended)**, **CloudFront + S3**, or **S3 only** for simplicity.  
- Perform large-scale data management: object transfer, cross-region replication, and automation with Lifecycle Rules.  
- Clean up resources properly to avoid unexpected costs.  
