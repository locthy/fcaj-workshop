---
title: "Worklog Tuần 4"
date: 2026-07-30
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Biết nên dùng dịch vụ nào cho database
* Triển khai được hạ tầng mạng VPC

### Các công việc cần triển khai trong tuần này:

| Thứ | Nhiệm vụ | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --------- | ------------ | --------------- | ------------------- |
| 2   | - Tìm hiểu về RDS, DynamoDB, Aurora  | 21/06/2026 | 21/06/2026 | [Relational Database Service (RDS) - Học Cloud từ A-Z (#5)](https://www.youtube.com/watch?v=oKNBD-J4cvE&t=2422s) |
| 3   | - Nghiên cứu VPC:<br>&nbsp;&nbsp;+ Subnet, Route Table, Internet/NAT Gateway<br>&nbsp;&nbsp;+ Security Group và Network ACL | 22/06/2026 | 22/06/2026 | [Virtual Private Cloud (VPC) - Học Cloud từ A-Z (#6)](https://aws.amazon.com/dms/) |
| 4   | - Thực hành thiết kế VPC bằng draw.io với các yêu cầu: <br>&nbsp;&nbsp;+ VPC CIDR: 10.0.0.0/16 <br>&nbsp;&nbsp;+ 2 public, 2 private subnet. Mỗi AZ chứa ít nhất 1 loại <br>&nbsp;&nbsp;+ Internet Gateway và cấu hình Route table chỉa tới nó <br>&nbsp;&nbsp;+ NAT Gateway và cấu hình route table tới NAT <br>&nbsp;&nbsp;+ Các Security group  | 23/06/2026 | 23/06/2026 | [Virtual Private Cloud (VPC) - Học Cloud từ A-Z (#6)](https://www.youtube.com/watch?v=jGLUTFs7-1c&t=2146s) |
| 5   | - Tiến hành tạo VPC đã thiết kế bằng thủ công và tự động (VPC and more)   | 24/06/2026 | 24/06/2026 | [Amazon VPC Connectivity Options](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/introduction.html) |
| 6   | - Thực hành tạo db subnet nằm trong VPC đã tạo <br> - Khởi tạo RDS Postpre, Mysql | 25/06/2026 | 25/06/2026 | [Amazon Route 53](https://aws.amazon.com/route53/) / [Amazon CloudFront](https://aws.amazon.com/cloudfront/) |

### Thành tích tuần 4:

* Phân biệt được RDS và DynamoDB và biết được nên áp dụng cái nào vào project
* Làm quen được với các thao tác tạo các thành phần cần thiết trong VPC
