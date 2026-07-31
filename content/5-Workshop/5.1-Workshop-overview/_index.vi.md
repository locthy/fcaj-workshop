---
title : "Giới thiệu"
date : 2026-07-16 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

## Tổng quan dự án

Dự án **Perfume Web** là ứng dụng web thương mại điện tử phục vụ kinh doanh nước hoa trực tuyến. Workshop này hướng dẫn xây dựng và triển khai hạ tầng đám mây cho hệ thống Perfume Web trên nền tảng **Amazon Web Services (AWS)**, đáp ứng tiêu chuẩn **tính sẵn sàng cao**, **khả năng tự động mở rộng** và **bảo mật nhiều lớp**.

---
## Kiến trúc hệ thống

![Architecture Overview](/images/5-Workshop/5.1-Workshop-overview/architecture1.png)

---

## Thành phần chính trong hệ thống

Hệ thống được tổ chức hoàn toàn trong một **Amazon VPC (`10.0.0.0/16`)** triển khai trên 2 **Availability Zones (AZ)**, kết hợp cùng các dịch vụ Edge và Managed Services của AWS:

* **Bảo mật Edge & Phân phối nội dung:**
  * **AWS WAF (Web Application Firewall):** Tường lửa ứng dụng web giúp ngăn chặn các lỗ hổng bảo mật phổ biến (SQL Injection, XSS, DDoS).
  * **Amazon CloudFront:** Mạng phân phối nội dung (CDN) giúp tăng tốc độ truyền tải dữ liệu và giảm độ trễ cho người dùng cuối.
  * **Amazon S3:** Lưu trữ các tệp tài nguyên tĩnh (hình ảnh sản phẩm nước hoa, giao diện tĩnh).

* **Tầng xử lý & Hạ tầng mạng:**
  * **Application Load Balancer (ALB):** Phân phối cân bằng lưu lượng truy cập từ người dùng đến nhóm ứng dụng backend.
  * **Auto Scaling Group (EC2):** Nhóm các máy chủ EC2 xử lý logic ứng dụng Perfume Web đặt trong các **Private Subnets** (`10.0.8.0/22` và `10.0.12.0/22`), tự động tăng/giảm số lượng instance dựa trên tải thực tế.
  * **Regional NAT Gateway:** Cho phép các máy chủ EC2 nằm trong Private Subnet truy cập ra Internet một cách an toàn để cập nhật phần mềm hoặc gọi các API bên ngoài.

* **Tầng dữ liệu:**
  * **Amazon RDS :** Cơ sở dữ liệu  tại các **Private Subnets** độc lập (`10.0.16.0/22` và `10.0.20.0/22`). 

* **Dịch vụ dùng chung & Quản trị:**
  * **AWS IAM:** Quản lý danh tính và phân quyền truy cập theo nguyên tắc quyền tối thiểu (Least Privilege).
  * **AWS KMS (Key Management Service):** Quản lý khóa mã hóa dữ liệu lưu trữ (Data-at-rest).
  * **AWS Secrets Manager (SM):** Lưu trữ và quản lý an toàn thông tin đăng nhập database và API keys.
  * **Amazon CloudWatch:** Thu thập log, giám sát hiệu năng và phát cảnh báo hệ thống.

---

## Luồng xử lý yêu cầu

Luồng xử lý dữ liệu của hệ thống Perfume Web được thực hiện tuần tự theo các bước từ **1 đến 7** trên sơ đồ kiến trúc:

1. **Gửi yêu cầu:** Người dùng (Users/Admin) gửi truy cập qua Internet. Yêu cầu đi qua **AWS WAF** để kiểm tra tính an toàn trước khi đến **Amazon CloudFront**.
2. **Xử lý tài nguyên tĩnh:** **CloudFront** điều hướng và phản hồi trực tiếp các tài nguyên tĩnh (hình ảnh, CSS, JavaScript) lấy từ **Amazon S3**.
3. **Chuyển tiếp yêu cầu động:** Các truy vấn API và logic nghiệp vụ được CloudFront đẩy qua ranh giới mạng vào **VPC**.
4. **Cân bằng tải:** Yêu cầu truy cập động được chuyển đến **Application Load Balancer (ALB)**.
5. **Xử lý ứng dụng:** **ALB** điều phối truy cập đến các máy chủ **EC2** đang hoạt động trong **Auto Scaling Group** tại các Private Subnet.
6. **Truy vấn cơ sở dữ liệu:** Các thao tác đọc/ghi dữ liệu đơn hàng và sản phẩm được EC2 gửi tới **Amazon RDS DB**.
7. **Kết nối Outbound:** Khi các máy chủ EC2 cần cập nhật phần mềm hoặc liên kết API bên ngoài, lưu lượng truy cập sẽ đi qua **Regional NAT Gateway** để ra Internet.

