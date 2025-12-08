---
title: "Worklog Tuần 5"

weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---
### Mục tiêu tuần 5:

* Hiểu sâu về **Amazon S3** — mô hình object storage, các tính năng chính và các trường hợp sử dụng.  
* Thực hành **host static website** trên S3: kích hoạt tính năng, cấu hình public access, kiểm tra và tối ưu hiệu năng.  
* Học cách **bảo mật bucket** (Block Public Access, IAM policy, Bucket Policy) đồng thời cho phép public object khi cần.  
* Thực hiện các thao tác quản lý nâng cao: **Versioning**, **S3 Transfer Acceleration**, **S3 Batch / S3 Replication (sao chép sang region khác)**, **di chuyển object**.  
* Biết cách **dọn dẹp tài nguyên** để tránh phát sinh chi phí và nắm được các best practices khi dùng S3.

---


### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ---------- | ------------- | ---------------- | --------------- |
| 2 | **Chuẩn bị môi trường & lý thuyết cơ bản** <br>&emsp; + Tổng quan S3: object, bucket, key, region, storage class (STANDARD, IA, GLACIER) <br>&emsp; + Độ bền & tính sẵn sàng (11 nines) <br>&emsp; + Trường hợp sử dụng (static website, backup, data lake) | 06/10/2025 | 06/10/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3 | **Tạo bucket S3 & bật Static Website Hosting** <br>&emsp; + Tạo bucket (quy tắc đặt tên, chọn region) <br>&emsp; + Tải file index.html / error.html lên bucket <br>&emsp; + Bật Static website hosting và lấy endpoint để kiểm tra | 07/10/2025 | 07/10/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4 | **Cấu hình Block Public Access & Public Object + Bucket Policy** <br>&emsp; + Hiểu các thiết lập Block Public Access ở cấp tài khoản và bucket <br>&emsp; + Cấu hình Bucket Policy cho phép truy cập công khai chỉ với object cụ thể (index.html) <br>&emsp; + Kiểm tra truy cập từ trình duyệt <br>&emsp; + Thực hành dọn dẹp quyền public và xác minh bảo mật | 08/10/2025 | 08/10/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5 | **Tăng tốc Static Website & Bảo mật nâng cao** <br>&emsp; + So sánh dùng S3 + CloudFront vs S3 Transfer Acceleration vs AWS Amplify Hosting <br>&emsp; + Thực hành bật S3 Transfer Acceleration và kiểm nghiệm tốc độ (curl thử từ nhiều vùng) <br>&emsp; + (Tuỳ chọn) Tạo CloudFront distribution trỏ tới S3 để bật HTTPS và CDN <br>&emsp; + Tích hợp giám sát bằng CloudWatch và theo dõi chi phí | 09/10/2025 | 09/10/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6 | **Versioning, Lifecycle & Replication + Dọn dẹp tài nguyên** <br>&emsp; + Bật Bucket Versioning, thử overwrite và khôi phục version cũ <br>&emsp; + Thiết lập lifecycle rules: chuyển object sang IA/Glacier sau N ngày <br>&emsp; + Cấu hình S3 Replication (CRR) sao chép sang region khác, tạo IAM role phù hợp <br>&emsp; + Di chuyển object giữa bucket/region (copy, move, sync) <br>&emsp; + Dọn dẹp tài nguyên: xóa object, tắt transfer acceleration, gỡ CloudFront (nếu có), xóa bucket thử nghiệm | 10/10/2025 | 10/10/2025 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Kết quả đạt được trong tuần 5:

**Cấu hình và thao tác cơ bản:**
- Thiết lập và cấu hình **AWS CLI** để làm việc với Amazon S3 (Access Key, Secret Key, Region mặc định).  
- Kiểm tra kết nối và thông tin cấu hình bằng các lệnh:  
  - `aws configure list`  
  - `aws s3 ls` để liệt kê bucket hiện có.  
  - `aws s3api list-buckets` để lấy thông tin chi tiết bucket.  
- Tạo và xóa bucket qua CLI:  
  - `aws s3 mb s3://ten-bucket`  
  - `aws s3 rb s3://ten-bucket --force`  

 **Thực hành Static Website Hosting:**
