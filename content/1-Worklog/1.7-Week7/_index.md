---
title: "Week 7 Worklog"

weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---



### Week 7 Objectives:

**Part 1 – AWS CloudWatch**

* Understand the overall architecture of Amazon CloudWatch and its components: Metrics, Logs, Alarms, Dashboard, Events.
* Practice creating and monitoring CloudWatch Metrics for EC2, RDS, Lambda.
* Collect and analyze logs using CloudWatch Logs.
* Create CloudWatch Alarms with custom thresholds.
* Build CloudWatch Dashboard to monitor the system.
* Practice container monitoring with CloudWatch Container Insights.
* Clean up resources to avoid cost.

**Part 2 – Hybrid DNS with Route 53 Resolver**

* Understand hybrid DNS architecture between on-premise and AWS.
* Create and configure Route 53 Resolver (inbound, outbound).
* Create and apply Resolver Rules to forward DNS queries.
* Integrate on-premise DNS (Active Directory DNS) with Route 53 Private Hosted Zone.
* Verify bidirectional DNS resolution (AWS → on-premise, on-premise → AWS).
* Clean up resources: AD, endpoint, VPC configuration.

---
### Tasks to be carried out this week:

| Day | Detailed Tasks                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Start Date | Completion Date | Documentation Source           |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------------------ |
| 2   | **CloudWatch – Overview & Architecture** <br> • Research CloudWatch overview and its role in AWS. <br> • Study key components: Metrics, Logs, Alarms, Dashboards, Events, Container Insights. <br> • Understand the difference between Basic Monitoring and Detailed Monitoring. <br> • View end-to-end CloudWatch architecture: application → log agent → log group → metric filter → alarm → SNS → automatic action. <br> • Create the first dashboard from EC2 default metrics.                                                                | 20/10/2025 | 20/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3   | **CloudWatch Metrics & Logs – Practical Implementation** <br> • Create Log Group manually and study Log Stream structure. <br> • Install CloudWatch Agent on EC2 to collect OS-level CPU, RAM, Disk, Network data. <br> • Configure `cloudwatch-agent.json` to send system logs (syslog, application log). <br> • Create Metric Filter to detect error patterns (“ERROR”, “CRITICAL”, “Failed”). <br> • Send custom metrics using AWS CLI (`put-metric-data`). <br> • Observe retention period and test retention change.                         | 21/10/2025 | 21/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4   | **CloudWatch Alarm & Dashboard – Automated Alerts** <br> • Create CPU Alarm with 70% threshold for 5 minutes. <br> • Create Alarm for EC2 Status Check Failure. <br> • Connect Alarm → SNS Topic → Email for notification. <br> • Create Alarm to automatically reboot EC2 when CPU overloads (using EC2 action). <br> • Build custom Dashboard: add metrics widgets, logs, alarm status, text widget. <br> • Create system-wide Dashboard monitoring EC2 + RDS + Network. <br> • Enable Container Insights for ECS: view CPU, RAM, Task Restart. | 22/10/2025 | 22/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5   | **Route 53 Resolver – Understanding & Building Hybrid DNS Architecture** <br> • Study Route 53 Private Hosted Zone and DNS resolution inside VPC. <br> • Create Outbound Resolver Endpoint for AWS → on-premise query. <br> • Create Inbound Resolver Endpoint for on-premise → AWS query. <br> • Create Resolver Rule forwarding “corp.local” to on-premise DNS. <br> • Attach rules to VPC and verify endpoint status.                                                                                                                          | 23/10/2025 | 23/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6   | **Microsoft AD + DNS Integration – On-Premise DNS Simulation** <br> • Launch EC2 Windows Server and install Microsoft Active Directory. <br> • Create domain “corp.local” and configure DNS zone in AD. <br> • Configure Conditional Forwarder from AD → AWS Inbound Endpoint. <br> • Create A and CNAME records in on-premise DNS. <br> • Test bidirectional resolution: <br>   – From AWS: `nslookup dc1.corp.local` <br>   – From AD: `nslookup api.internal.aws` <br> • Test failover when endpoint is down.                                  | 24/10/2025 | 24/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 7   | **Clean up resources, review and optimize cost** <br> • Delete unused Log Group, Log Stream, Alarm, Dashboard. <br> • Disable Container Insights to avoid CloudWatch fee. <br> • Delete Route 53 Resolver endpoints (hourly charges). <br> • Delete Resolver Rules. <br> • Disable and delete Microsoft AD domain controller. <br> • Delete all EC2 test instances. <br> • Check Bill → review CloudWatch Logs, metrics, AD, endpoints cost.                                                                                                      | 25/10/2025 | 25/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Achievements in Week 7: 

#### 1. AWS CloudWatch