---

## Mục tiêu bài thực hành

Sau khi hoàn thành bài thực hành này, bạn sẽ nắm vững:
* Thiết kế và quy hoạch hạ tầng mạng **Amazon VPC Multi-AZ** tiêu chuẩn.
* Xây dựng kiến trúc bảo mật nhiều lớp với **WAF**, **Private Subnets**, **KMS** và **Secrets Manager**.
* Cấu hình cơ chế cân bằng tải và tự động mở rộng quy mô ứng dụng với **ALB** và **Auto Scaling Group**.
* Triển khai cơ sở dữ liệu **Amazon RDS Multi-AZ** có khả năng dự phòng cao.
* Tối ưu hóa hiệu năng ứng dụng thương mại điện tử bằng cách tách biệt luồng xử lý tài nguyên tĩnh (S3/CloudFront) và động (ALB/EC2).

---

## Thời lượng ước tính

Bảng dưới đây trình bày chi tiết lộ trình thực hiện từng bước và thời gian ước tính để hoàn thành bài thực hành:

| Bước | Nội dung | Thời gian ước tính |
| :--- | :--- | :--- |
| 1 | Chuẩn bị môi trường | ~30 phút |
| 2 | Thiết lập VPC | ~20 phút |
| 3 | Triển khai RDS | ~25 phút |
| 4 | Triển khai EC2 + App | ~45 phút |
| 5 | Cấu hình S3 | ~20 phút |
| 6 | Dọn dẹp | ~15 phút |
| **Tổng** | | **~3 giờ** |

---

## Chi phí ước tính

Bảng dưới đây ước tính chi phí duy trì hàng tháng cho từng dịch vụ AWS trong kiến trúc hệ thống (khi vận hành 24/7 ở quy mô nhỏ/thử nghiệm):

| Dịch vụ AWS | Cấu hình / Thông số ước tính | Chi phí ước tính / Tháng |
| :--- | :--- | :--- |
| **Amazon EC2 & Auto Scaling** | 2x `t3.micro` / `t3.small` chạy liên tục 2 AZs | ~$15.00 - $25.00 |
| **Amazon RDS Multi-AZ** | `db.t3.micro` (Primary + Standby DB) | ~$25.00 - $35.00 |
| **Application Load Balancer (ALB)** | 1 ALB + LCU cơ bản | ~$18.00 - $22.00 |
| **Regional NAT Gateway** | 1 NAT Gateway (~0.045 USD/giờ + phí truyền tải) | ~$32.00 - $38.00 |
| **AWS WAF & CloudFront** | 1 Web ACL + Quy tắc cơ bản & CDN Caching | ~$5.00 - $10.00 |
| **Amazon S3** | Lưu trữ tệp tĩnh & hình ảnh sản phẩm (< 10 GB) | ~$0.20 - $1.00 |
| **AWS Secrets Manager & KMS** | Lưu trữ bí mật database + Khóa mã hóa | ~$1.50 - $2.50 |
| **Amazon CloudWatch** | Logs, Metrics và Dashboard giám sát cơ bản | ~$2.00 - $5.00 |
| **Tổng cộng (Vận hành 24/7)** | | **~$100.00 - $140.00 / tháng** |

> **Lưu ý:** Nếu chỉ triển khai hệ thống này để **thực hành/thử nghiệm trong khoảng 2 - 3 giờ** rồi dọn dẹp (Clean up) toàn bộ tài nguyên ngay sau khi hoàn thành, tổng chi phí thực tế phát sinh khoảng **$1.50 - $3.00 USD**.