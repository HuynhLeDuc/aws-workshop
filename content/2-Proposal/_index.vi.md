---
title: "Bản đề xuất"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# FoodMind Recommender Platform For Prompt-IPoG
## Giải pháp AWS Serverless hợp nhất cho việc theo dõi và gợi ý bữa ăn cá nhân hóa. 

### 1. Tóm tắt điều hành  
**FoodMind Recommender Platform** là nền tảng web thông minh được thiết kế để trở thành một trợ lí ăn uống cá nhân thông minh. Nền tảng tự động tính toán calo mục tiêu (TDEE) dựa trên hồ sơ người dùng, sử dụng **AWS Bedrock (AI Tạo sinh)** để cho phép người dùng ghi log bữa ăn bằng ngôn ngữ tự nhiên (ví dụ: "tôi vừa ăn 1 bát phở bò"). Hệ thống cung cấp một tính năng gợi ý bữa ăn (Sáng/Trưa/Tối) thông minh, tự động **"lọc"** các món ăn dựa trên mục tiêu calo và các ràng buộc sức khỏe (ví dụ: "dị ứng", "bệnh gout") của người dùng.

Toàn bộ giải pháp được xây dựng trên **kiến trúc serverless** với giao diện sử dụng AWS Amplify (Frontend), API Gateway, AWS Lambda, và Amazon DynamoDB (Backend). Cho phép người dùng có thể  nhận được gợi ý các món ăn trong ngày dựa trên lượng calo được tính toán theo người dùng sử dụng cần tiêu thụ trong ngày. Dữ liệu được lưu trữ và truy vấn qua Amazon DynamoDB, đảm bảo hiệu năng cao và mở rộng linh hoạt.

Giải pháp tập trung vào sự kết hợp giữa AI và dữ liệu thực tế để hỗ trợ ra quyết định tìm món ăn linh hoạt và thiết kế **dashboard** để có thể xem quá trình theo dõi bữa ăn hàng ngày hiệu quả. 

### 2. Tuyên bố vấn đề  
**Vấn đề hiện tại**  

Nhiều người dùng gặp khó khăn trong việc quản lý chế độ ăn uống hàng ngày — không biết nên ăn bao nhiêu calo, món nào phù hợp với mục tiêu cá nhân cho mỗi ngày. Việc ghi chép thủ công và tra cứu dinh dưỡng gây mất thời gian, thiếu chính xác và không có tính cá nhân hóa. 

**Giải pháp** 

FoodMind Recommender Platform ứng dụng **AI và AWS Cloud** để tự động hóa toàn bộ quy trình theo dõi và gợi ý bữa ăn:

- **Tự động hóa Mục tiêu:** Hệ thống tự động tính toán Calo Mục tiêu cho người dùng (dựa trên công thức Mifflin-St Jeor) ngay khi họ cập nhật hồ sơ.
- **Tự động hóa Gợi ý:** Hệ thống cung cấp API GET /recommendations sử dụng **"logic nghiệp vụ"** (do Lambda thực thi) để "lọc" (filter) kho dữ liệu món ăn, dựa trên Calo Mục tiêu (ví dụ: bữa trưa < 700 calo) và Luật cấm Bệnh lý (ví dụ: không chứa "thịt đỏ" cho bệnh gout).
- **Tự động hóa Ghi log (AI Logging):** Hệ thống cung cấp API POST /log-food sử dụng **AWS Bedrock** để "bóc tách" (parse) ngôn ngữ tự nhiên của người dùng. Hệ thống tự tra cứu calo và lưu vào nhật ký.
- **Tự động hóa Học hỏi:** Khi người dùng log một món ăn mới (ví dụ: "bún đậu mắm tôm") mà hệ thống không biết, **AWS Bedrock** sẽ được dùng để "ước tính" calo và "tự động lưu" món mới này vào kho tri thức.
- **Theo dõi Trực quan:** Cung cấp **dashboard (trên Amplify)** hiển thị lịch sử ăn uống 7 ngày qua, giúp người dùng quan sát và theo dõi chế độ ăn uống cá nhân.

Người dùng chỉ cần nhập thông tin, hệ thống sẽ tự động hiểu, phân tích và đề xuất–gợi ý bữa ăn phù hợp với sức khỏe và mục tiêu cá nhân.

**Lợi ích và hoàn vốn đầu tư (ROI)**  

