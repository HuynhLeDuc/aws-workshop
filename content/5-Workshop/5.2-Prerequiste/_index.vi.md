---
title : "Các bước chuẩn bị"

weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---
#### 1. Tạo IAM Role bằng Console có quyền cần thiết
Tạo một IAM role tên **bedrock** và gán các quyền cần thiết để sử dụng Amazon Bedrock: quyền gọi mô hình/agent (`bedrock:InvokeModel`, `bedrock:CreateAgent`, `bedrock:InvokeAgent`), quyền truy cập S3 (đọc/ghi) để nạp tài liệu cho Knowledge Base, và quyền CloudWatch Logs để ghi nhật ký v.v.v.

![alt text](/images/5-Workshop/5.2-Prerequisite/pre1.png)



![alt text](/images/5-Workshop/5.2-Prerequisite/pre2.png)
#### Mẫu tài liệu để nạp vào knowledge base (PDF, văn bản, markdown, HTML)


+ Chúng ta sẽ tạo 1 tài liệu giới thiệu Amazon Web Services (Text)
```bash

Amazon Web Services (AWS) là nền tảng điện toán đám mây của Amazon, chính thức ra mắt vào năm 2006. Ban đầu, AWS được tạo ra nhằm giải quyết vấn đề nội bộ của Amazon: họ cần một hạ tầng có khả năng mở rộng linh hoạt để phục vụ hệ thống thương mại điện tử khổng lồ của mình. Khi nhận ra rằng các doanh nghiệp khác cũng gặp những khó khăn tương tự về hạ tầng CNTT, Amazon quyết định thương mại hóa nền tảng này và cung cấp nó như một dịch vụ đám mây.

AWS ra đời với mục tiêu giúp tổ chức và doanh nghiệp giảm chi phí đầu tư máy chủ, triển khai ứng dụng nhanh hơn, và tận dụng hạ tầng theo nhu cầu thay vì phải tự vận hành trung tâm dữ liệu. Đây là tầm nhìn cốt lõi đằng sau mô hình “điện toán đám mây” hiện đại: đưa tài nguyên tính toán trở thành một loại dịch vụ tiện ích có thể dùng ngay, giống như điện và nước.

Trong những năm tiếp theo, AWS phát triển thần tốc, từ vài dịch vụ cơ bản như lưu trữ (Amazon S3) và máy ảo (EC2) thành hệ sinh thái hơn 200 dịch vụ bao gồm máy chủ ảo, container, trí tuệ nhân tạo, lưu trữ dữ liệu, bảo mật, IoT và phân tích dữ liệu. Nhờ khả năng mở rộng toàn cầu với hàng chục Region và hàng trăm điểm Edge trên thế giới, AWS trở thành nền tảng cloud dẫn đầu thị trường.

Mục tiêu dài hạn của AWS là mang đến một môi trường điện toán an toàn, linh hoạt và có thể đáp ứng mọi nhu cầu của người dùng — từ startup nhỏ cho đến các tập đoàn lớn. AWS hướng đến việc giúp doanh nghiệp tập trung vào phát triển sản phẩm, thay vì tốn thời gian vận hành hạ tầng. Đến nay, AWS được sử dụng bởi các công ty công nghệ hàng đầu, chính phủ, trường đại học và hàng triệu tổ chức trên toàn thế giới.

AWS không chỉ là dịch vụ hạ tầng, mà còn trở thành nền tảng quan trọng thúc đẩy đổi mới trong các lĩnh vực như học máy, Big Data, AI generative với (Amazon Bedrock), và phát triển ứng dụng serverless. Nhờ đó, AWS đóng vai trò quan trọng trong việc hình thành thế hệ công nghệ hiện đại.
```


