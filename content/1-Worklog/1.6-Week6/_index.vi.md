---
title: "Worklog Tuần 6"

weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---


---

###  Mục tiêu tuần 6 :

* Hiểu kiến trúc **Amazon RDS** và các engine được hỗ trợ (MySQL, PostgreSQL, MariaDB, SQL Server…).
* Tạo, cấu hình và quản lý một **RDS Instance** ở mức nền tảng.
* Thiết lập **parameter group**, **security group**, **subnet group** dành cho RDS.
* Kết nối RDS từ **EC2**, **Cloud9**, và từ máy local.
* Thực hành **backup – restore – snapshot – automated backup – failover**.
* Làm quen với **Performance Insights**, **Monitoring**, **Enhanced Logging**.
* Biết cách **tối ưu chi phí**, scale storage và compute, và dọn dẹp tài nguyên.

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                                                                                                                              | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                 |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | --------------- | ------------------------------ |
| 2   | **Tổng quan Amazon RDS** <br>  + Các engine hỗ trợ <br>  + Kiến trúc Multi-AZ & Read Replica <br>  + Backup/Snapshot lifecycle                                                                         | 13/10/2025   | 13/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3   | **Tạo RDS Instance** <br>  + Tạo Subnet Group <br>  + Cấu hình Security Group (cho phép EC2/Cloud9) <br>  + Chọn engine, size, storage                                                                 | 14/10/2025   | 14/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |                  
| 4   | **Kết nối & thao tác trên RDS** <br>  + Kết nối từ Cloud9/EC2 <br>  + Tạo database & table <br>  + CRUD bằng MySQL Client hoặc PostgreSQL Client                                                       | 15/10/2025   | 15/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |                   |
| 5   | **Backup – Restore – Snapshot – Monitoring** <br>  + Tạo snapshot thủ công <br>  + Restore từ snapshot <br>  + Quan sát monitoring, CPU, connections <br>  + Sử dụng Performance Insights              | 16/10/2025   | 16/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6   | **Scaling – Tối ưu chi phí – Dọn dẹp tài nguyên** <br>  + Thay đổi instance class <br>  + Mở rộng storage <br>  + Cấu hình tự động backup hợp lý <br>  + Xóa snapshot & RDS để tránh phát sinh chi phí | 17/10/2025   | 17/10/2025      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Kết quả đạt được trong tuần 6:
**1. Hiểu rõ kiến trúc Amazon RDS:**
* Phân biệt được: Single-AZ, Multi-AZ, Read Replica.
* Biết cách hoạt động của automated backup (giữ 1–35 ngày).
* Biết snapshot là backup thủ công, không tự xóa.

**2. Tạo và cấu hình RDS Instance hoàn chỉnh:**
* Tạo **DB Subnet Group** chứa 2 subnet ở 2 AZ.
* Tạo **Security Group** cho phép kết nối từ EC2/Cloud9 (port 3306 hoặc 5432).
* Cấu hình instance với:
  * Engine (MySQL/PostgreSQL)
  * Instance class (db.t3.micro)
  * Storage (20GB gp3)
  * Backup retention
  * Public/Private endpoint
**3. Kết nối thành công từ EC2 / Cloud9 / local:**
* Cài đặt MySQL/PostgreSQL client.
* Kết nối bằng chuỗi:
  ```
  mysql -h endpoint.amazonaws.com -u admin -p
  ```
* Tạo database, table và CRUD dữ liệu:
  * `CREATE DATABASE demo;`
  * `CREATE TABLE users (...);`
  * `INSERT`, `SELECT`, `UPDATE`, `DELETE`

**4. Làm chủ Backup – Restore – Snapshot:**
* Tạo manual snapshot.
* Restore thành RDS mới từ snapshot.
* Quan sát backup window.
* Kiểm tra automated backups tạo tự động mỗi ngày.

**5. Monitoring & Performance:**
* Theo dõi CPU, RAM, active connections trong “Monitoring”.
* Sử dụng **Performance Insights** xem truy vấn nặng.
* Xem Slow Query Log (nếu bật).

**6. Scaling & Tối ưu chi phí:**
* Thay đổi instance class từ t3.micro → t3.small.
* Tăng storage từ 20GB → 30GB.
* Giảm backup retention xuống 3 ngày để giảm chi phí.
* Xóa snapshot không cần thiết.

**7. Dọn dẹp tài nguyên để tránh phát sinh chi phí:**
* Xóa RDS instance.
* Xóa subnet group.
* Xóa security group.
* Xóa snapshot cũ.

---

###  Tóm tắt kiến thức đạt được

* Hiểu cách RDS hoạt động và các engine phổ biến.
* Biết tạo, cấu hình và kết nối tới RDS từ Cloud9 và EC2.
* Nắm được cơ chế backup, snapshot, restore.
* Sử dụng Performance Insights để theo dõi hiệu năng.
* Biết cách scale và tối ưu chi phí RDS.
* Dọn dẹp tài nguyên đúng cách để tránh lệ phí cao.

---




