---
title: "Event 2"

weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---


# Báo cáo thu hoạch “Generative AI cùng Amazon Bedrock”

### Mục tiêu của buổi hội thảo

- Trang bị kiến thức cơ bản về Generative AI và điểm khác biệt so với Machine Learning cổ điển.
- Mô tả chi tiết dịch vụ Amazon Bedrock và các mô hình nền (Foundation Models).
- Hướng dẫn kỹ thuật RAG (Retrieval Augmented Generation) để phát triển ứng dụng AI thông minh, chính xác và giảm thiểu lỗi ảo giác.
- Giới thiệu hệ thống các dịch vụ AI chuyên sâu của AWS.
### Danh sách người trình bày

- **Lâm Tuấn Kiệt** - Kỹ sư DevOps cấp cao, FPT Software.
- **Danh Hoàng Hiếu Nghĩa** - Kỹ sư AI, Renova Cloud.
- **Đinh Lê Hoàng Anh** - Thực tập sinh Kỹ sư Đám mây, First Cloud AI Journey.


### Nội dung chính

#### Xu hướng chuyển đổi: Mô hình ML truyền thống và Mô hình nền

- **Mô hình ML truyền thống**: Tập trung vào những nhiệm vụ riêng lẻ (Specific tasks), yêu cầu dữ liệu được dán nhãn (Labeled data), quy trình Huấn luyện/Triển khai phức tạp cho từng mục tiêu.
- **Mô hình nền (FM)**: Được đào tạo trên khối lượng dữ liệu không cấu trúc khổng lồ (Unlabeled data), có thể thích ứng cho nhiều tác vụ khác nhau như: Tạo văn bản, Tóm tắt, Hỏi đáp, Chatbot.

#### Hệ sinh thái AI trên nền tảng AWS

- **Amazon Bedrock**: Nền tảng tập hợp các mô hình FM hàng đầu từ các đối tác của AWS (AI21 Labs, Anthropic, Cohere, Meta, Stability AI,...) và mô hình của chính Amazon.
- **Các Dịch vụ AI Chuyên biệt của AWS**: Có thể xem như những "giải pháp có sẵn", được tối ưu cho từng tác vụ cụ thể mà không cần huấn luyện mô hình:
    - Amazon Rekognition: Nhận diện đối tượng, Nhận diện khuôn mặt, Nhận diện cảm xúc, Nhận diện người nổi tiếng, Phân tích video - 0.001$/ảnh cho 1 triệu ảnh đầu.
    - Amazon Translate: Dịch văn bản đa ngôn ngữ thời gian thực với độ chính xác cao và văn phong tự nhiên.
    - Amazon Textract: Trích xuất thông tin có cấu trúc (bảng biểu, mẫu đơn) từ tài liệu scan hoặc PDF.
    - Amazon Transcribe: Chuyển đổi giọng nói thành văn bản.
    - Amazon Polly: Chuyển đổi văn bản thành giọng nói.
    - Amazon Comprehend: Phân tích cảm xúc văn bản, trích xuất từ khóa và phân loại chủ đề tự động.
    - Amazon Kendra: Cho phép tìm kiếm thông tin trong tài liệu nội bộ bằng ngôn ngữ tự nhiên.
    - Amazon Lookout: Phát hiện bất thường trong dây chuyền sản xuất hoặc thiết bị công nghiệp để bảo trì dự đoán.
    - Amazon Personalize: Xây dựng hệ thống đề xuất theo thời gian thực dựa trên công nghệ học máy.

#### Kỹ thuật Định hướng (Prompting): Chuỗi suy nghĩ (Chain of Thought - CoT)

- So sánh giữa **Định hướng Tiêu chuẩn** (hỏi trực tiếp kết quả) và **Định hướng Chuỗi Suy nghĩ**.
- CoT hướng dẫn mô hình lập luận từng bước để giải quyết các bài toán logic phức tạp, giúp cải thiện đáng kể độ chính xác so với việc chỉ đưa ra câu trả lời cuối.

#### Kỹ thuật RAG (Retrieval Augmented Generation) – Trọng tâm kỹ thuật

- **Vấn đề**: Giải quyết hiện tượng "ảo giác" và thiếu thông tin cập nhật của các mô hình LLM.
- **Giải pháp**: Kết hợp khả năng truy xuất (Retrieval) từ Cơ sở Kiến thức bên ngoài với khả năng tạo sinh (Generation) của LLM.
- **Quy trình thu thập dữ liệu (Data Ingestion)**:
    1. Dữ liệu thô (New data) → Chia nhỏ (Chunking).
    2. Xử lý qua Mô hình Embedding (ví dụ: Amazon Titan Text Embeddings V2.0).
    3. Lưu trữ dưới dạng vector vào Kho lưu trữ Vector (OpenSearch Serverless, Pinecone, Redis...).
