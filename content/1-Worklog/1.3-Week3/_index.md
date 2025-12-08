---
title: "Week 3 Worklog"
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* Understand the concept and functionality of **Amazon EC2 (Elastic Compute Cloud)**.  
* Learn how to **launch, connect, configure, and manage EC2 instances** on both Windows and Linux.  
* Practice deploying a **sample web application (AWS User Management)** on EC2 instances.  
* Learn how to **monitor, secure, and clean up** EC2 resources efficiently.  

---

### Tasks to be carried out this week:

| No. | Task | Start Date | Completion Date | Reference |
| --- | ---- | ----------- | ---------------- | ---------- |
| 1 | - Overview of **Amazon EC2** and its key concepts: <br>&emsp; + Instance, AMI, Key Pair, Elastic IP, Security Group, Volume <br>&emsp; + EC2 pricing models (On-Demand, Spot, Reserved, Savings Plan) | 22/09/2025 | 22/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 2 | - **Hands-on:** Create and configure a **Windows EC2 instance** <br>&emsp; + Choose AMI and instance type <br>&emsp; + Configure key pair and security group <br>&emsp; + Connect using Remote Desktop (RDP) <br>&emsp; + Explore Windows Server 2022 environment | 23/09/2025 | 23/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3 | - **Hands-on:** Create and configure a **Linux EC2 instance** <br>&emsp; + Launch Amazon Linux 2 <br>&emsp; + Connect via SSH using key pair <br>&emsp; + Explore the Linux environment and essential commands <br>&emsp; + Update system packages | 24/09/2025 | 24/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4 | - **Deploy sample app “AWS User Management”** <br>&emsp; + Install Node.js, npm, and dependencies on both Linux and Windows instances <br>&emsp; + Deploy CRUD web app (User Management System) <br>&emsp; + Test Create, Read, Update, Delete, and Search functions <br>&emsp; + Share app across network using Security Groups | 25/09/2025 | 25/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5 | - Learn EC2 monitoring and management tools: <br>&emsp; + Amazon CloudWatch (for metrics and logs) <br>&emsp; + AWS Systems Manager <br>&emsp; + EC2 Instance Connect <br> - Clean up unused instances, Elastic IPs, and security groups | 26/09/2025 | 26/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Week 3 Achievements:

* Understood the **core concepts of Amazon EC2**, including:  
  * **AMI (Amazon Machine Image):** Provides the OS and app template for launching instances.  
  * **Instance Type:** Defines computing capacity (CPU, RAM, storage).  
  * **Key Pair:** Used for secure login (SSH/RDP).  
  * **Elastic IP:** A static IP for accessing instances over the Internet.  
  * **Security Group:** Acts as a virtual firewall controlling inbound/outbound traffic.  

* Successfully created and configured **Windows and Linux EC2 instances**:  
  * Connected via **RDP (Windows)** and **SSH (Linux)**.  
  * Managed instances through **AWS Console and CLI**.  
  * Configured **network rules** to allow web traffic (port 80, 443, 22, 3389).  

* Deployed the **AWS User Management** web application on both platforms:  
  * Installed **Node.js**, **npm**, and app dependencies.  
  * Deployed a fully functional CRUD application (Add, Edit, Delete, Search users).  
  * Shared the application with other users using **public IP or Elastic IP**.  

* Learned to **monitor EC2 instances** using:  
  * **Amazon CloudWatch** (view CPU, memory, and network usage).  
  * **AWS Systems Manager** for automation and instance control.  
  * **EC2 Instance Connect** for secure browser-based access.  

* Practiced **resource management and cost optimization**:  
  * Stopped and terminated instances when not in use.  
  * Released unused Elastic IPs.  
  * Deleted unneeded Security Groups and Key Pairs.  

---

### Summary of Knowledge Gained:

- **Amazon EC2:** Deep understanding of cloud-based compute instances.  
- **Windows & Linux Management:** Hands-on experience configuring, connecting, and securing both OS environments.  
- **Application Deployment:** Deployed Node.js CRUD app on EC2 instances.  
- **Cloud Monitoring:** Used CloudWatch and Systems Manager to observe performance.  
- **Cost Efficiency:** Learned to clean up and optimize EC2 resources effectively.  

---

