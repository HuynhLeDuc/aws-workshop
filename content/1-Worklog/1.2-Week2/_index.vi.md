---
title: "Worklog Tuần 2"
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---
### Mục tiêu tuần 2:

* Hiểu khái niệm **Amazon Virtual Private Cloud (VPC)** và tầm quan trọng của nó trong kiến trúc AWS.  
* Biết cách thiết kế, triển khai và quản lý **mạng riêng ảo** trên AWS.  
* Học cách thiết lập kết nối **AWS Site-to-Site VPN** giữa môi trường On-Premise và AWS Cloud.  
* Nắm được các **phương pháp bảo mật mạng** tốt nhất theo chuẩn AWS Well-Architected Framework.  

---

### Các công việc cần triển khai trong tuần này:

| **Thứ** | **Công việc** | **Ngày bắt đầu** | **Ngày hoàn thành** | **Nguồn tài liệu** |
| -------- | -------------- | ---------------- | ------------------- | ------------------ |
| 2 | - Tổng quan về **Amazon VPC** <br> - Tìm hiểu kiến trúc mạng AWS và vai trò của VPC trong môi trường đám mây <br> - Nắm các khái niệm: Subnet, Route Table, Internet Gateway, NAT Gateway, VPC Peering | 15/09/2025 | 15/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3 | - **Thực hành:** <br>&emsp; + Tạo **VPC** với cấu trúc mạng chuẩn <br>&emsp; + Tạo các **Public** và **Private Subnet** <br>&emsp; + Cấu hình **Route Table** và **Internet Gateway** để kết nối Internet | 16/09/2025 | 16/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4 | - Tìm hiểu về **Network Security trên AWS** <br>&emsp; + Security Groups <br>&emsp; + Network ACLs <br>&emsp; + So sánh và thực hành thiết lập quy tắc truy cập <br> - **Thực hành:** <br>&emsp; + Tạo Security Group và Network ACL cho VPC <br>&emsp; + Kiểm thử truy cập bằng EC2 Instance | 17/09/2025 | 17/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5 | - Giới thiệu **AWS Site-to-Site VPN** <br> - Tìm hiểu mô hình kết nối giữa **On-premise** và **AWS Cloud** <br> - **Thực hành:** <br>&emsp; + Tạo **Virtual Private Gateway (VGW)** và **Customer Gateway (CGW)** <br>&emsp; + Thiết lập kết nối VPN giữa hai môi trường <br>&emsp; + Kiểm tra trạng thái kết nối và định tuyến | 18/09/2025 | 18/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6 | - Tổng kết và đánh giá kết quả học tập tuần 2 <br> - **Thực hành nâng cao:** <br>&emsp; + Thiết kế VPC theo chuẩn **AWS Well-Architected Framework** <br>&emsp; + Tự động hóa triển khai hạ tầng bằng **Infrastructure as Code (IaC)** template (CloudFormation hoặc Terraform) <br>&emsp; + Dọn dẹp tài nguyên sau khi hoàn thành workshop | 19/09/2025 | 19/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Kết quả đạt được tuần 2:

* Hiểu rõ **Amazon VPC** là gì và tầm quan trọng của việc cô lập mạng trong AWS Cloud.  
* Nắm được cấu trúc cơ bản của một VPC bao gồm:  
  * **Subnets:** Phân chia vùng mạng cho tài nguyên.  
  * **Route Tables:** Định tuyến lưu lượng mạng trong VPC.  
  * **Internet Gateway:** Cho phép kết nối từ VPC ra Internet.  
  * **NAT Gateway:** Cho phép các instance trong subnet riêng kết nối Internet an toàn.  
  * **VPC Peering:** Kết nối hai VPC khác nhau để chia sẻ tài nguyên.  

* Thực hành triển khai thành công VPC với các subnet riêng và công khai, kiểm tra kết nối thông qua EC2 Instance.  
* Hiểu và cấu hình thành công **Security Groups** và **Network ACLs**, phân biệt được phạm vi áp dụng của từng loại bảo mật mạng.  

* Nắm được quy trình thiết lập **Site-to-Site VPN** giữa hệ thống tại chỗ (on-premise) và AWS:
  * Tạo và cấu hình **Virtual Private Gateway (VGW)** và **Customer Gateway (CGW)**.  
  * Kết nối hai đầu VPN bằng các thông số định tuyến (tunnel configuration).  
  * Kiểm tra kết nối VPN bằng lệnh CLI và bảng điều khiển AWS Console.  

* Nắm được các phương pháp **bảo mật mạng nâng cao** theo chuẩn **AWS Well-Architected Framework**, bao gồm:
  * Phân đoạn mạng (Network Segmentation).  
  * Kiểm soát truy cập ở cấp subnet và instance.  
  * Mã hóa dữ liệu trong quá trình truyền tải qua VPN.  

* Làm quen với cách triển khai **Infrastructure as Code (IaC)** để tự động hóa việc tạo VPC, Subnet, Route Table và Security Groups.  

* Hoàn thành workshop:  
  * Thiết kế và triển khai mô hình VPC hoàn chỉnh.  
  * Thiết lập thành công **Site-to-Site VPN**.  
  * Dọn dẹp toàn bộ tài nguyên sau khi hoàn tất.  

---

### Tóm tắt kiến thức đạt được:

- **Amazon VPC:** Nắm rõ mô hình mạng riêng ảo trong AWS.  
- **Network Security:** Biết cấu hình và kiểm soát truy cập hiệu quả bằng Security Group & Network ACL.  
- **VPN Connection:** Hiểu cách thiết lập và vận hành kết nối Site-to-Site an toàn.  
- **AWS CLI & Console:** Thực hành triển khai, kiểm tra và dọn dẹp tài nguyên qua cả hai công cụ.  
- **IaC (Infrastructure as Code):** Làm quen với việc tự động hóa triển khai hạ tầng AWS.  
