---
title: "Worklog Tuần 10"

weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---

---

###  Mục tiêu tuần: 

**Phần 1 – Xây dựng backend Document Management System (DMS) với Lambda + DynamoDB**

* Hiểu kiến trúc tổng thể của hệ thống Document Management System.
* Thiết kế bảng DynamoDB theo đúng access patterns thực tế của ứng dụng.
* Tạo các Lambda Functions phục vụ CRUD tài liệu (Create, Read, Query, Delete).
* Thiết lập IAM Role tối ưu cho Lambda theo nguyên tắc least privilege.
* Kiểm thử API bằng test event và CloudWatch Logs.
* Chuẩn bị nền tảng cho việc tích hợp API Gateway và Amplify ở tuần kế tiếp.

**Phần 2 – Hiểu rõ cách ứng dụng DMS sẽ mở rộng trong các tuần tiếp theo**

* Nắm rõ cách tích hợp Cognito Authentication, Amplify Storage.
* Xác định vai trò của DynamoDB Streams trong search engine với OpenSearch.
* Hiểu quá trình triển khai toàn bộ backend bằng AWS SAM.
* Hiểu luồng CI/CD dự kiến sử dụng AWS CodePipeline.

---

###  Các công việc triển khai trong tuần

| Thứ | Công việc chi tiết                                                                                                                                                                                                                                                                                                                                                      | Bắt đầu | Hoàn thành | Nguồn |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------- | ---------- | ------ |
| 2   | **Phân tích kiến trúc tổng quan của hệ thống DMS**<br>• Hiểu mục tiêu ứng dụng: upload, xem, tải xuống, xoá và tìm kiếm tài liệu.<br>• Xác định các thành phần chính: Lambda, DynamoDB, S3, Cognito, API Gateway.<br>• Phân tích workflow: Upload → Lưu metadata → Xử lý tìm kiếm.<br>• Liệt kê API endpoints cần thiết cho backend.                                      | 10/11   | 10/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3   | **Thiết kế DynamoDB Table cho Document Metadata**<br>• Tạo bảng `Documents` với PK = `userId`, SK = `documentId`.<br>• Thiết kế attributes: filename, fileType, size, tags, createdAt, updatedAt.<br>• Phân tích access patterns: Query theo user, Get theo documentId, lọc theo tag.<br>• Chuẩn bị dữ liệu mẫu và test với AWS Console + CLI.                                | 11/11   | 11/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4   | **Tạo IAM Role cho Lambda Functions**<br>• Tạo Role `DMSLambdaRole`.<br>• Gán quyền DynamoDB CRUD: GetItem, Query, PutItem, DeleteItem.<br>• Gán quyền CloudWatch Logs để ghi log.<br>• Kiểm tra Trust Policy: `lambda.amazonaws.com`.<br>• Kiểm thử việc assume role bằng Lambda test environment.                                                                     | 12/11   | 12/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5   | **Viết Lambda Function CreateDocument**<br>• Validate input từ người dùng.<br>• Tự tạo `documentId` theo UUID.<br>• Lưu metadata vào DynamoDB bằng `put_item`.<br>• Ghi log input/output để phục vụ giám sát.<br>• Test bằng test event trên AWS Lambda + CloudWatch Logs.<br>• Tối ưu exception handling: missing fields, DynamoDB errors.                                  | 13/11   | 13/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6   | **Viết Lambda Function GetDocuments & GetDocumentById**<br>• Viết query để lấy tất cả tài liệu theo userId.<br>• Hỗ trợ phân trang bằng LastEvaluatedKey.<br>• Viết GetDocumentById để lấy chi tiết theo documentId.<br>• Trả về JSON chuẩn phục vụ front-end.<br>• Kiểm thử với dữ liệu mẫu trên DynamoDB.                                                               | 14/11   | 14/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 7   | **Viết Lambda Function DeleteDocument & Cleanup**<br>• Kiểm tra sự tồn tại của tài liệu trước khi xoá.<br>• Xoá metadata bằng `delete_item`.<br>• Chuẩn bị logic xoá file thật trên S3 (tuần tiếp theo).<br>• Ghi log chi tiết quá trình xoá để theo dõi.<br>• Dọn dẹp tài nguyên test, xoá các records không cần thiết.                                                   | 15/11   | 15/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Kết quả đạt được trong tuần 10 :

**1. Hoàn thiện bảng DynamoDB với thiết kế tối ưu**

* Xây dựng đầy đủ bảng `Documents` đáp ứng đầy đủ nhu cầu của một Document Management System.
* Thiết kế PK/SK để tối ưu cho Query theo user & lấy dữ liệu chi tiết.
* Chuẩn bị mô hình dữ liệu có thể mở rộng khi tích hợp OpenSearch hoặc DynamoDB Streams.

---

**2. Viết thành công bộ Lambda Functions phục vụ CRUD cho hệ thống**

* Tạo mới tài liệu với CreateDocument.
* Truy vấn danh sách tài liệu theo userId với GetDocuments.
* Lấy chi tiết theo documentId với GetDocumentById.
* Xoá tài liệu với DeleteDocument.
* Tất cả function đều tuân thủ chuẩn Serverless, logging đầy đủ, retry-safe.

---

**3. Áp dụng đầy đủ best practices về bảo mật và logging**

* IAM Role tuân thủ nguyên tắc least privilege.
* CloudWatch Logs dùng để trace toàn bộ luồng xử lý.
* Xử lý lỗi rõ ràng: input error, DynamoDB error, missing item.

---

**4. Hiểu rõ kiến trúc tổng thể của DMS và sẵn sàng cho tuần tiếp theo**

* Nắm workflow Authentication – API – Storage – Metadata.
* Hiểu cách Lambda sẽ kết nối với API Gateway trong tuần 11.
* Tạo nền tảng kỹ thuật để tuần sau triển khai Amplify Storage + Authentication.

---

###  Tóm tắt kiến thức đạt được

**AWS DynamoDB**
* Thiết kế bảng theo access patterns.
* Sử dụng Partition/Sort key đúng mục đích.
* Query, PutItem, GetItem, DeleteItem trong Boto3.

**AWS Lambda**
* Viết code serverless cho CRUD.
* Tạo IAM Role + policy tối ưu.
* Logging bằng CloudWatch Logs.
* Error handling chuẩn sản phẩm.

**DMS Architecture**
* Metadata lưu DynamoDB.
* File thật lưu ở S3.
* Authentication bằng Cognito.
* API được điều phối bằng Lambda + API Gateway.

---



