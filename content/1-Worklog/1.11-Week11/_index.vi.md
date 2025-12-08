---
title: "Worklog Tuần 11"

weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---

---


---

###  Mục tiêu tuần

**Phần 1 – Serverless: Sử dụng Amplify Authentication và Storage**

* Hiểu cách hoạt động của Amplify Libraries, Amplify Auth và Amplify Storage.
* Tích hợp Cognito Authentication vào ứng dụng web.
* Tạo hệ thống upload file từ frontend và lưu trữ vào S3 bằng Amplify Storage.
* Tìm hiểu các cấp độ truy cập (public / protected / private).
* Nắm được tổng quan kiến trúc sử dụng Cognito + S3 + Amplify.

**Phần 2 – Serverless: Xây dựng Front-end gọi API Gateway**

* Hiểu quy trình tạo API Gateway kết nối Lambda.
* Tạo frontend sử dụng JavaScript/React gọi API Gateway → Lambda → DynamoDB.
* Kiểm thử API từ Postman và kiểm thử trực tiếp từ frontend.
* Nắm rõ kiến trúc front-end → API Gateway → Lambda → DynamoDB.

---

###  Các công việc triển khai trong tuần

| Thứ | Công việc chi tiết | Bắt đầu | Hoàn thành | Nguồn |
| --- | ------------------ | ------- | ---------- | ------ |
| 2 | **Giới thiệu Amplify & Chuẩn bị môi trường**<br>• Tìm hiểu Amplify Libraries, CLI và UI Components.<br>• Khởi tạo project web để tích hợp Amplify.<br>• Cài đặt gói `@aws-amplify/ui` và `aws-amplify`.<br>• Cấu hình môi trường AWS. | 17/11 | 17/11 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3 | **Xác thực với Amplify Auth (Cognito)**<br>• Tạo User Pool & Identity Pool.<br>• Cấu hình Amplify Auth trong frontend.<br>• Tạo UI login bằng Amplify UI Components.<br>• Test đăng ký, đăng nhập, reset password. | 18/11 | 18/11 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4 | **Lưu trữ file với Amplify Storage (S3)**<br>• Tạo S3 bucket qua Amplify.<br>• Cấu hình quyền truy cập public/protected/private.<br>• Viết logic upload file từ front-end → S3.<br>• Kiểm tra file trên S3 console.<br>• Viết hàm list files & get URL. | 19/11 | 19/11 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5 | **Triển khai API Gateway kết nối Lambda**<br>• Tạo API Gateway REST.<br>• Map method → Lambda CRUD functions.<br>• Enable CORS cho front-end.<br>• Triển khai ARN mới cho Lambda. | 20/11 | 20/11 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6 | **Test API với Postman**<br>• Gửi request GET/POST/DELETE.<br>• Kèm Authorization token từ Cognito.<br>• Kiểm tra log CloudWatch.<br>• Fix lỗi CORS và IAM permission. | 21/11 | 21/11 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 7 | **Tích hợp Front-end gọi API Gateway**<br>• Viết service JavaScript gọi API Gateway.<br>• Gắn token Cognito vào request header.<br>• Render kết quả trả về từ Lambda/DynamoDB.<br>• Test end-to-end: Front-end → API → Lambda → DynamoDB.<br>• Dọn dẹp tài nguyên test. | 22/11 | 22/11 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Kết quả đạt được trong tuần 11 :


 **1. Hoàn thiện Authentication với Amplify + Cognito**

* Đăng nhập/đăng ký người dùng hoạt động hoàn chỉnh.
* Xử lý các luồng xác thực: login, sign-up, confirm code, reset password.
* Front-end có thể truy cập JWT token để gửi request đến API Gateway.
* Hiểu sâu về cơ chế User Pool & Identity Pool.

---

**2. Upload & quản lý file bằng Amplify Storage + S3**

* Upload file từ frontend thành công.
* S3 bucket được tạo tự động bởi Amplify.
* Thử nghiệm thành công 3 cấp độ truy cập:  
  `public`, `protected`, `private`.
* Implement được các hàm:
  * upload
  * list files
  * get URL  
  * delete file (tùy chọn)

---

 **3. Xây dựng API Gateway hoàn chỉnh cho DMS**

* Tạo REST API bao gồm các route CRUD tài liệu.
* Gắn Lambda functions từ tuần trước.
* Kích hoạt CORS đầy đủ.
* Test tất cả API bằng Postman với JWT Cognito.

---

 **4. Tích hợp Front-end gọi API Gateway**

* Viết đầy đủ logic frontend gửi request kèm token Cognito.
* Parse và hiển thị danh sách tài liệu từ DynamoDB.
* Thực hiện thành công luồng:
  
  **Login → Upload file → Lưu metadata → Query → Hiển thị kết quả**

---

### Tóm tắt kiến thức đạt được

 **Amplify**
* Amplify Auth sử dụng Cognito làm backend.
* Amplify Storage hỗ trợ tương tác S3 đơn giản.
* Amplify UI giúp tạo screen login nhanh chóng.

 **Cognito(Authentication)**
* User Pool quản lý người dùng.
* Identity Pool cấp quyền tạm thời để truy cập S3.
* JWT token được dùng để gọi API Gateway.

 **S3(Storage)**
* Tổ chức object theo cấp độ: public / private / protected.
* Upload trực tiếp từ frontend thông qua Amplify.

 **API Gateway**
* Định tuyến request vào Lambda.
* CORS configuration rất quan trọng với frontend.
* Có thể yêu cầu token Cognito để xác thực.

 **Lambda + DynamoDB**
* Lambda xử lý logic CRUD.
* DynamoDB lưu metadata tài liệu.
* API Gateway giúp frontend truy vấn dữ liệu thông qua Lambda.

---



