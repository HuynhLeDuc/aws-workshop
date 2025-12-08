---
title: "Worklog Tuần 3"
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Hiểu khái niệm và chức năng của **Amazon EC2 (Elastic Compute Cloud)**.  
* Học cách **khởi tạo, kết nối, cấu hình và quản lý các EC2 instance** trên cả Windows và Linux.  
* Thực hành triển khai một **ứng dụng web mẫu (AWS User Management)** trên các EC2 instance.  
* Học cách **giám sát, bảo mật và dọn dẹp tài nguyên EC2** một cách hiệu quả.  

---

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ---------- | ------------- | ---------------- | --------------- |
| 2 | - Tổng quan về **Amazon EC2** và các khái niệm chính: <br>&emsp; + Instance, AMI, Key Pair, Elastic IP, Security Group, Volume <br>&emsp; + Các mô hình tính phí của EC2 (On-Demand, Spot, Reserved, Savings Plan) | 22/09/2025 | 22/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3 | - **Thực hành:** Tạo và cấu hình **Windows EC2 instance** <br>&emsp; + Chọn AMI và loại instance <br>&emsp; + Cấu hình key pair và security group <br>&emsp; + Kết nối bằng Remote Desktop (RDP) <br>&emsp; + Khám phá môi trường Windows Server 2022 | 23/09/2025 | 23/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4 | - **Thực hành:** Tạo và cấu hình **Linux EC2 instance** <br>&emsp; + Khởi tạo Amazon Linux 2 <br>&emsp; + Kết nối qua SSH bằng key pair <br>&emsp; + Làm quen với môi trường Linux và các lệnh cơ bản <br>&emsp; + Cập nhật gói hệ thống | 24/09/2025 | 24/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5 | - **Triển khai ứng dụng mẫu “AWS User Management”** <br>&emsp; + Cài đặt Node.js, npm và các thư viện cần thiết trên cả Linux và Windows instance <br>&emsp; + Triển khai ứng dụng CRUD (User Management System) <br>&emsp; + Kiểm thử các chức năng: thêm, sửa, xóa, tìm kiếm người dùng <br>&emsp; + Chia sẻ ứng dụng qua mạng bằng Security Group | 25/09/2025 | 25/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6 | - Tìm hiểu công cụ giám sát và quản lý EC2: <br>&emsp; + Amazon CloudWatch (giám sát chỉ số và nhật ký) <br>&emsp; + AWS Systems Manager <br>&emsp; + EC2 Instance Connect <br> - Dọn dẹp các instance, Elastic IP và Security Group không sử dụng | 26/09/2025 | 26/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Kết quả đạt được trong tuần 3:

* Hiểu rõ **các khái niệm cốt lõi của Amazon EC2**, bao gồm:  
  * **AMI (Amazon Machine Image):** Cung cấp hệ điều hành và mẫu ứng dụng để khởi tạo instance.  
  * **Instance Type:** Xác định tài nguyên tính toán (CPU, RAM, bộ nhớ).  
  * **Key Pair:** Dùng để đăng nhập an toàn (SSH/RDP).  
  * **Elastic IP:** Địa chỉ IP tĩnh cho phép truy cập instance qua Internet.  
  * **Security Group:** Tường lửa ảo kiểm soát lưu lượng vào/ra.  

* Tạo và cấu hình thành công **Windows và Linux EC2 instance**:  
  * Kết nối qua **RDP (Windows)** và **SSH (Linux)**.  
  * Quản lý instance thông qua **AWS Console và CLI**.  
  * Cấu hình **quy tắc mạng** cho phép truy cập web (port 80, 443, 22, 3389).  

* Triển khai thành công ứng dụng **AWS User Management** trên cả hai nền tảng:  
  * Cài đặt **Node.js**, **npm** và các thư viện phụ thuộc.  
  * Triển khai ứng dụng CRUD đầy đủ (Thêm, Sửa, Xóa, Tìm kiếm người dùng).  
  * Chia sẻ ứng dụng cho người dùng khác thông qua **Public IP hoặc Elastic IP**.  

* Học cách **giám sát EC2 instance** bằng:  
  * **Amazon CloudWatch** (giám sát CPU, bộ nhớ, lưu lượng mạng).  
  * **AWS Systems Manager** để tự động hóa và quản lý instance.  
  * **EC2 Instance Connect** để truy cập an toàn qua trình duyệt.  

* Thực hành **quản lý tài nguyên và tối ưu chi phí**:  
  * Dừng hoặc xóa các instance không còn sử dụng.  
  * Giải phóng Elastic IP chưa dùng.  
  * Xóa các Security Group và Key Pair dư thừa.  

---

### Tóm tắt kiến thức đạt được:

- **Amazon EC2:** Hiểu sâu về cách vận hành máy chủ ảo trong môi trường đám mây.  
- **Quản lý Windows & Linux:** Thực hành cấu hình, kết nối và bảo mật trên cả hai hệ điều hành.  
- **Triển khai ứng dụng:** Triển khai thành công ứng dụng Node.js CRUD trên EC2.  
- **Giám sát hệ thống:** Sử dụng CloudWatch và Systems Manager để theo dõi hiệu suất.  
- **Tối ưu chi phí:** Biết cách dọn dẹp và quản lý tài nguyên EC2 hiệu quả.  

---