**CloudWatch Metrics – Collection & Analysis**

* Listed all default metrics from EC2, EBS, VPC, ELB.
* Created custom metrics using CLI and PutMetricData.
* Verified 15-month retention and 1-second granularity display.
* Analyzed anomaly patterns: CPU Spike, abnormal Network I/O, high DiskOps.

---

**CloudWatch Logs – Application Log Collection**

* Installed CloudWatch Agent to collect OS and application logs.
* Created Log Group, Log Stream, pushed real-time logs.
* Set up log retention, exported logs to S3 for analysis.
* Identified common errors in logs: throttling, unauthorized, CPUCredit error.

---

**CloudWatch Alarms – Alerts and Response**

* Created alarm for CPU > 70% within 3 minutes.
* Created alarm for EC2 system status failure.
* Configured SNS notifications for email alerts.
* Enabled auto-recovery for EC2 hardware failure.

---

**CloudWatch Dashboard – Monitoring Console**

* Built real-time monitoring dashboard.
* Added metrics for EC2, RDS, NAT Gateway, ELB in one interface.
* Integrated graph widgets, single-value widgets, and log pattern widgets.

---

**Container Insights – Microservices Monitoring**

* Enabled CloudWatch Container Insights for ECS & Fargate.
* Monitored CPU/memory per task, pod, and container.
* Analyzed restart counts to find root causes.
* Evaluated how Container Insights supports fast troubleshooting.

---

**Resource Cleanup**

* Deleted Dashboards, Alarms, and custom metrics.
* Stopped agent and removed log groups.
* Disabled Container Insights to reduce cost.

---

**Final Results**

* Mastered CloudWatch architecture and end-to-end monitoring pipeline.
* Successfully deployed complete monitoring workflow: **metrics → logs → alarm → dashboard**.
* Learned how to troubleshoot issues using logs and metrics.
* Improved skills in cost optimization and performance tuning using CloudWatch data.
* Gained capability to build real-time alerting systems for DevOps / SRE.

---

#### 2. Building Hybrid DNS with Route 53 Resolver

**Understanding Hybrid DNS Architecture**

* Analyzed common issues in enterprises with on-premise DNS.
* Understood roles of:

  * **Inbound Endpoint** (on-premise → AWS)
  * **Outbound Endpoint** (AWS → on-premise)
  * **Resolver Rules** for forwarding private domains

---

**Environment Preparation**

* Created a dedicated VPC with 2 private subnets for endpoints.
* Created DNS Security Group with port 53 UDP/TCP.
* Deployed EC2 Windows Server to run Microsoft Active Directory Domain Services.

---

**Connecting through RDGW (Remote Desktop Gateway)**

* Connected via RDGW to access private subnet servers.
* Verified DNS resolution inside VPC before hybrid configuration.

---

**Deploying Microsoft Active Directory**

* Configured on-premise Domain Controller (simulated).
* Created internal DNS zone: `company.local`.
* Verified SRV, A, NS records.

---

**Setting Up Hybrid DNS System**

**1) Outbound Endpoint**

* Created Outbound Endpoint so EC2 in VPC can send DNS queries to on-premise AD.
* Assigned resolver rule forwarding `company.local` to on-premise DNS IPs.

**2) Inbound Endpoint**

* Created Inbound Endpoint enabling on-premise DNS to query AWS Private Hosted Zone.
* Verified DNS resolution of Route 53 private records.

**3) Resolver Rules**

* Created Forwarding rule for internal domain.
* Created System rule to automatically inherit VPC default DNS.

---

**Testing Full DNS Flow**

* From on-premise server: ping Private Hosted Zone record → success.
* From AWS EC2: resolve on-premise domain → success.
* Checked DNS latency and validated two-way resolution.

---

**Resource Cleanup**

* Deleted endpoints to avoid hourly charges.
* Deleted Private Hosted Zone and test records.
* Removed AD and terminated test EC2.

---

**Final Results**

* Fully understood enterprise hybrid DNS operation.
* Successfully deployed a complete Route 53 Resolver system (inbound, outbound, rules).
* Integrated Microsoft AD DNS with AWS DNS.
* Verified bidirectional DNS resolution.
* Gained solid knowledge of modern DNS systems for multi-cloud and hybrid-cloud environments.

---

### Summary of Knowledge Gained

**CloudWatch:**

* End-to-end metrics and log collection.
* Intelligent alarm creation and automated responses.
* Building intuitive dashboards.
* Monitoring containers using Container Insights.

**Route 53 Hybrid DNS:**

* Understanding real-world hybrid DNS architecture.
* Integrating on-premise DNS with Route 53 Resolver.
* Verifying two-way resolution.
* Applying architecture to enterprise deployments.

---
