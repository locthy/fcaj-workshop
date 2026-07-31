---
title: "Worklog Tuần 4"
date: 2026-07-30
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4

* Xác định dịch vụ database phù hợp.
* Hoàn thành triển khai hạ tầng mạng VPC.

### Kế hoạch tuần

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --------- | ------------ | --------------- | ------------------- |
| 2 | Tìm hiểu về RDS, DynamoDB và Aurora. | 21/06/2026 | 21/06/2026 | [Relational Database Service (RDS) - Học Cloud từ A-Z (#5)](https://www.youtube.com/watch?v=oKNBD-J4cvE&t=2422s) |
| 3 | Nghiên cứu VPC:<br>&nbsp;&nbsp;+ Subnet, Route Table, Internet/NAT Gateway<br>&nbsp;&nbsp;+ Security Group và Network ACL | 22/06/2026 | 22/06/2026 | [Virtual Private Cloud (VPC) - Học Cloud từ A-Z (#6)](https://aws.amazon.com/dms/) |
| 4 | Thực hành thiết kế VPC bằng draw.io với yêu cầu:<br>&nbsp;&nbsp;+ VPC CIDR: 10.0.0.0/16<br>&nbsp;&nbsp;+ 2 public, 2 private subnet, mỗi AZ có ít nhất 1 loại<br>&nbsp;&nbsp;+ Internet Gateway và route table trỏ đến Internet<br>&nbsp;&nbsp;+ NAT Gateway và route table trỏ đến NAT<br>&nbsp;&nbsp;+ Các Security Group | 23/06/2026 | 23/06/2026 | [Virtual Private Cloud (VPC) - Học Cloud từ A-Z (#6)](https://www.youtube.com/watch?v=jGLUTFs7-1c&t=2146s) |
| 5 | Tạo VPC đã thiết kế bằng thủ công và tự động. | 24/06/2026 | 24/06/2026 | [Amazon VPC Connectivity Options](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/introduction.html) |
| 6 | Thực hành tạo subnet cho database trong VPC và khởi tạo RDS PostgreSQL, MySQL. | 25/06/2026 | 25/06/2026 | [Amazon Route 53](https://aws.amazon.com/route53/) / [Amazon CloudFront](https://aws.amazon.com/cloudfront/) |

### Kết quả tuần 4

* Đã phân biệt được RDS và DynamoDB, chọn được dịch vụ phù hợp cho dự án.
* Làm quen với việc xây dựng các thành phần cơ bản của VPC.

