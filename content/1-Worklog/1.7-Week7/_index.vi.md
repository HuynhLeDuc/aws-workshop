---
title: "Worklog Tuần 7"

weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---





---

###  Mục tiêu tuần  : 

**Phần 1 – AWS CloudWatch**

* Hiểu tổng quan kiến trúc Amazon CloudWatch và các thành phần: Metrics, Logs, Alarms, Dashboard, Events.
* Thực hành tạo và giám sát CloudWatch Metrics cho EC2, RDS, Lambda.
* Thu thập và phân tích logs với CloudWatch Logs.
* Tạo CloudWatch Alarm với các ngưỡng tùy chỉnh.
* Xây dựng CloudWatch Dashboard theo dõi hệ thống.
* Thực hành container monitoring với CloudWatch Container Insights.
* Dọn dẹp tài nguyên tránh phát sinh chi phí.

**Phần 2 – Hybrid DNS với Route 53 Resolver**

* Hiểu kiến trúc DNS hybrid giữa on-premise và AWS.
* Tạo và cấu hình Route 53 Resolver (inbound, outbound).
* Tạo và áp dụng Resolver Rules để forward DNS query.
* Tích hợp DNS on-premise (Active Directory DNS) với Route 53 private hosted zone.
* Kiểm tra phân giải tên miền 2 chiều (AWS → on-premise, on-premise → AWS).
* Dọn dẹp tài nguyên: AD, endpoint, VPC config.

---

### Các công việc triển khai trong tuần


| Thứ | Công việc chi tiết | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------ | ------------ | --------------- | -------------- |
| 2 | **CloudWatch – Tổng quan & Kiến trúc** <br> • Nghiên cứu tổng quan CloudWatch và vai trò trong hệ thống AWS. <br> • Tìm hiểu các thành phần chính: Metrics, Logs, Alarms, Dashboards, Events, Container Insights. <br> • Hiểu sự khác biệt giữa Basic Monitoring và Detailed Monitoring. <br> • Xem kiến trúc CloudWatch end-to-end: ứng dụng → log agent → log group → metric filter → alarm → SNS → hành động tự động. <br> • Tạo biểu đồ đầu tiên từ metrics mặc định của EC2. | 20/10/2025 | 20/10/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3 | **CloudWatch Metrics & Logs – Triển khai thực tế** <br> • Tạo Log Group thủ công và tìm hiểu cấu trúc Log Stream. <br> • Cài đặt CloudWatch Agent lên EC2 để thu thập CPU, RAM, Disk, Network ở mức OS-level. <br> • Cấu hình file `cloudwatch-agent.json` để gửi logs hệ thống (syslog, application log). <br> • Tạo Metric Filter để tìm lỗi theo pattern (“ERROR”, “CRITICAL”, “Failed”). <br> • Gửi custom metric bằng lệnh AWS CLI (`put-metric-data`). <br> • Quan sát retention period và test thay đổi retention. | 21/10/2025 | 21/10/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4 | **CloudWatch Alarm & Dashboard – Tự động hóa cảnh báo** <br> • Tạo CPU Alarm với ngưỡng 70% trong 5 phút. <br> • Tạo Alarm cho EC2 Status Check Failure. <br> • Kết nối Alarm → SNS Topic → Email để nhận cảnh báo. <br> • Tạo Alarm tự động reboot EC2 khi CPU quá tải (bằng EC2 action). <br> • Tạo Dashboard tùy chỉnh: thêm widget metrics, logs, alarm status, text widget. <br> • Tạo Dashboard giám sát toàn bộ hệ thống: EC2 + RDS + Network. <br> • Thực hiện Container Insights cho ECS: xem CPU, RAM, Task Restart. | 22/10/2025 | 22/10/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5 | **Route 53 Resolver – Hiểu và xây dựng kiến trúc DNS Hybrid** <br> • Tìm hiểu Route 53 private hosted zone và DNS resolution trong VPC. <br> • Tạo Outbound Resolver Endpoint để AWS gửi truy vấn về on-premise DNS. <br> • Tạo Inbound Resolver Endpoint cho phép hệ thống on-premise truy vấn ngược lên AWS. <br> • Tạo Resolver Rule chuyển tiếp tên miền “corp.local” về DNS on-premise. <br> • Gán rules vào VPC và kiểm tra trạng thái endpoint. | 23/10/2025 | 23/10/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6 | **Microsoft AD + DNS Integration – Mô phỏng on-premise DNS** <br> • Khởi tạo EC2 Windows Server và cài đặt Microsoft Active Directory. <br> • Tạo domain “corp.local” và cấu hình DNS zone trong AD. <br> • Cấu hình Conditional Forwarder từ AD → Inbound Endpoint AWS. <br> • Tạo bản ghi A, CNAME trong on-premise DNS. <br> • Kiểm tra phân giải 2 chiều: <br>   – Từ AWS: `nslookup dc1.corp.local` <br>   – Từ AD: `nslookup api.internal.aws` <br> • Kiểm tra phân giải khi endpoint down (test failover). | 24/10/2025 | 24/10/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 7 | **Dọn dẹp tài nguyên, review và tối ưu chi phí** <br> • Xóa Log Group, Log Stream, Alarm, Dashboard không dùng. <br> • Tắt Container Insights để tránh phí CloudWatch. <br> • Xóa Route 53 Resolver endpoints (vì tính theo giờ). <br> • Xóa Resolver Rule. <br> • Tắt và xóa Microsoft AD domain controller. <br> • Xóa toàn bộ EC2 test. <br> • Kiểm tra Bill → xem phần CloudWatch Logs, metrics, AD, endpoints. | 25/10/2025 | 25/10/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |


