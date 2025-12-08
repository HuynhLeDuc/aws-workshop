---
title : "Prerequiste"

weight : 2 
chapter : false
pre : " <b> 5.2. </b> "
---

### 1. Create an IAM Role using the Console with the required permissions
Create an IAM role named **bedrock** and assign the necessary permissions to use Amazon Bedrock: model/agent invocation permissions (`bedrock:InvokeModel`, `bedrock:CreateAgent`, `bedrock:InvokeAgent`), S3 access permissions (read/write) to load documents to the Knowledge Base, and CloudWatch Logs permissions to write logs, etc.

![alt text](/images/5-Workshop/5.2-Prerequisite/pre1.png)

![alt text](/images/5-Workshop/5.2-Prerequisite/pre2.png)

#### Document templates to load kwoledge base (PDF, text, markdown, HTML)

+ We will create an introduction document to Amazon Web Services (Text)
```bash

Amazon Web Services (AWS) is Amazon's cloud computing platform, officially launched in 2006. Initially, AWS was created to solve Amazon's internal problem: they needed a flexible scalable infrastructure to serve their huge e-commerce system. When realizing that other businesses were also facing similar difficulties with IT infrastructure, Amazon decided to commercialize this platform and provide it as a cloud service.

AWS was born with the goal of helping organizations and businesses reduce server investment costs, deploy applications faster, and take advantage of infrastructure on demand instead of having to operate data centers themselves. This is the core vision behind the modern "cloud computing" model: turning computing resources into a utility service that can be used immediately, like electricity and water.

In the following years, AWS grew rapidly, from a few basic services such as storage (Amazon S3) and virtual machines (EC2) to an ecosystem of more than 200 services including virtual servers, containers, artificial intelligence, data storage, security, IoT and data analytics. Thanks to its global scalability with dozens of Regions and hundreds of Edge points around the world, AWS became the leading cloud platform in the market.

AWS's long-term goal is to provide a secure, flexible computing environment that can meet the needs of all users — from small startups to large corporations. AWS aims to help businesses focus on product development, instead of spending time operating infrastructure. To date, AWS is used by leading technology companies, governments, universities and millions of organizations around the world.

AWS is not just an infrastructure service, but has also become an important platform to drive innovation in areas such as machine learning, Big Data, generative AI with (Amazon Bedrock), and serverless application development. Thanks to that, AWS plays an important role in shaping the modern technology generation.
```