- Tiết kiệm thời gian theo dõi dinh dưỡng, loại bỏ thao tác thủ công.
- Mang đến trải nghiệm AI thực tế, có tính cá nhân hóa cao.
- Tạo cơ sở dữ liệu chuẩn hóa cho nghiên cứu về AI trong lĩnh vực ẩm thực và cá nhân hóa bữa ăn.
- Chi phí thấp nhờ kiến trúc serverless.
- Dễ mở rộng và tái sử dụng mô hình cho các ứng dụng chăm sóc sức khỏe khác.
- ROI ước tính: hoàn vốn trong 6 tháng thông qua tiết kiệm thời gian phát triển và tái sử dụng mô hình AI đã có sẵn.
- Chi phí ước tính: khoảng **10–15 USD/tháng**.

### 3. Kiến trúc giải pháp  
Nền tảng được xây dựng hoàn toàn trên mô hình **AI-as-a-Service** kết hợp **AWS Serverless**, đảm bảo hiệu năng cao, bảo mật và khả năng mở rộng linh hoạt. Dữ liệu dĩnh dưỡng về lượng calo của các món ăn được thu thập lưu trữ trong **Amazon DynamoDB**, sau đó sẽ gợi ý bữa ăn dựa phù hợp với lượng tính toán Calo mục tiêu. **Amazon Bedrock** được sử dụng để phân tích xử lý ngôn ngữ tự nhiên của người dùng tra cứu Calo món ăn và lưu vào **Amazon DynamoDB**. AWS Amplify lưu trữ giao diện web Next.js và **Amazon Cognito** đảm bảo xác thực người dùng an toàn. Kiến trúc được trình bày chi tiết bên dưới:

![alt text](/images/2-Proposal/Architecture.jpg)

**Dịch vụ AWS sử dụng**

**AWS Amplify:** Triển khai và lưu trữ giao diện web của nền tảng (Next.js), kết nối CI/CD trực tiếp với GitLab để tự động build và deploy.
**Amazon Route 53 + AWS WAF + Amazon CloudFront:** Tầng Edge bảo vệ và phân phối nội dung nhanh chóng, đảm bảo bảo mật và hiệu năng truy cập toàn cầu.
**Amazon Cognito:** Quản lý xác thực người dùng, đăng nhập và phân quyền truy cập an toàn cho từng tài khoản.
**Amazon API Gateway:** Cung cấp endpoint cho các tác vụ như GET /Recommendation, POST /Log, GET /Dashboard, kết nối trực tiếp với Lambda.
**AWS Lambda (Private Subnet):** Xử lý logic ứng dụng, gọi Bedrock và DynamoDB thông qua các VPC Endpoint để đảm bảo bảo mật và hiệu năng.
**AWS Bedrock:** Sinh mô tả món ăn, chuẩn hóa log bữa ăn bằng ngôn ngữ tự nhiên và lưu vào DynamoDB phục vụ gợi ý bữa ăn cá nhân hóa.
**Amazon DynamoDB:** Lưu trữ dữ liệu người dùng, nhật ký ăn uống, mục tiêu calo, và dữ liệu gợi ý – đảm bảo khả năng mở rộng linh hoạt.
**AWS Secrets Manager:** Bảo mật thông tin xác thực (API Key, Bedrock credentials) cho Lambda và dịch vụ backend.
**Amazon CloudWatch & AWS CloudTrail:** Theo dõi log, truy cập và hiệu năng toàn hệ thống; hỗ trợ giám sát và khôi phục sự cố.
**Amazon S3:** Lưu trữ log.
**AWS IAM:** Quản lý phân quyền truy cập chi tiết giữa các dịch vụ và người dùng.
**Amazon VPC:** Cách ly Lambda trong subnet riêng, đảm bảo kết nối an toàn nội bộ giữa Lambda – DynamoDB – Bedrock.

**Thiết kế thành phần**  

- **Quản lý người dùng**: Amazon Cognito quản lý quyền truy cập của người dùng.
- **Phân phối & Bảo vệ truy cập:** Route 53 định tuyến tên miền, AWS WAF bảo vệ khỏi tấn công web (SQL Injection, DDoS) và CloudFront tăng tốc độ tải nội dung và phân phối toàn cầu.
- **Giao diện web**: Amplify lưu trữ ứng dụng Next.js.
- **Ghi nhật ký & gợi ý bữa ăn:** Người dùng nhập dữ liệu (text) lưu vào DynamoDB, Lambda gợi ý món ăn theo số tính toán Calo.
- **Phân tích bữa ăn:** Lambda gọi Bedrock xử lý thông tin bữa ăn bằng ngôn ngữ tự nhiên của user nhập vào, bóc tách và tìm nhật ký Calo của món và lưu lại DynamoDB nếu món mới.
- **Hiển thị dashboard:** Amplify hiển thị biểu đồ calo theo ngày/tuần/tháng sau khi user cập nhật bữa ăn.
- **Xác thực & bảo mật:** Cognito đảm bảo đăng nhập an toàn và quản lý user.
- **Giám sát & theo dõi:** Amazon CloudWatch theo dõi log, hiệu năng Lambda, AWS CloudTrail lưu lại lịch sử thao tác và truy cập dịch vụ. 