---

### Kết quả đạt được trong tuần 7:
#### 1. AWS CloudWatch 

**CloudWatch Metrics – Thu thập & phân tích**  
* Liệt kê toàn bộ metrics mặc định từ EC2, EBS, VPC, ELB.
* Tự tạo custom metrics bằng CLI và PutMetricData.
* Kiểm tra retention 15 tháng, xem thử biểu đồ theo 1s granularity.
* Phân tích các tình huống bất thường: CPU Spike, Network I/O tăng đột biến, DiskOps cao.

---

**CloudWatch Logs – Thu thập log ứng dụng**
* Cài đặt CloudWatch Agent để thu thập log OS và ứng dụng.
* Tạo Log Group, Log Stream, đẩy dữ liệu real-time.
* Thiết lập log retention, export logs ra S3 để phân tích.
* Nhận diện các lỗi phổ biến trong log: throttling, unauthorized, lỗi CPUCredit.

---

**CloudWatch Alarms – Cảnh báo và phản hồi**
* Tạo alarm cho CPU > 70% trong 3 phút.
* Tạo alarm cho trạng thái hệ thống EC2 fail.
* Thiết lập SNS notification để gửi email cảnh báo.
* Thiết lập auto-recovery khi EC2 bị lỗi phần cứng.

---
**CloudWatch Dashboard – Bảng điều khiển giám sát**
* Tự xây dựng dashboard theo dạng real-time.
* Gắn metrics của EC2, RDS, NAT Gateway, ELB lên cùng một giao diện.
* Tích hợp widget dạng graph, single value và log pattern.

---

**Container Insights – Giám sát microservices**
* Bật CloudWatch Container Insights cho ECS & Fargate.
* Giám sát CPU/memory per task, per pod, per container.
* Phân tích lỗi container restart count để xác định root cause.
* Đánh giá cách CloudWatch Insight hỗ trợ troubleshooting nhanh.

---

 **Dọn dẹp tài nguyên**
* Xóa Dashboard, Alarm, Metrics custom.
* Dừng agent và xoá log group.
* Tắt Container Insights để tránh phát sinh phí.

---

