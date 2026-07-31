---
title : "Thiết lập CloudFront và S3 cho Frontend"
date : 2026-07-28
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

#### Tổng quan

Trong phần này, chúng ta sẽ thiết lập hạ tầng phân phối nội dung tĩnh (Static Web Hosting) cho ứng dụng frontend **MonaPerfume** (hoặc ứng dụng Perfume) sử dụng kết hợp giữa **Amazon S3** và **Amazon CloudFront**.

Kiến trúc này giúp tối ưu hóa hiệu năng tải trang, giảm độ trễ (latency) nhờ mạng lưới Edge Locations toàn cầu của CloudFront, đồng thời bảo mật tuyệt đối cho dữ liệu trên S3 Bucket thông qua cơ chế **Origin Access Control (OAC)**.

![Kiến trúc S3 và CloudFront](/images/5-Workshop/5.6-CloudFront-S3/architecture-overview.png)

#### Lợi ích của mô hình CloudFront + S3:

1. **Hiệu năng vượt trội**: Nội dung tĩnh (HTML, CSS, JS, hình ảnh) được cache tại các vị trí Edge của CloudFront gần với người dùng nhất.
2. **Bảo mật tối đa**: S3 Bucket không cần mở public internet (`Block Public Access` bật 100%). Người dùng chỉ có thể truy cập thông qua CDN CloudFront nhờ **OAC (Origin Access Control)**.
3. **Tiết kiệm chi phí**: Giảm thiểu lưu lượng truy cập trực tiếp vào S3 Bucket và giảm tải cho máy chủ backend EC2.
4. **Hỗ trợ HTTPS miễn phí**: Tự động mã hóa lưu lượng bằng chứng chỉ SSL/TLS từ AWS Certificate Manager (ACM) hoặc chứng chỉ mặc định của CloudFront.

---

#### Nội dung thực hiện

1. [Tạo S3 Bucket và tải source code ứng dụng Perfume](5.6.1-create-s3-bucket/)
2. [Tạo CloudFront Distribution kết nối S3 Origin](5.6.2-create-cloudfront-distribution/)
3. [Cấu hình Origin Access Control (OAC) & Bucket Policy](5.6.3-oac-bucket-policy/)
4. [Kiểm tra truy cập và vô hiệu hóa Cache (Invalidation)](5.6.4-testing-invalidation/)