### 4. Triển khai kỹ thuật  
**Các giai đoạn triển khai** 
- Nghiên cứu và Thiết kế: Thiết kế pipeline AI + Cloud, kiểm tra tính khả thi và vẽ sơ đồ hệ thống AWS (5 Tuần đầu tiên).  
- Tính toán chi phí và tối ưu giải pháp: Kiểm tra lại chi phí các dịch vụ trong kiến trúc để tối ưu chi phí (Tuần 6).
- Phát triển, Kiểm thử và triển khai: Lưu dữ liệu ban đầu, sau đó tạo giao diện wed với Next.js, kiểm thử các luồng tính năng API, tốc độ và vận hành sản phẩm (Tuần 7 - tuần 11).  

**Yêu cầu kỹ thuật**  
- *Dữ liệu Calo món ăn*: Thu thập dữ liệu ban đầu và dùng script AWS SDK (Boto3) để nạp vào DynamoDB. 
- *Nền tảng gợi ý quán ăn*: Kiến thức thực tế về AWS Amplify (lưu trữ Next.js), S3 (bucket), Cognito. Kiến thức thực tế về AWS Serverless (Lambda, DynamoDB, API Gateway), thiết kế schema DynamoDB (PK, SK), và cách dùng Bedrock API.
### 5. Lộ trình & Mốc triển khai  
- *Thực tập (Tháng 1–3)*:  
    - Tháng 1: Học và làm chủ các dịch vụ AWS.  
    - Tháng 2: Thiết kế và điều chỉnh kiến trúc.  
    - Tháng 3: Triển khai, kiểm thử, đưa vào sử dụng.  
- *Sau triển khai*: Theo dõi, cải tiến hệ thống gợi ý và mở rộng dữ liệu trong vòng 1 năm.

### 6. Ước tính ngân sách  
Có thể xem chi phí trên [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01).
Hoặc tải [tệp ước tính ngân sách](../attachments/budget_estimation.pdf).  

**Chi phí hạ tầng**

- AWS Amplify: 0.50 USD/tháng (~100 MB, traffic thấp).

- AWS Lambda: 0.20-0.30 USD/tháng ( 100.000 request/tháng, thời gian chạy trung bình <1s ).

- Amazon API Gateway: 0.10-o.20 USD/tháng ( 50.000 request REST API/tháng).

- Amazon DynamoDB: 0.10-0.30 USD/tháng ( 50 MB dữ liệu, ~20.000 request/tháng).

- Amazon S3 (lưu trữ log/back-up): 0.10 USD/tháng (<2GB).

- AWS Bedrock: 3,00-500 USD/tháng  ( vài nghìn token/tháng).

- CloudWatch + CloudTrail + IAM etc: ~ 0.10-USD.

- Amazon Cognito: 0.00 USD/tháng ( <50 người dùng hoạt động (Free Tier)).

**Tổng**:  ~4-6 USD/tháng, ~50-75 USD/12 tháng.

### 7. Đánh giá rủi ro  
*Ma trận rủi ro*    
- Lỗi AI xử lý sai: Ảnh hưởng cao, xác suất thấp. 
- Quá tải request: Ảnh hưởng trung bình, xác suất Thấp. 
- Vượt ngân sách: Ảnh hưởng trung bình, xác suất thấp.  
- Lỗi logic: Ảnh hưởng trung bình, xác suất thấp.   

*Chiến lược giảm thiểu*  
- Sai lệch AI: Dùng "prompt engineering" kỹ lưỡng.
- Quá tải request API: Giới hạn truy cập qua API Gateway.
- Chi phí: Cảnh báo ngân sách AWS, tối ưu dịch vụ.  
- Logic: Điều chình code kĩ lưỡng với các hàm lambda.

*Kế hoạch dự phòng*  
- Quay lại thu thập thủ công nếu AWS gặp sự cố.  
- Sử dụng CloudFormation để khôi phục cấu hình liên quan đến chi phí.  

### 8. Kết quả kỳ vọng  
**Trải nghiệm người dùng nâng cao**: Cung cấp một trợ lý bữa ăn "thông minh", xóa bỏ mọi rào cản thủ công trong việc ghi log và chọn món.

**Tích hợp AI thực tế**: Ứng dụng Bedrock trong hệ thống sản phẩm hoàn chỉnh.

**Tạo nền tảng dữ liệu dinh dưỡng**: Có thể mở rộng, phục vụ nghiên cứu AI & y tế.

**Khả năng mở rộng**: tích hợp thêm phân tích hình ảnh món ăn, chat AI coach, và ứng dụng di động.