- Tạo bucket mới, upload `index.html` và `error.html`.  
- Bật **Static Website Hosting** và truy cập được website qua endpoint công khai.  
- Kiểm tra lỗi 403/404 khi truy cập sai đường dẫn, xác minh error.html hoạt động đúng.  

**Thiết lập bảo mật và quyền truy cập:**
- Bật và tắt **Block Public Access** ở cả cấp tài khoản và bucket để hiểu cơ chế.  
- Cấu hình **Bucket Policy** cho phép public duy nhất object `index.html`.  
- Thử public và private object để kiểm tra chính xác quyền truy cập.  

**Quản lý dữ liệu và tối ưu hiệu năng:**
- Bật **Versioning** trên bucket, upload nhiều version cho cùng object, và thực hành khôi phục version cũ.  
- Thiết lập **Lifecycle Rules** để chuyển object ít truy cập sang lớp lưu trữ **IA** hoặc **Glacier**.  
- Thử **S3 Transfer Acceleration** và đo sự khác biệt tốc độ upload từ các region khác nhau bằng `curl`.  

**Quản lý nâng cao và di chuyển dữ liệu:**
- Cấu hình **Cross-Region Replication (CRR)** để sao chép object sang bucket ở region khác, hiểu vai trò của IAM Role (Replication Role).  
- Dùng các lệnh CLI:  
  - `aws s3 cp`, `aws s3 mv`, `aws s3 sync` để di chuyển hoặc đồng bộ dữ liệu giữa các bucket.  
- Kiểm tra và xác nhận object replicated thành công trên bucket đích.  

**Dọn dẹp & tối ưu chi phí:**
- Xóa toàn bộ object test, tắt Transfer Acceleration và CloudFront (nếu dùng).  
- Tắt hosting hoặc xóa bucket thử nghiệm để tránh phát sinh chi phí.  
- Tổng hợp **best practices**:  
  - Không public toàn bộ bucket.  
  - Dùng Versioning + Lifecycle để tiết kiệm chi phí.  
  - Giám sát dung lượng qua S3 Storage Lens và đặt **budget alert** qua CloudWatch.


---

### Ghi chú :

- **Không để bucket public toàn bộ** trừ khi thật sự cần; dùng **Bucket Policy** để chỉ public object cụ thể (index.html).  
- **Bật Block Public Access** ở cấp tài khoản để tránh mở nhầm; vượt qua Block Public Access chỉ khi bạn hiểu rõ rủi ro.  
- **Dùng Versioning + Lifecycle**: versioning giúp khôi phục nhầm lẫn; lifecycle rules giúp tự động chuyển dữ liệu sang lớp rẻ hơn (IA/Glacier).  
- **Sử dụng CloudFront** nếu cần HTTPS, custom domain hoặc tối ưu hiệu năng toàn cầu; **S3 Transfer Acceleration** phù hợp khi upload/ download từ client ở xa cần tăng tốc — nhưng chi phí có thể cao hơn.  
- **AWS Amplify Hosting** là lựa chọn hiện đại, tự động hóa deploy từ repo, cung cấp HTTPS mặc định và CDN — dùng nếu bạn host site tĩnh mà muốn ít cấu hình.  
- **Bảo mật**: sử dụng IAM policy chặt chẽ, tránh chèn Access Key trong mã nguồn; sử dụng IAM Role cho EC2 / Lambda.  
- **Theo dõi & Báo cáo chi phí**: bật CloudWatch + S3 Storage Lens, và tạo budget để tránh phát sinh chi phí bất ngờ.  
- **Kiểm thử trước khi xóa**: khi xóa bucket có Versioning, cần xóa mọi versions & delete markers, chú ý chi phí chuyển dữ liệu khi replicate hoặc restore từ Glacier.  

---

### Tóm tắt kiến thức đạt được:

- Vận hành S3 ở mức production: hosting, bảo mật, tối ưu chi phí, versioning và replication.  
- Lựa chọn công cụ tối ưu cho hosting static site: **Amplify (khuyến nghị)**, **CloudFront + S3** hoặc **S3 (đơn giản)** tùy nhu cầu.  
- Thực hiện các tác vụ quản lý dữ liệu lớn: di chuyển, sao chép sang region khác, và tự động hoá bằng lifecycle rules.  
- Biết dọn dẹp an toàn và tối ưu để tránh chi phí phát sinh không mong muốn.  

---