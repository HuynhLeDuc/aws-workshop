---
title: "Bản đề xuất"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# FoodMind Recommender Platform For Prompt-IPoG
## Giải pháp AWS Serverless hợp nhất cho gợi ý quán ăn thông minh dựa trên trải nghiệm người dùng 

### 1. Tóm tắt điều hành  
**AI Food Recommender Platform** là nền tảng web thông minh được thiết kế để giúp người dùng khám phá quán ăn phù hợp dựa trên dữ liệu thực tế từ đánh giá và cảm xúc của khách hàng. Nền tảng sử dụng mô hình AI cảm xúc (Sentiment Analysis) được triển khai trên Amazon SageMaker, kết hợp với AWS Bedrock để xử lý dữ liệu thô (đánh giá của người dùng, mô tả quán ăn), tạo ra cơ sở dữ liệu chuẩn hóa phục vụ cho việc gợi ý.

Giao diện web được xây dựng trên AWS Amplify (Next.js), cho phép người dùng tìm kiếm và khám phá quán ăn thông qua thanh tìm kiếm thông minh dựa trên embedding. Dữ liệu được lưu trữ và truy vấn qua Amazon RDS, đảm bảo hiệu năng cao và khả năng mở rộng linh hoạt.
Giải pháp tập trung vào sự kết hợp giữa AI và dữ liệu thực tế để hỗ trợ ra quyết định tìm quán ăn dựa trên cảm nhận, trải nghiệm và sở thích. 

### 2. Tuyên bố vấn đề  
**Vấn đề hiện tại**  
Trong bối cảnh số lượng quán ăn ngày càng tăng, việc tìm kiếm một địa điểm phù hợp với sở thích và nhu cầu cá nhân trở nên khó khăn. Nhiều ứng dụng như Google Maps hiện chủ yếu hiển thị danh sách quán ăn dựa trên xếp hạng hoặc quảng cáo, chưa thực sự mang lại trải nghiệm tìm kiếm cá nhân hóa. Người dùng phải đọc hàng chục bình luận mới có thể cảm nhận được chất lượng phục vụ, món ăn hoặc không gian. Việc phân tích cảm xúc và mô tả dữ liệu vẫn còn thủ công, thiếu khả năng cá nhân hóa.

**Giải pháp** 
Nền tảng AI FoodMind Recommender sử dụng dữ liệu từ những đánh giá của người dùng của các quán ăn trên Google Map, sau đó:
- **Amazon S3** lưu dữ liệu thô đã được thu thâp về   
- **AWS Bedrock** xử lý dữ liệu thô để tạo mô tả, embedding, và trích xuất yếu tố liên quan (loại món, cảm xúc, chất lượng phục vụ, mức giá...).
- **Amazon SageMaker** triển khai mô hình cảm xúc (Sentiment Analysis) lấy từ Hugging Face để đánh giá sentiment trong các bình luận.

- **Amazon RDS** lưu trữ dữ liệu đã xử lý và embedding cho việc tìm kiếm ngữ nghĩa.

- **AWS Amplify** triển khai web UI (Next.js) và tích hợp Amazon Cognito để quản lý người dùng.

- **AWS Lambda** và **API Gateway** kết nối frontend – backend – AI model.

Hệ thống cho phép người dùng tìm kiếm bằng ngôn ngữ tự nhiên như “phở ngon, phục vụ nhanh ở quận 3”, và nhận kết quả phù hợp dựa trên cảm xúc, chất lượng, và mô tả thực tế.

**Lợi ích và hoàn vốn đầu tư (ROI)**  

- Tối ưu hóa trải nghiệm tìm kiếm quán ăn theo cảm xúc thay vì chỉ theo rating.

- Tạo cơ sở dữ liệu chuẩn hóa cho nghiên cứu về AI trong lĩnh vực ẩm thực và hành vi người dùng.

- Chi phí thấp nhờ kiến trúc serverless (tận dụng free tier AWS).

- ROI ước tính: hoàn vốn trong 6 tháng thông qua tiết kiệm thời gian phát triển và tái sử dụng mô hình AI đã có sẵn.

- Chi phí ước tính: khoảng 15–20 USD/tháng.

### 3. Kiến trúc giải pháp  
Nền tảng áp dụng kiến trúc AI-as-a-Service kết hợp AWS Serverless, đảm bảo khả năng mở rộng linh hoạt, chi phí tối ưu và dễ bảo trì. Dữ liệu được thu thập lưu trữ tạm thời trong Amazon S3, sau đó được xử lý bởi AWS Lambda kết hợp AWS Bedrock để chuẩn hóa, sinh mô tả và tạo embedding. Amazon SageMaker được sử dụng để phân tích cảm xúc trong bình luận, kết quả được lưu trữ trong Amazon RDS. AWS Amplify lưu trữ giao diện web Next.js và Amazon Cognito đảm bảo xác thực người dùng an toàn. Kiến trúc được trình bày chi tiết bên dưới:

![FoodMind Recommender Platform Architecture](/images/2-Proposal/Architecture.png)

**Dịch vụ AWS sử dụng**    
- **AWS Lambda**: Xử lý logic ứng dụng và gọi các dịch vụ AI (3 hàm).
- **Amazon S3**: Lưu trữ dữ liệu thô
- **Amazon SageMaker**: Triển khai mô hình sentiment từ Hugging Face.   
- **Amazon API Gateway**: Giao tiếp với ứng dụng web.    
- **AWS Bedrock**: Sinh mô tả, tạo embedding, chuẩn hóa dữ liệu.
- **Amazon RDS (PostgreSQL)**: Lưu dữ liệu quán ăn đã chuẩn hóa và embedding.  
- **AWS Amplify**: Lưu trữ giao diện web Next.js.  
- **Amazon Cognito**: Quản lý người dùng và đăng nhập.  

