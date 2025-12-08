---
title: "Week 8 Worklog"

weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---


---

### Weekly Objectives

**Part 1 – Amazon DynamoDB**

* Understand DynamoDB’s NoSQL key-value & document architecture.
* Learn the core components: Partition Key, Sort Key, Partition, RCU/WCU, On-Demand, TTL, Streams, Global Tables.
* Create a DynamoDB table with GSI/LSI and define access patterns.
* Practice CRUD: PutItem, GetItem, UpdateItem, DeleteItem.
* Practice Query & Scan, FilterExpression, ConditionExpression.
* Use AWS CLI and JSON to interact with DynamoDB.
* Import a sample dataset into DynamoDB.

**Part 2 – Amazon ElastiCache for Redis**

* Understand in-memory caching structure, cluster mode enabled/disabled.
* Create a Redis Cluster inside a VPC: node, parameter group, subnet group.
* Connect to Redis from EC2 via redis-cli.
* Test data operations: SET, GET, TTL & persistence snapshot.
* Apply the Cache-Aside model between Redis & DynamoDB.
* Measure cache-hit vs cache-miss performance.
* Clean up resources to avoid unexpected costs.

---

### Tasks to be carried out this week:

| Day | Detailed Tasks                                                                                                                                                                                                                                                                                                                        | Start Date | Completion Date | Reference                      |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------------------ |
| 2   | **DynamoDB – Overview & Architecture** <br> • Learn that DynamoDB is a key-value/document NoSQL database. <br> • Understand partitions and how data is distributed via Partition Key. <br> • Understand WCU/RCU, Auto Scaling, On-Demand. <br> • Learn roles of GSI/LSI and common access patterns. <br> • Learn about TTL & Streams. | 27/10/2025 | 27/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3   | **Create DynamoDB Table & Real Query Tests** <br> • Create a table with Partition Key + Sort Key. <br> • Create GSIs to expand query flexibility. <br> • Enable TTL and test record expiration. <br> • Practice CRUD (Put/Get/Update/Delete). <br> • Practice Query vs Scan, FilterExpression, ProjectionExpression.                  | 28/10/2025 | 28/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4   | **DynamoDB via AWS CLI** <br> • Create DynamoDB tables using CLI. <br> • Import sample JSON file. <br> • Query via CLI: KeyConditionExpression. <br> • UpdateItem with ConditionExpression. <br> • Observe throughput & consumed capacity.                                                                                            | 29/10/2025 | 29/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5   | **ElastiCache Redis – Architecture & Deployment** <br> • Understand in-memory architecture, replication group. <br> • Create subnet group & security group for Redis. <br> • Deploy Redis Cluster (1 primary + replicas). <br> • Enable automatic failover. <br> • Connect EC2 to Redis via redis-cli.                                | 30/10/2025 | 30/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6   | **Advanced Redis Practice & DynamoDB Integration** <br> • Test GET, SET, EXPIRE, TTL. <br> • Test persistence snapshot (RDB). <br> • Build Cache-Aside model: <br>   – Cache hit returns immediately. <br>   – Cache miss → read from DynamoDB. <br>   – Write back to Redis cache. <br> • Measure Redis vs DynamoDB latency.         | 31/10/2025 | 31/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 7   | **Resource Cleanup & Performance Evaluation** <br> • Delete Redis Cluster, subnet group, parameter group. <br> • Delete test DynamoDB tables. <br> • Check Billing for WCU/RCU usage. <br> • Evaluate performance difference: <br> Redis: ~1–2ms vs DynamoDB: ~10–20ms.                                                               | 1/11/2025  | 1/11/2025       | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Achievements in Week 8 :

#### 1. Amazon DynamoDB

**Architecture & Table Design**

* Fully understand partitioning, scaling, and throughput mechanism.
* Learn how to design Partition Key and Sort Key to avoid hotspots.
* Optimize access patterns using GSI & LSI.

**CRUD & Query**

* Successfully executed CRUD operations using both Console & CLI.
* Proficient with Query using KeyConditionExpression.
* Understand FilterExpression, UpdateExpression.
* Performed table Scan and advanced filtering.

**Advanced DynamoDB Management**

* Enabled TTL & validated automatic item deletion.
* Explored DynamoDB Streams & event-driven architecture.
* Evaluated cost based on RCU/WCU vs On-Demand.

---

#### 2. Amazon ElastiCache for Redis

**Redis Cluster Deployment**

* Created Redis inside VPC with correct subnet group & security group.
* Configured replication group + automatic failover.
* Successfully connected to Redis from EC2.

**Redis Operations**

* Proficient with SET, GET, DEL, TTL, EXPIRE.
* Tested RDB persistence snapshots.
* Analyzed eviction policies when cache is full.

---

#### 3. DynamoDB + Redis Integration (Cache-Aside)

* Built workflow: check cache → query DB → update cache.
* Tested real-world cache hit/miss scenarios.
* Measured latency: Redis is ~10× faster than DynamoDB.
* Understood why Redis caching is essential for read-heavy systems.
* Learned real-world use cases: user profile caching, session store, product caching.

---

### Summary of Knowledge Gained

**DynamoDB:**

* Distributed NoSQL architecture.
* Partition Key, Sort Key, GSI/LSI.
* CRUD, Query, Scan.
* RCU/WCU Throughput & On-Demand mode.
* TTL, Streams.

**ElastiCache Redis:**

* Ultra-fast in-memory architecture.
* Cluster mode, replication, failover.
* TTL, persistence snapshot.

**Combining DynamoDB + Redis:**

* Cache-Aside pattern.
* Cache hit/miss & performance benefits.
* Practical usage in microservices architectures.

---