**Kết quả đạt được**
* Nắm vững kiến trúc CloudWatch và pipeline giám sát toàn hệ thống AWS.
* Tự triển khai đầy đủ quy trình monitoring: **metrics → logs → alarm → dashboard**.
* Biết phân tích và xử lý lỗi dựa trên logs và metrics.
* Thành thạo hơn trong việc tối ưu hoá chi phí và hiệu năng nhờ dữ liệu CloudWatch.
* Có khả năng xây dựng hệ thống cảnh báo real-time phục vụ DevOps / SRE.

---

#### 2. Thiết lập Hybrid DNS với Route 53 Resolver
**Tìm hiểu kiến trúc Hybrid DN**

* Phân tích vấn đề thường gặp khi doanh nghiệp có DNS on-prem.
* Hiểu vai trò của:
  * **Inbound Endpoint** (on-prem → AWS)
  * **Outbound Endpoint** (AWS → on-prem)
  * **Resolver Rules** để forward tên miền nội bộ.

---

**Chuẩn bị môi trường**
* Tạo 1 VPC riêng với 2 private subnet để đặt endpoint.
* Tạo Security Group cho DNS với port 53 UDP/TCP.
* Deploy 1 EC2 Windows Server để chạy Microsoft Active Directory Domain Services.

---

**Kết nối đến RDGW (Remote Desktop Gateway)**
* Kết nối qua RDGW để truy cập server trong private subnet.
* Kiểm tra khả năng phân giải DNS trong VPC trước khi cấu hình hybrid.

---

**Triển khai Microsoft Active Directory**
* Cấu hình Domain Controller on-prem (giả lập).
* Thiết lập DNS internal zone: ví dụ `company.local`.
* Kiểm tra bản ghi SRV, A, NS hoạt động đúng.

---

**Thiết lập hệ thống DNS Hybrid**

**1) Outbound Endpoint**
* Tạo Outbound Endpoint để EC2 trong VPC có thể gửi DNS query về AD on-prem.
* Gán các resolver rule forward domain `company.local` về IP DNS on-prem.

**2) Inbound Endpoint**
* Tạo Inbound Endpoint để DNS on-prem có thể truy cập Private Hosted Zone của AWS.
* Kiểm tra khả năng phân giải record trong Route 53 Private Zone.

 **3) Resolver Rules**
* Tạo rule kiểu Forwarding cho domain nội bộ.
* Tạo rule kiểu System để tự động nhận DNS mặc định của VPC.
---

 **Kiểm thử toàn bộ luồng DNS**
* Từ server on-prem: ping DNS record của Private Hosted Zone → thành công.
* Từ EC2 trên AWS: phân giải tên miền on-prem → thành công.
* Kiểm tra độ trễ DNS và xác thực 2-way resolution.
---

**Dọn dẹp tài nguyên**
* Xóa endpoint để tránh phát sinh chi phí theo giờ.
* Xóa Private Hosted Zone và các test records.
* Gỡ AD và tắt EC2 test.
---

**Kết quả đạt được** 
* Hiểu rõ cơ chế vận hành DNS hybrid trong doanh nghiệp.
* Tự triển khai hệ thống Route 53 Resolver hoàn chỉnh (inbound, outbound, rules).
* Tích hợp thành công DNS Microsoft AD với DNS của AWS.
* Kiểm tra thành công luồng phân giải DNS hai chiều.
* Nắm chắc mô hình DNS hiện đại cho môi trường multi-cloud và hybrid-cloud.

---

### Tóm tắt kiến thức đạt được

**CloudWatch:**
* Thu thập metrics, logs end-to-end.
* Tạo alarms thông minh và tự động hóa xử lý.
* Xây dashboard trực quan.
* Giám sát container bằng Container Insights.

**Route 53 Hybrid DNS:**
* Hiểu mô hình DNS hybrid thực tế.
* Tích hợp on-premise DNS với Route 53 Resolver.
* Kiểm tra phân giải 2 chiều giữa hệ thống.
* Áp dụng vào triển khai hệ thống doanh nghiệp.