**Thiết kế thành phần**  

- **Thu Thập dữ liệu**: Thu thập dữ liệu thô về lưu tạm thời ở Amazon S3
- **Triển khai mô hình**: Deploy mô hình cảm xúc trên SageMaker Endpoint.  
- **Xử lý dữ liệu**: AWS Bedrock và SageMaker lấy dữ liệu từ Amazon S3 sau đó chuẩn hóa và lưu vào Amazon RDS 
- **Xây dựng Backend**: Lambda, API Gateway, kết nối RDS.  
- **Giao diện web**: Lưu trữ ứng dụng Next.js với thanh tìm kiếm thông minh cho việc tìm kiếm để gợi ý quán ăn từ trải nghiệm của người dùng.
- **Quản lý người dùng**: Amazon Cognito quản lý quyền truy cập của người dùng.

### 4. Triển khai kỹ thuật  
**Các giai đoạn triển khai** 
- Nghiên cứu và vẽ kiến trúc: Thiết kế pipeline AI + Cloud, kiểm tra tính khả thi và vẽ sơ đồ hệ thống AWS (5 Tuần đầu tiên).  
- Tính toán chi phí và tối ưu giải pháp: Điều chỉnh kiến trúc để tối ưu chi phí (Tuần 6)
- Phát triển, Kiểm thử và triển khai: lưu dữ liệu thô, Các dịch vụ AWS chuẩn hóa và lưu trữ dữ liệu sạch sau đó tạo giao diện wed với Next.js, test tốc độ và vận hành sản phẩm (Tuần 7 - tuần 11).  

**Yêu cầu kỹ thuật**  
- *Dữ liệu trải nghiệm cá nhân*: Dữ liệu (đánh giá, xếp hạng, dịch vụ, không gian, ...). Lên lịch gọi Lambda lấy dữ liệu 1 lần/tháng và xử lý lấy dữ liệu mới. 
- *Nền tảng gợi ý quán ăn*: Kiến thức thực tế về AWS Amplify (lưu trữ Next.js), Lambda, S3 (2 bucket), Cognito, Bedrock, RDS, API Gateway. Sử dụng AWS CDK/SDK để lập trình. Next.js giúp giảm tải Lambda cho ứng dụng web.  

### 5. Lộ trình & Mốc triển khai  
- *Thực tập (Tháng 1–3)*:  
    - Tháng 1: Học AWS và nâng cấp phần cứng.  
    - Tháng 2: Thiết kế và điều chỉnh kiến trúc.  
    - Tháng 3: Triển khai, kiểm thử, đưa vào sử dụng.  
- *Sau triển khai*: Theo dõi, cải tiến hệ thống gợi ý và mở rộng dữ liệu trong vòng 1 năm.

### 6. Ước tính ngân sách  
Có thể xem chi phí trên [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01)  
Hoặc tải [tệp ước tính ngân sách](../attachments/budget_estimation.pdf).  

**Chi phí hạ tầng**

- AWS Amplify: 0,50 USD/tháng (~100 MB, traffic thấp).

- AWS Lambda: 0,20 USD/tháng ( 100.000 request/tháng, thời gian chạy trung bình <1s ).

- Amazon API Gateway: 0,10 USD/tháng ( 50.000 request REST API/tháng).

- Amazon RDS (PostgreSQL): 0,00 USD/tháng ( Sử dụng Free Tier 750 giờ/tháng ).

- AWS S3 (Standard): 0,10 USD/tháng ( 2 GB dữ liệu ).

- Amazon SageMaker Endpoint: 4,00 USD/tháng ( ~100 giờ/tháng).

- AWS Bedrock: 3,00 USD/tháng  ( vài nghìn token/tháng).

- Amazon Cognito: 0,00 USD/tháng ( <50 người dùng hoạt động (Free Tier)).

**Tổng**:  ~8 USD/tháng, ~96 USD/12 tháng

### 7. Đánh giá rủi ro  
*Ma trận rủi ro*  
- Mất mạng: Ảnh hưởng trung bình, xác suất trung bình.  
- Quá tải request API: Ảnh hưởng Trung bình, xác suất Trung bình. 
- Sai lệch dữ liệu cảm xúc: Ảnh hưởng Cao, xác suất Thấp. 
- Vượt ngân sách: Ảnh hưởng trung bình, xác suất thấp.  

*Chiến lược giảm thiểu*  
- Mạng: Lưu trữ cục bộ trên Raspberry Pi với Docker.  
- Quá tải request API: Giới hạn truy cập qua API Gateway
- Sai lệch dữ liệu cảm xúc: Hiệu chỉnh mô hình định kỳ
- Chi phí: Cảnh báo ngân sách AWS, tối ưu dịch vụ.  

*Kế hoạch dự phòng*  
- Quay lại thu thập thủ công nếu AWS gặp sự cố.  
- Sử dụng CloudFormation để khôi phục cấu hình liên quan đến chi phí.  

### 8. Kết quả kỳ vọng  
**Trải nghiệm người dùng nâng cao**: Gợi ý quán ăn dựa trên cảm xúc và mô tả thực tế.

**Tích hợp AI thực tế**: Ứng dụng Bedrock + SageMaker trong hệ thống sản phẩm hoàn chỉnh.

**Nền tảng dữ liệu tái sử dụng**: Cho các nghiên cứu về AI cảm xúc, hành vi khách hàng.

**Khả năng mở rộng**: Có thể mở rộng thêm yếu tố như “vị trí”, “xu hướng ẩm thực”, “món phổ biến theo mùa”.