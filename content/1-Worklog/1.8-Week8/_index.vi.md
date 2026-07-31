---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Quản lý thông tin cấu hình nhạy cảm (API Keys, DB Credentials) an toàn bằng AWS Systems Manager Parameter Store.
* Nắm tư duy và luồng hoạt động của tích hợp/triển khai tự động (CI/CD).
* Tự động hóa quá trình Deploy code/máy chủ khi có thay đổi trên Repository (GitHub Actions / AWS CodePipeline).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ----------| ------------ | --------------- | -------------- |
| 2,3   | - Nghiên cứu cơ chế hoạt động của tường lửa ứng dụng web và thực hiện các bài lab kèm theo | 20/07/2026   | 21/07/2026  |[AWS Web Application Firewall](https://000026.awsstudygroup.com/vi/)|
| 4, 5 | - Tìm hiểu cú pháp viết file cấu hình hạ tầng bằng định dạng YAML/JSON trong AWS CloudFormation. <br> - Viết mã nguồn mẫu để định nghĩa các tài nguyên cơ bản bao gồm VPC, Subnet và Internet Gateway.  | 22/07/2026 | 23/07/2026 | |
| 6 | - Tìm hiểu và áp dụng dịch vụ lưu trữ thông tin bảo mật AWS Secrets Manager.  | 24/07/2026 | 24/07/2026      | [Sử dụng AWS Secrets Manager với Amazon RDS và AWS Fargate](https://000096.awsstudygroup.com/vi/)|


### Kết quả đạt được tuần 8:

* Biết cách thiết lập các luật chặn lọc mã độc và truy cập trái phép bằng AWS WAF để bảo vệ an toàn cho các đầu cuối Web API.
* Biết cách quản lý hạ tầng bằng mã nguồn, biết cách viết file YAML CloudFormation để khởi tạo nhanh một cụm tài nguyên mạng mà không cần làm thủ công trên giao diện web.
* Nắm vững phương pháp bảo mật thông tin cấu hình ứng dụng bằng AWS Secrets Manager, loại bỏ hoàn toàn việc hardcode các thông tin đăng nhập trong mã nguồn.