- **RetrieveAndGenerate API**: API quản lý toàn bộ quy trình từ nhận đầu vào người dùng → tạo query embedding → truy xuất dữ liệu → bổ sung ngữ cảnh (augment prompt) → tạo ra câu trả lời.

### Kiến thức thu nhận được

#### Về Tư duy AI và Đám mây

- Hiểu rõ khi nào nên sử dụng **Các Dịch vụ AI Chuyên biệt** cho bài toán nhanh, cụ thể và khi nào dùng **Bedrock/GenAI** cho bài toán sáng tạo, phức tạp.
- Nắm vững tư duy thiết kế hệ thống RAG: Không chỉ đơn thuần là gọi API LLM, mà là bài toán quản lý dữ liệu và vector hóa để cung cấp ngữ cảnh chính xác cho AI tạo ra phản hồi tốt hơn.

#### Về Kiến trúc Kỹ thuật

- Kỹ thuật **Chuỗi Suy nghĩ (CoT)** là chìa khóa để tối ưu kết quả đầu ra của mô hình mà không cần tinh chỉnh (fine-tuning).
- Hiểu sâu vai trò của **Amazon Titan Embeddings V2.0** trong việc chuyển đổi văn bản đa ngôn ngữ thành vector (hỗ trợ 100+ ngôn ngữ, kích thước vector linh hoạt 256/512/1024).

### Kế hoạch áp dụng vào công việc
- Ứng dụng Amazon Bedrock cho dự án hiện tại: Amazon Rekognition để nhận diện món ăn từ ảnh nhằm tự động điền thông tin calo; Amazon Comprehend để phân tích văn bản nhằm chuẩn hóa tên món ăn và ghi nhận dữ liệu calo.
- Thử nghiệm áp dụng kỹ thuật RAG cho dự án hiện tại.
- Sử dụng Bedrock Agents để điều phối các tác vụ như truy vấn món ăn từ kho vector, tính toán mục tiêu calo và xây dựng thực đơn hàng ngày.

### Trải nghiệm tham gia sự kiện
Tham gia workshop Generative AI với Amazon Bedrock đem lại góc nhìn thực tế về cách xây dựng ứng dụng AI hiện đại, từ lý thuyết nền tảng đến triển khai thực tế.

#### Kiến thức thực tiễn từ chuyên gia
- Các diễn giả đã trình bày rõ ràng luồng dữ liệu trong một hệ thống **RAG**, giúp tôi hình dung được cách hoạt động phía sau các ứng dụng Chatbot hiện nay.
- Việc phân tích rõ ràng sự khác biệt giữa **Mô hình ML truyền thống** và **Generative AI** giúp tôi định hình lại chiến lược lựa chọn công nghệ cho các dự án sắp tới.

#### Trải nghiệm công nghệ
- Ấn tượng với **RetrieveAndGenerate API** của Bedrock vì nó giúp giảm đáng kể công sức lập trình thủ công cho phần kết nối giữa Kho Vector và LLM.
- Thấy được sức mạnh của **Amazon Titan Embedding** trong hỗ trợ đa ngôn ngữ, rất phù hợp với ứng dụng tại thị trường Việt Nam.

#### Bài học rút ra
- RAG là tiêu chuẩn mới: Để ứng dụng AI trong doanh nghiệp, RAG gần như bắt buộc để đảm bảo tính chính xác và bảo mật dữ liệu.
- Hệ sinh thái toàn diện: AWS cung cấp đầy đủ từ hạ tầng (Kho Vector) đến tầng mô hình (Bedrock) và tầng ứng dụng (Agents), giúp việc triển khai trở nên nhanh chóng hơn nhiều.

#### Một Số Hình Ảnh Khi Tham Gia Sự Kiện

![Hình ảnh](/images/2-Proposal/genaigenai.png)
![Hình ảnh](/images/2-Proposal/genai1.png)
![Hình ảnh](/images/2-Proposal/genai2.png)
![Hình ảnh](/images/2-Proposal/genai3.png)

> Tổng quan, sự kiện không chỉ cung cấp kiến thức kỹ thuật mà còn giúp tôi thay đổi cách tư duy thiết kế ứng dụng, hiện đại hóa hệ thống và phối hợp hiệu quả hơn giữa các nhóm.