---
title: "Worklog Tuần 2"
date: 2026-07-30
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Hiểu được cách vận hành máy chủ EC2

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   |   Nghiên cứu sơ và tổng hợp những dịch vụ cần thiết và có thể áp dụng vào project | 08/06/2026   | 08/06/2026      | [Guidance for Web Store on AWS](https://docs.aws.amazon.com/solutions/web-store-on-aws/) |
| 3   | - Tìm hiểu lý thuyết Amazon EC2:<br>&nbsp;&nbsp;+ Các khái niệm cơ bản <br>&nbsp;&nbsp;+ Security Group <br>&nbsp;&nbsp;+  Pricing<br>&nbsp;&nbsp;+ Kết nối SSH | 09/06/2026 | 09/06/2026 | [ Elastic Compute Cloud (EC2) - Part 1 - Học Cloud từ A-Z (#1) ](https://www.youtube.com/watch?v=6PqZVGoeEEA&t=1994s)  /  [Giới thiệu EC2](https://000004.awsstudygroup.com/vi/1-introduce/) |
| 4   | - Tìm hiểu  AWS CLI <br> - Thiết lập môi trường CLI: <br>&emsp; +  Cài AWS CLI & cấu hình <br> &emsp; + Thực hiện các lệnh cơ bản | 10/06/2026   | 10/06/2026      |[Làm quen với AWS CLI](https://000011.awsstudygroup.com/vi/)  |
| 5   | - Thực hiện nốt task "Amazon Bedrock Playground - $20 credit" để kiếm 20$ cuối cùng <br> - Khởi chạy máy chủ EC2 với AMI Amazon Linux 2023 và tiến hành kết nối thông qua SSH bằng terminal và Mobaxterm | 11/06/2026   | 11/06/2026      |[Khởi tạo Linux instance](https://000004.awsstudygroup.com/vi/4-launchlinuxinstance/) |
| 6,7   | - Tiến hành các bài lab đơn giản với EC2: <br>&nbsp;&nbsp;+ Cài nginx, cấu hình website và truy cập website <br>&nbsp;&nbsp;+ Tạo AMI, snapshot và tạo 1 con instance mới từ đó  | 12/06/2026   | 13/06/2026      |[Amazon EC2 User Guide](https://docs.aws.amazon.com/ec2/)  |


### Kết quả đạt được tuần 2:

* Có được danh sách các dịch vụ sẽ học ở các tuần tiếp theo để áp dụng vào project.

* Hiểu rõ các thành phần của Amazon EC2, bao gồm:
  * Các loại Instance (General Purpose, Compute Optimized, Memory Optimized)
  * Quy trình tạo và sử dụng AMI
  * Cấu hình lưu trữ EBS (gp2, gp3, io1)
  * Các phương thức kết nối từ xa (SSH Key Pair, EC2 Instance Connect)

* Làm quen với việc khởi tạo EC2 và security group.

* Cài đặt và cấu hình AWS CLI trên máy tính bao gồm:
  * Access Key
  * Secret Key
  * Region mặc định

* Thực hiện được các bài lab: 
  * Thiết lập kết nối SSH từ máy cục bộ
  * Khởi tạo EC2 instance từ AMI
  * Host 1 website tĩnh đơn giản


