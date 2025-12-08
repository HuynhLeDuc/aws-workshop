---
title: "Week 6 Worklog"

weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---


---

### Week 6 Objectives:

* Understand the architecture of **Amazon RDS** and supported engines (MySQL, PostgreSQL, MariaDB, SQL Server, etc.).
* Create, configure, and manage an **RDS Instance** at the infrastructure level.
* Set up **parameter groups**, **security groups**, and **subnet groups** for RDS.
* Connect to RDS from **EC2**, **Cloud9**, and from a local machine.
* Practice **backup – restore – snapshot – automated backup – failover**.
* Become familiar with **Performance Insights**, **Monitoring**, and **Enhanced Logging**.
* Learn how to **optimize cost**, scale storage/compute, and clean up unused resources.

---

### Tasks to be carried out this week:

| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material             |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ------------------------------ |
| 2   | **Amazon RDS Overview** <br>  + Supported engines <br>  + Multi-AZ & Read Replica architecture <br>  + Backup/Snapshot lifecycle                                                                       | 13/10/2025 | 13/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3   | **Create an RDS Instance** <br>  + Create a Subnet Group <br>  + Configure Security Group (allow EC2/Cloud9) <br>  + Choose engine, instance size, storage                                             | 14/10/2025 | 14/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4   | **Connect & Operate on RDS** <br>  + Connect from Cloud9/EC2 <br>  + Create database & table <br>  + CRUD using MySQL Client or PostgreSQL Client                                                      | 15/10/2025 | 15/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5   | **Backup – Restore – Snapshot – Monitoring** <br>  + Create manual snapshot <br>  + Restore from snapshot <br>  + Monitor CPU, connections <br>  + Use Performance Insights                            | 16/10/2025 | 16/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6   | **Scaling – Cost Optimization – Resource Cleanup** <br>  + Modify instance class <br>  + Increase storage <br>  + Configure proper automated backup retention <br>  + Delete snapshots & RDS instances | 17/10/2025 | 17/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Achievements in Week 6:

#### 1. Solid understanding of Amazon RDS architecture:

* Differentiated between Single-AZ, Multi-AZ, and Read Replica.
* Understood how automated backups work (retention 1–35 days).
* Understood that snapshots are manual backups and not auto-deleted.

#### 2. Successfully created and configured a full RDS Instance:

* Created a **DB Subnet Group** with 2 subnets across 2 AZs.
* Created a **Security Group** allowing connections from EC2/Cloud9 (port 3306 or 5432).
* Configured the instance with:

  * Engine (MySQL/PostgreSQL)
  * Instance class (db.t3.micro)
  * Storage (20GB gp3)
  * Backup retention
  * Public/Private endpoint options

#### 3. Successfully connected from EC2 / Cloud9 / local machine:

* Installed MySQL/PostgreSQL client.

* Connected using the command:

  ```
  mysql -h endpoint.amazonaws.com -u admin -p
  ```

* Created database, table, and performed CRUD operations:

  * `CREATE DATABASE demo;`
  * `CREATE TABLE users (...);`
  * `INSERT`, `SELECT`, `UPDATE`, `DELETE`

#### 4. Mastered Backup – Restore – Snapshot flow:

* Created manual snapshots.
* Restored a new RDS instance from snapshots.
* Observed backup windows.
* Verified daily automated backups.

#### 5. Monitoring & Performance:

* Monitored CPU, RAM, and active connections from the Monitoring dashboard.
* Used **Performance Insights** to identify heavy queries.
* Checked Slow Query Log (if enabled).

#### 6. Scaling & Cost Optimization:

* Modified instance class from t3.micro → t3.small.
* Increased storage from 20GB → 30GB.
* Reduced backup retention to 3 days for cost savings.
* Removed unnecessary snapshots.

#### 7. Cleaned up resources to avoid extra charges:

* Deleted the RDS instance.
* Deleted subnet group.
* Deleted security group.
* Deleted old snapshots.

---

### Summary of Knowledge Gained:

* Understood how Amazon RDS works and common database engines.
* Learned how to create, configure, and connect to RDS from Cloud9 and EC2.
* Gained knowledge of backup, snapshot, and restore workflows.
* Used Performance Insights for performance monitoring.
* Understood how to scale and optimize RDS cost.
* Cleaned up resources properly to avoid unnecessary fees.

---


