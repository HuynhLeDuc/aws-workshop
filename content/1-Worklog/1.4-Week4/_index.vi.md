---
title: "Worklog Tuần 4"
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

###  Mục tiêu tuần 4

* Hiểu rõ cơ chế **cấp quyền truy cập** cho ứng dụng sử dụng dịch vụ AWS.  
* Nắm được sự khác biệt giữa **Access Key/Secret Access Key** và **IAM Role**.  
* Biết cách **tạo và gán IAM Role cho EC2 Instance** để ứng dụng có thể truy cập dịch vụ AWS mà không cần lưu trữ thông tin xác thực.  
* Làm quen và thực hành với **AWS Cloud9**, môi trường IDE trên trình duyệt được tích hợp sẵn AWS CLI.  
* Học cách **viết, chạy, và kiểm thử mã nguồn** trực tiếp trong Cloud9.  

---

###  Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ---------- | ------------- | ---------------- | --------------- |
| 2 | - Tổng quan về **AWS Identity and Access Management (IAM)** <br> - Tìm hiểu cách AWS kiểm soát truy cập vào tài nguyên <br> - Ôn lại khái niệm **User**, **Group**, **Policy**, **Role** | 22/09/2025 | 22/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3 | - Thực hành cấp quyền bằng **Access Key và Secret Access Key** <br> - Chạy thử ứng dụng truy cập dịch vụ AWS qua Access Key <br> - Phân tích rủi ro bảo mật khi lưu trữ Access Key trong mã nguồn | 23/09/2025 | 23/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4 | - Giới thiệu và tạo **IAM Role cho EC2 Instance** <br> - Gán IAM Role cho instance và kiểm tra quyền truy cập đến S3/DynamoDB qua ứng dụng Node.js mẫu <br> - Thực hành thu hồi quyền truy cập và kiểm thử lại ứng dụng | 24/09/2025 | 24/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5 | - Làm quen với **AWS Cloud9 IDE** <br> - Tạo một **Cloud9 instance** và thiết lập môi trường làm việc <br> - Khám phá các tính năng: terminal, file explorer, debugger, syntax highlighting | 25/09/2025 | 25/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6 | - **Thực hành nâng cao:** <br>&emsp; + Viết script truy cập dịch vụ AWS bằng AWS CLI trên Cloud9 <br>&emsp; + Triển khai ứng dụng Node.js CRUD (AWS User Management) trực tiếp trên Cloud9 <br>&emsp; + Dọn dẹp tài nguyên sau khi hoàn thành | 26/09/2025 | 26/09/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

###  Kết quả đạt được trong tuần 4 :

* Hiểu rõ sự khác biệt giữa **Access Key/Secret Key** và **IAM Role**, và lý do nên sử dụng IAM Role để tăng cường bảo mật.  
* Biết cách **tạo IAM Role** với quyền hạn phù hợp (ví dụ: quyền đọc/ghi S3).  
* Gán **IAM Role cho EC2 Instance** và kiểm tra truy cập dịch vụ AWS trực tiếp mà không cần thông tin đăng nhập tĩnh.  
* Làm quen và sử dụng thành thạo **AWS Cloud9 IDE**:  
  * Tạo và cấu hình môi trường phát triển.  
  * Kết nối với EC2 instance.  
  * Chạy các lệnh AWS CLI và thử nghiệm mã nguồn trực tiếp.  
* Viết và triển khai ứng dụng Node.js đơn giản trên Cloud9 để truy cập dữ liệu từ AWS S3 hoặc DynamoDB.  
* Nắm được quy trình **dọn dẹp tài nguyên** sau khi thực hành để tránh phát sinh chi phí.  

---

###  Tóm tắt kiến thức đạt được

- **IAM Role:** Giải pháp bảo mật tốt hơn Access Key, cho phép cấp quyền tạm thời cho EC2.  
- **Access Key/Secret Key:** Hiểu rõ nhược điểm khi sử dụng trong mã nguồn.  
- **AWS Cloud9:** IDE mạnh mẽ chạy trên trình duyệt, hỗ trợ nhiều ngôn ngữ lập trình và tích hợp CLI.  
- **AWS CLI & SDK:** Sử dụng để truy cập dịch vụ AWS thông qua vai trò IAM.  
- **Thực hành triển khai:** Cấu hình, chạy và dọn dẹp môi trường AWS an toàn, hiệu quả.  

---