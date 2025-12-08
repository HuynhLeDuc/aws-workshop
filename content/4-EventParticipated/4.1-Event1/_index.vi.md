---
title: "Event 1"

weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---



#  Bài Thu Hoạch Sự Kiện “Cloud Day” 

### Mục Đích Của Sự Kiện

Sự kiện “Cloud Day” được tổ chức nhằm giới thiệu xu hướng phát triển AI tại Việt Nam, đặc biệt là bước tiến từ Generative AI sang Agentic AI. Các diễn giả cũng trình bày các giải pháp mới của AWS như **Amazon Bedrock**, **AgentCore**, và **SageMaker Unified Studio** – những công cụ hỗ trợ doanh nghiệp xây dựng, triển khai và vận hành AI agent một cách nhanh chóng và an toàn.

---

### Diễn Giả

* **Kien Nguyen** – Solutions Architect
* **Jun Kai Loke** – AI/ML Specialist SA, AWS
* **Tamelly Lim** – Storage Specialist SA, AWS
* **Binh Tran** – Senior Solutions Architect, AWS
* **Taiki Dang** – Solutions Architect, AWS
* **Michael Armentano** – Principal WW GTM Specialist, AWS

---

### Nội Dung Chính

#### Tác động của AI đối với kinh tế Việt Nam

* AI dự kiến đóng góp **120–130 tỷ USD** (khoảng 25% GDP) vào năm 2040.
* Quy mô thị trường AI hiện đạt **750 triệu USD**, tăng trưởng **15–18% mỗi năm**.
* Việt Nam có khoảng **765 startup AI**, xếp **thứ 2 trong ASEAN**.
* Dù tiềm năng lớn, Việt Nam vẫn đang trong giai đoạn đầu, cần đầu tư thêm về hạ tầng, nhân lực và chính sách hỗ trợ.

---

#### Hành trình phát triển: từ Generative AI → Agentic AI

* Công nghệ AI đang chuyển từ **công cụ hỗ trợ tạo nội dung** sang **hệ thống có khả năng hành động độc lập**.
* Agentic AI cho phép nhiều agent phối hợp để hoàn thành các nhiệm vụ phức tạp.
* Mức độ tự động hóa ngày càng cao, giảm dần sự can thiệp trực tiếp của con người.

---

#### Ứng dụng Agentic AI trong doanh nghiệp

* Tăng năng suất, giảm tải công việc lặp lại, hỗ trợ đổi mới sáng tạo.
* Đến **2028**, dự báo **33% ứng dụng doanh nghiệp** sẽ tích hợp Agentic AI.
* Khoảng **15% các quyết định vận hành thường ngày** có thể được tự động hóa.

---

#### Amazon Bedrock – Nền tảng AI tổng hợp

* Cung cấp nhiều mô hình từ các nhà cung cấp hàng đầu.
* Hỗ trợ tùy chỉnh mô hình bằng dữ liệu riêng, đảm bảo bảo mật và tối ưu chi phí.
* Có sẵn cơ chế **Responsible AI**.
* Cung cấp nền tảng triển khai AI agent nhanh chóng, dễ mở rộng, dễ tích hợp.

---

#### Amazon Bedrock AgentCore

* Khung triển khai agent bảo mật, có khả năng mở rộng.
* Tương thích với các framework phổ biến: **LangChain**, **CrewAI**, **LangGraph**, **Strands Agents**.
* Hỗ trợ quản lý **memory ngắn hạn, dài hạn** và **semantic search**.
* Cho phép tích hợp, theo dõi và khám phá công cụ linh hoạt.

---

#### Hạ tầng dữ liệu và AI hiện đại

* **SageMaker Unified Studio** đóng vai trò trung tâm cho dữ liệu, phân tích, và AI.
* Tích hợp chặt chẽ với:

  * **Redshift, Athena, EMR, Glue** – xử lý và quản lý dữ liệu.
  * **QuickSight** – trực quan hóa.
  * **Bedrock** – xây dựng ứng dụng GenAI.
* Hỗ trợ mô hình **Zero-ETL** giữa **S3** và **Redshift**, giúp đơn giản hóa luồng dữ liệu.

---

#### Mô hình Data Lakehouse

* Hỗ trợ đa dạng các hệ thống lưu trữ: **S3 Tables**, **Redshift Managed Storage**.
* Kết nối dữ liệu từ nhiều nguồn lớn như **Aurora, DynamoDB, MSK, Kinesis, Salesforce, SAP, Facebook Ads**, v.v.

---

### Những Gì Tôi Học Được

#### Về tư duy AI và Cloud

* Hiểu rõ sự khác biệt giữa Generative AI và Agentic AI – hướng phát triển tất yếu của ngành.
* Nhận thức rằng Agentic AI không chỉ trả lời mà còn **hành động và ra quyết định**.
* Nắm được khả năng của Bedrock trong xây dựng hệ thống AI thông minh và tự động hóa.

#### Về kiến trúc kỹ thuật

* Hình dung được cách Bedrock kết hợp với SageMaker, Redshift và S3 trong một hệ sinh thái AI hoàn chỉnh.
* Hiểu cách AWS xử lý các phần phức tạp như memory, tool discovery và quan sát agent (observability).

---

### Ứng Dụng Thực Tế

* Ứng dụng **Amazon Titan Embeddings** để tạo embedding cho dự án hiện tại.
* Thử nghiệm mô hình **Zero-ETL** giữa Aurora/DynamoDB và Redshift.
* Tìm hiểu khả năng xây dựng **tác tử AI tự động hóa quy trình doanh nghiệp** bằng AgentCore thay vì dùng Lambda thủ công.

---

### Trải Nghiệm Tại Sự Kiện

Tham gia Cloud Day giúp tôi có góc nhìn rõ ràng hơn về cách AI, đặc biệt Agentic AI, đang thay đổi cách doanh nghiệp vận hành.

#### Giao lưu với các chuyên gia AWS

* Các diễn giả chia sẻ nhiều ví dụ thực tế về cách Amazon ứng dụng AI trong quy mô lớn.
* Hiểu sâu hơn cách hệ thống multi-agent vận hành trong môi trường doanh nghiệp.

#### **Trải nghiệm kỹ thuật**

* Tìm hiểu hoạt động của AgentCore từ quản lý memory đến tích hợp công cụ.
* Nắm được cách dữ liệu được luân chuyển giữa S3 – Redshift – SageMaker trong các ứng dụng AI.
* Thấu hiểu mô hình Lakehouse và Zero-ETL.

#### **Bài học rút ra**

* Agentic AI là bước tiến không thể tránh khỏi nếu doanh nghiệp muốn tự động hóa ở quy mô lớn.
* Hạ tầng AI hiện đại phải dựa trên cloud và dữ liệu.
* AWS đang dẫn đầu trong việc cung cấp nền tảng đầy đủ cho AI/ML.

---

### Hình Ảnh Tại Sự Kiện

![Image](/images/2-Proposal/clouday.png)
![Image](/images/2-Proposal/cloudday1.png)
![Image](/images/2-Proposal/cloudday2.png)
![alt text](/images/2-Proposal/cloudday3.jpg)


> Tổng thể, sự kiện không chỉ mang đến cho tôi kiến thức kỹ thuật mà còn giúp tôi thay đổi cách tiếp cận trong việc thiết kế ứng dụng, hiện đại hóa hệ thống và nâng cao khả năng phối hợp giữa các nhóm. Đây thực sự là một trải nghiệm giá trị, giúp tôi nhìn nhận rõ hơn cách xây dựng các giải pháp hiệu quả và linh hoạt trong môi trường doanh nghiệp.


