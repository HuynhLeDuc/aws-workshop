---
title: "Worklog Tuần 9"

weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---





---

###  Mục tiêu tuần

 **Phần 1 – Tối ưu chi phí EC2 bằng Lambda Function**

* Hiểu mô hình tự động Start/Stop EC2 phục vụ mục tiêu tối ưu chi phí.
* Tạo tag để định danh các EC2 cần tự động bật/tắt.
* Viết Lambda Function tự động Start/Stop EC2 dựa trên tag.
* Tích hợp EventBridge Scheduler để chạy Lambda theo lịch.
* Kiểm tra hoạt động thực tế bằng CloudWatch Logs.
* Dọn dẹp tài nguyên sau khi thử nghiệm.

**Phần 2 – Tối ưu chi phí EC2 bằng Savings Plan**

* Hiểu Savings Plan là gì và nguyên lý giảm chi phí.
* Phân biệt Compute Saving Plans và EC2 Instance Saving Plans.
* Hiểu commit USD/hour và cách estimator tính toán.
* Biết quy trình mua Savings Plan đúng chuẩn AWS.
* Tính toán chi phí với AWS Pricing Calculator.

---

### Các công việc triển khai trong tuần

| Thứ | Công việc chi tiết                                                                                                                                                                                                                                                                              | Bắt đầu | Hoàn thành | Nguồn         |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | ---------- | ------------- |
| 2   | **Giới thiệu & phân tích mô hình tối ưu chi phí EC2**<br>• Hiểu sự lãng phí khi EC2 chạy 24/7 nhưng chỉ dùng vài giờ/ngày.<br>• Phân tích mô hình: User → EventBridge → Lambda → EC2 API.<br>• Phân loại workload phù hợp với Auto Start/Stop.<br>• Tìm hiểu hạn chế và rủi ro khi tắt/bật EC2. | 03/11   | 03/11      |[cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 3   | **Tạo Tag định danh máy chủ cần tự động hóa**<br>• Tạo Tag Key: `Schedule`.<br>• Tạo Tag Value: `office-hours`, `training-only`, `weekend-shutdown`.<br>• Áp dụng tag vào EC2 cần tự động tối ưu chi phí.<br>• Kiểm tra bằng AWS CLI: `describe-instances --filters tag:Schedule=office-hours`. | 04/11   | 04/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 4   | **Tạo IAM Role cho Lambda Function**<br>• Tạo role tên: `LambdaEC2ScheduleRole`.<br>• Gắn policy: `AmazonEC2FullAccess` (lab training).<br>• Gắn thêm quyền ghi log: `AWSLambdaBasicExecutionRole`.<br>• Kiểm tra trust relationship: `lambda.amazonaws.com`.                                   | 05/11   | 05/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 5   | **Tạo Lambda Function Start/Stop EC2**<br>• Viết code Python dùng boto3: StartInstances & StopInstances.<br>• Logic lọc EC2 theo tag `<Schedule>`.<br>• Log lại instance ID đã start/stop để kiểm tra.<br>• Test thủ công bằng “Test event”.                                                    | 06/11   | 06/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 6   | **Tạo EventBridge Scheduler để tự động hóa**<br>• Tạo rule bật EC2 lúc 8:00 AM.<br>• Tạo rule tắt EC2 lúc 18:00 PM.<br>• Gán target là Lambda Function.<br>• Kiểm tra log thực tế tại CloudWatch Logs.                                                                                          | 07/11   | 07/11      | [cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |
| 7   | **Kiểm tra kết quả & Dọn dẹp tài nguyên**<br>• Kiểm thử EC2 bật/tắt chính xác theo lịch.<br>• Xem CloudWatch Logs để debug lỗi permission.<br>• Xóa EventBridge Rules, Lambda Function, IAM Role sau khi hoàn thành.<br>• Review lại chi phí EC2 trước và sau tối ưu.                           | 08/11   | 08/11      |[cloudjourney.awsstudygroup.com](https://cloudjourney.awsstudygroup.com/) |

---

### Kết quả đạt được trong tuần 9:

 **1. Tối ưu chi phí EC2 với Lambda**

* Triển khai thành công mô hình tự động bật/tắt EC2 theo giờ làm việc.
* Hiểu và sử dụng thành thạo Tag để phân nhóm EC2 cần tối ưu.
* Viết Lambda Function tự động Start/Stop EC2 bằng boto3.
* Tự động hóa bằng EventBridge Scheduler theo lịch cố định.
* Ghi log chi tiết: instance đã start/stop, thời gian chạy, lỗi permission.
* Giảm được 50–70% chi phí EC2 cho workload chỉ chạy vài giờ mỗi ngày.

---

 **2. Tối ưu chi phí với Savings Plan**

* Hiểu rõ Savings Plan hoạt động dựa trên commit USD/hour.
* Tính toán số tiền commit phù hợp bằng AWS Pricing Calculator.
* Phân biệt hai loại Savings Plan:

  * **Compute Savings Plan** → linh hoạt nhất.
  * **EC2 Instance Savings Plan** → giảm giá sâu nhất.
* Nắm quy trình mua và áp dụng Savings Plan.
* Hiểu lợi ích khi áp dụng đúng: tiết kiệm đến 66% chi phí.

---

### Tóm tắt kiến thức đạt được

**AWS Lambda + EC2 Automation**

* Tự động hóa bật/tắt EC2 bằng Lambda.
* Sử dụng Boto3 để gọi API điều khiển EC2.
* EventBridge Scheduler dùng để tạo lịch chạy định kỳ.
* CloudWatch Logs dùng để phân tích & debug.

**AWS Savings Plans**

* Cách commit chi phí để giảm giá hạ tầng.
* Tối ưu hóa cho workload chạy 24/7.
* Phân biệt Compute vs EC2 Plans.
* Kết hợp Auto Scheduling + Savings Plan để tối ưu toàn diện.

---
