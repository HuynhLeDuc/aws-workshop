---
title: "Worklog Tuần 12"

weight: 2
chapter: false
pre: " <b> 1.12 </b> "
---





### Mục tiêu trong tuần

**Phần 1 – Giới thiệu Amazon Bedrock & Foundation Models**

* Hiểu kiến trúc Amazon Bedrock và các dịch vụ chính.
* Học cách truy cập và sử dụng foundation models (FM) qua Bedrock.
* Tìm hiểu các mô hình: Claude, Llama, Mistral, Amazon Titan…
* Phân biệt mô hình sinh văn bản, embeddings và mô hình đa phương thức.

**Phần 2 – Xây dựng AI Agent với Bedrock Agent**

* Hiểu AI Agent là gì và cách hoạt động.
* Học các khái niệm:

  * Action groups  
  * Knowledge bases  
  * Orchestration  
  * Tích hợp Lambda functions  

* Cấu hình một AI Agent có khả năng gọi công cụ qua Lambda.

**Phần 3 – Sử dụng Knowledge Base cho Enterprise Search**

* Tạo Knowledge Base với vector embeddings.
* Kết nối Bedrock KB với tài liệu trong S3.
* Kiểm thử semantic search và RAG (Retrieval Augmented Generation).
* Tích hợp KB vào Bedrock Agent.

**Phần 4 – Tích hợp Front-end với Bedrock Agent**

* Xây dựng giao diện chat web để giao tiếp với Bedrock Agent.
* Thực hiện streaming response.
* Luồng hoạt động: Input người dùng → Agent → (KB, Lambda Tools) → Trả về đáp án.
* Triển khai front-end bằng Amplify Hosting.

---

### Các công việc triển khai trong tuần

| Thứ | Công việc chi tiết                                                                                                                                                                                          | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                 |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ------ |
| Hai | **Học nền tảng Amazon Bedrock**<br>• Khám phá danh mục mô hình.<br>• Test Claude / Llama 3 trong Playground.<br>• So sánh giá & khả năng.<br>• Tìm hiểu API Bedrock cơ bản.                                | 24/11 | 24/11 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| Ba | **Xây dựng ứng dụng Text Generation đầu tiên với Bedrock**<br>• Viết Lambda gọi Bedrock InvokeModel API.<br>• Test tham số temperature, max tokens.<br>• Xây dựng CLI nhỏ bằng SDK.                        | 25/11 | 25/11 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| Tư | **Tạo Bedrock Agent**<br>• Thiết lập cấu hình agent.<br>• Thêm instructions & guardrails.<br>• Tạo Action Group sử dụng Lambda.<br>• Kết nối agent với bảng DynamoDB thử nghiệm.                          | 26/11 | 26/11 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| Năm | **Xây dựng Knowledge Base (RAG System)**<br>• Tạo S3 bucket chứa tài liệu.<br>• Cấu hình embeddings (Titan Embeddings G1).<br>• Test hỏi đáp với PDF/CSV.<br>• Tích hợp KB vào Agent.                   | 27/11 | 27/11 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| Sáu | **Kiểm thử AI Agent End-to-End**<br>• Chat: Agent → KB → Lambda → Trả lời.<br>• Fix lỗi IAM, KMS.<br>• Kiểm thử hội thoại nhiều lượt.<br>• Thêm fallback & error handling.                                | 28/11 | 28/11 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| Bảy | **Xây dựng ứng dụng Chat Frontend bằng Amplify**<br>• Xây UI React Chat.<br>• Kết nối UI với Bedrock Agent qua API Gateway.<br>• Thực hiện streaming output.<br>• Deploy bằng Amplify Hosting.           | 29/11 | 29/11 | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Kết quả đạt được trong tuần 12 :

**1. Nắm vững Amazon Bedrock & Foundation Models**

* Biết cách gọi mô hình thông qua SDK.
* Thử nghiệm nhiều nhóm mô hình khác nhau.
* Hiểu các use-case: sinh văn bản, tóm tắt, sinh mã, embeddings.

---

**2. Xây dựng thành công một AI Agent hoàn chỉnh**

* Agent hiểu intent người dùng.
* Dùng Action Groups để chạy Lambda.
* Hỗ trợ reasoning nhiều bước.
* Có thể truy vấn DynamoDB qua Lambda.

---

**3. Tạo Knowledge Base tích hợp RAG**

* Tạo vector store từ tài liệu trong S3.
* Chạy thành công semantic search.
* Agent trả lời chính xác hơn nhờ tích hợp KB.

---

**4. Xây dựng giao diện chat kết nối Bedrock**

* Tạo UI chat bằng React.
* Tích hợp API Gateway để giao tiếp an toàn.
* Thực hiện thành công streaming response.
* Luồng hoàn chỉnh: UI → Agent → KB/Lambda → Trả lời.

---

### Tóm tắt kiến thức đã học

**Amazon Bedrock**

* Cung cấp quyền truy cập các mô hình mạnh nhất hiện nay.
* Fully managed, bảo mật cấp doanh nghiệp.
* Hỗ trợ sinh văn bản, embeddings và đa phương thức.

**Bedrock Agents**

* Agent có khả năng duy trì hội thoại và gọi công cụ.
* Action Groups cho phép tích hợp backend thực.
* Guardrails đảm bảo an toàn nội dung.

**Knowledge Bases**

* Embeddings tạo semantic search chính xác hơn.
* KB + Agent = hệ thống RAG hoàn chỉnh.
* Tự đồng bộ với tài liệu trong S3.

**Tích hợp & Triển khai**

* Lambda để xử lý logic backend.
* API Gateway để kết nối từ frontend.
* Amplify để deploy UI.


