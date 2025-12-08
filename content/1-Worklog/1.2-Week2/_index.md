---
title: "Week 2 Worklog"
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* Understand the concept of **Amazon Virtual Private Cloud (VPC)** and its importance in AWS architecture.  
* Learn how to design, deploy, and manage a **virtual private network** on AWS.  
* Learn how to set up a **AWS Site-to-Site VPN** connection between On-Premise and AWS Cloud environments.  
* Master **network security best practices** following the AWS Well-Architected Framework.  

---

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference |
| --- | ---- | ----------- | ---------------- | ---------- |
| 2 | - Overview of **Amazon VPC** <br> - Study AWS network architecture and the role of VPC in the cloud environment <br> - Understand the concepts: Subnet, Route Table, Internet Gateway, NAT Gateway, VPC Peering | 15/09/2025 | 15/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3 | - **Hands-on:** <br>&emsp; + Create a **VPC** with a standard network structure <br>&emsp; + Create **Public** and **Private Subnets** <br>&emsp; + Configure **Route Table** and **Internet Gateway** for Internet access | 16/09/2025 | 16/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4 | - Learn about **Network Security on AWS** <br>&emsp; + Security Groups <br>&emsp; + Network ACLs <br>&emsp; + Compare and practice configuring access rules <br> - **Hands-on:** <br>&emsp; + Create Security Groups and Network ACLs for VPC <br>&emsp; + Test access control using EC2 instances | 17/09/2025 | 17/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5 | - Introduction to **AWS Site-to-Site VPN** <br> - Study the connection model between **On-premise** and **AWS Cloud** <br> - **Hands-on:** <br>&emsp; + Create **Virtual Private Gateway (VGW)** and **Customer Gateway (CGW)** <br>&emsp; + Establish VPN connection between both environments <br>&emsp; + Verify connection status and routing configuration | 18/09/2025 | 18/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6 | - Summarize and review Week 2 learning outcomes <br> - **Advanced Practice:** <br>&emsp; + Design VPC based on **AWS Well-Architected Framework** <br>&emsp; + Automate infrastructure deployment using **Infrastructure as Code (IaC)** templates (CloudFormation or Terraform) <br>&emsp; + Clean up resources after completing the workshop | 19/09/2025 | 19/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Week 2 Achievements:

* Clearly understood what **Amazon VPC** is and the importance of network isolation in AWS Cloud.  
* Mastered the basic structure of a VPC, including:  
  * **Subnets:** Divide network segments for different resources.  
  * **Route Tables:** Define routing paths for network traffic within VPC.  
  * **Internet Gateway:** Enables public subnet Internet access.  
  * **NAT Gateway:** Allows private subnet instances to securely connect to the Internet.  
  * **VPC Peering:** Connects two different VPCs for resource sharing.  

* Successfully deployed a VPC with both public and private subnets, and verified connectivity through EC2 instances.  
* Understood and configured **Security Groups** and **Network ACLs**, differentiating their scopes and use cases.  

* Learned the process of setting up a **Site-to-Site VPN** between on-premise systems and AWS:  
  * Created and configured **Virtual Private Gateway (VGW)** and **Customer Gateway (CGW)**.  
  * Established VPN connections using routing and tunnel configuration parameters.  
  * Verified VPN connection via AWS CLI and AWS Management Console.  

* Mastered **advanced network security practices** following the **AWS Well-Architected Framework**, including:  
  * Network segmentation.  
  * Access control at both subnet and instance levels.  
  * Data encryption during transmission over VPN.  

* Gained hands-on experience with **Infrastructure as Code (IaC)** to automate the creation of VPCs, Subnets, Route Tables, and Security Groups.  

* Completed the workshop by:  
  * Designing and deploying a complete VPC model.  
  * Successfully establishing a **Site-to-Site VPN** connection.  
  * Cleaning up all AWS resources after completion.  

---

### Summary of Knowledge Gained:

- **Amazon VPC:** Gained in-depth understanding of virtual networking in AWS.  
- **Network Security:** Learned to configure and manage secure access with Security Groups and Network ACLs.  
- **VPN Connection:** Understood how to set up and maintain secure Site-to-Site VPN connections.  
- **AWS CLI & Console:** Practiced deploying, testing, and cleaning up resources using both tools.  
- **IaC (Infrastructure as Code):** Learned how to automate AWS infrastructure deployment efficiently.  
