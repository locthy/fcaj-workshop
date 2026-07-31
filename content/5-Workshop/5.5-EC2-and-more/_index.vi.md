---
title : "Thiết lập máy chủ backend trên EC2"
date : 2026-07-26
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

# Thiết lập máy chủ backend trên EC2

Trong phần này, chúng ta sẽ thực hiện triển khai hạ tầng tính toán cho ứng dụng Backend cửa hàng nước hoa (Perfume Store) nằm trong Private Subnet của VPC, bao gồm việc tạo IAM Role phân quyền, khởi tạo EC2 Instances, thiết lập Application Load Balancer (ALB) và tiến hành deploy ứng dụng Node.js/Express.

#### Các bước thực hiện:

1. [Tạo IAM role và EC2](5.5.1-create-EC2-Role/) - Tạo IAM Role hỗ trợ SSM Session Manager & S3 Access, sau đó khởi tạo EC2 instance trong Private Subnet.
2. [Tạo Auto Scaling Group và Application Load Balancer](5.5.2-create-ALB-ASgroup/) - Thiết lập Target Group (Port 3000) và Application Load Balancer (ALB) ở Public Subnet để điều phối lưu lượng.
3. [Cài đặt môi trường và Deploy](5.5.3-deploy/) - Kết nối vào EC2 qua SSM, cài đặt Node.js 22, Git, PM2, cấu hình biến môi trường kết nối RDS/S3, di trú cơ sở dữ liệu và khởi chạy server backend.
