---
title: "Worklog Tuần 8"

weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---


---

### Mục tiêu tuần :

**Phần 1 – Amazon DynamoDB**

* Hiểu kiến trúc NoSQL key-value & document của DynamoDB.
* Nắm các thành phần: Partition Key, Sort Key, Partition, RCU/WCU, On-Demand, TTL, Streams, Global Tables.
* Tạo bảng DynamoDB với GSI/LSI và định nghĩa Access Pattern.
* Thực hành CRUD: PutItem, GetItem, UpdateItem, DeleteItem.
* Thực hành Query & Scan, FilterExpression, ConditionExpression.
* Dùng AWS CLI và JSON để tương tác DynamoDB.
* Import dataset thử nghiệm vào DynamoDB.

**Phần 2 – Amazon ElastiCache for Redis**

* Hiểu cấu trúc in-memory caching, cluster mode enabled/disabled.
* Tạo Redis Cluster trong VPC: node, parameter group, subnet group.
* Kết nối Redis từ EC2 qua redis-cli.
* Thử nghiệm dữ liệu: SET, GET, TTL & persistence snapshot.
* Áp dụng mô hình Cache-Aside giữa Redis & DynamoDB.
* Kiểm tra hiệu năng cache-hit và cache-miss.
* Dọn dẹp tài nguyên để tránh chi phí.

---

### Các công việc triển khai trong tuần

| Thứ | Công việc chi tiết                                                                                                                                                                                                                                                                                                                 | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                 |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------------------ |
| 2   | **DynamoDB – Tổng quan & Kiến trúc** <br> • Tìm hiểu DynamoDB là NoSQL key-value/document. <br> • Hiểu kiến trúc partition, phân phối dữ liệu theo Partition Key. <br> • Hiểu WCU/RCU, Auto Scaling, On-Demand. <br> • Nắm vai trò GSI/LSI và các access pattern phổ biến. <br> • Tìm hiểu TTL & Streams.                          | 27/10/2025   | 27/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3   | **Tạo DynamoDB Table & Query thực tế** <br> • Tạo bảng với Partition Key + Sort Key. <br> • Tạo nhóm GSI để mở rộng truy vấn. <br> • Bật TTL và test bản ghi hết hạn. <br> • Thực hành CRUD (Put/Get/Update/Delete). <br> • Thực hành Query vs Scan, FilterExpression, ProjectionExpression.                                       | 28/10/2025   | 28/11/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4   | **Thao tác DynamoDB bằng AWS CLI** <br> • Tạo bảng DynamoDB bằng CLI. <br> • Import file JSON mẫu. <br> • Query qua CLI: KeyConditionExpression. <br> • UpdateItem có điều kiện với ConditionExpression. <br> • Quan sát throughput & consumed capacity.                                                                           | 29/10/2025   | 29/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5   | **ElastiCache Redis – Kiến trúc & Triển khai** <br> • Hiểu kiến trúc in-memory, replication group. <br> • Tạo subnet group và security group cho Redis. <br> • Khởi tạo Redis Cluster 1 primary + replicas. <br> • Kích hoạt Automatic Failover. <br> • Kết nối EC2 vào Redis qua redis-cli.                                       | 30/10/2025   | 30/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6   | **Redis thực hành nâng cao & tích hợp DynamoDB** <br> • Thử GET, SET, EXPIRE, TTL. <br> • Test persistence snapshot (RDB). <br> • Tạo mô hình Cache-Aside: <br>   – Cache hit trả về ngay. <br>   – Cache miss → đọc từ DynamoDB. <br>   – Ghi lại cache Redis để tối ưu hiệu năng. <br> • Kiểm tra độ trễ giữa Redis vs DynamoDB. | 31/10/2025   | 31/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 7   | **Dọn dẹp tài nguyên & Đánh giá hiệu năng** <br> • Xóa Redis Cluster, subnet group, parameter group. <br> • Xóa DynamoDB Table test. <br> • Kiểm tra Billing xem phí WCU/RCU phát sinh. <br> • Đánh giá sự khác biệt hiệu năng cache: <br> Redis: ~1–2ms – DynamoDB: ~10–20ms.                                                     | 1 /11/2025   | 1 /11/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Kết quả đạt được trong tuần 8:

#### 1. Amazon DynamoDB

**Kiến trúc & thiết kế bảng**

* Nắm rõ cơ chế phân vùng, scaling và throughput.
* Hiểu cách thiết kế Partition Key, Sort Key tránh hotspot.
* Tối ưu access pattern bằng GSI & LSI.

**CRUD & Query**

* Thực hiện đầy đủ CRUD qua Console & CLI.
* Thành thạo Query theo KeyConditionExpression.
* Biết sử dụng FilterExpression, UpdateExpression.
* Scan bảng và lọc dữ liệu nâng cao.

**Quản lý DynamoDB nâng cao**

* Bật TTL & kiểm tra cơ chế tự xóa bản ghi.
* Kiểm tra DynamoDB Streams & kiến trúc event-driven.
* Đánh giá cost dựa trên RCU/WCU và On-Demand.

---

#### 2. Amazon ElastiCache for Redis

**Triển khai Redis Cluster**

* Tạo Redis trong VPC với subnet group & security group đúng chuẩn.
* Cấu hình replication group + failover tự động.
* Kết nối Redis từ EC2 thành công.

**Thao tác Redis**

* Thành thạo SET, GET, DEL, TTL, EXPIRE.
* Test persistence snapshot (RDB).
* Phân tích eviction policy khi cache đầy.

---

#### 3. Tích hợp DynamoDB + Redis (Cache-Aside)

* Xây dựng quy trình: check cache → query DB → cập nhật cache.
* Thử nghiệm cache hit/miss thực tế.
* Đo hiệu năng: Redis nhanh gấp ~10 lần DynamoDB.
* Hiểu lý do phải dùng Redis caching đối với hệ thống đọc nhiều (read-heavy).
* Biết mô hình ứng dụng thực tế: user profile caching, session store, product caching.

---

### Tóm tắt kiến thức đạt được

**DynamoDB:**

* Kiến trúc NoSQL phân tán.
* Partition Key, Sort Key, GSI/LSI.
* CRUD, Query, Scan.
* Throughput RCU/WCU & On-Demand.
* TTL, Streams.

**ElastiCache Redis:**

* Kiến trúc in-memory cực nhanh.
* Cluster mode, replication, failover.
* TTL, snapshot persistence.

**Kết hợp DynamoDB + Redis:**

* Mô hình Cache-Aside.
* Cache hit/miss & hiệu năng.
* Ứng dụng thực tế cho microservices.

---


