---
title: "Bản đề xuất"
date: 2026-06-20
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# E-Commerce Perfume Store Backend Architecture  
## Giải pháp hạ tầng AWS tối ưu cho hệ thống thương mại điện tử nước hoa  

### Tóm tắt điều hành  
Hệ thống Backend E-commerce Perfume Store (`uyentrn/web-project`) được thiết kế nhằm cung cấp một nền tảng thương mại điện tử chuyên doanh các sản phẩm nước hoa với hiệu năng cao, bảo mật và khả năng mở rộng tốt. Nền tảng tập trung tối ưu hóa tầng backend, quản lý dữ liệu sản phẩm, giỏ hàng, đơn hàng, người dùng và tích hợp các dịch vụ đám mây AWS nhằm đảm bảo tính sẵn sàng cao và vận hành ổn định.  

### Tuyên bố vấn đề  
*Vấn đề hiện tại*  
Các hệ thống thương mại điện tử đơn lẻ thường gặp khó khăn trong việc mở rộng tải, bảo mật dữ liệu giao dịch, quản lý tài nguyên tĩnh (hình ảnh sản phẩm nước hoa) và đảm bảo tính liên tục khi lượng truy cập biến động.  

*Giải pháp*  
Nền tảng sử dụng **Amazon API Gateway** làm cổng giao tiếp API, kết hợp **Amazon S3** để lưu trữ tài nguyên tĩnh, và **Amazon RDS** (Primary & Standby) cho cơ sở dữ liệu quan hệ. Kiến trúc áp dụng mô hình mạng riêng ảo (VPC) bảo mật, sử dụng **Amazon CloudFront** kết hợp **AWS WAF** để phân phối nội dung và chống tấn công, cùng với hệ thống **EC2** chạy trên **Auto Scaling Group** qua **Application Load Balancer (ALB)** để xử lý nghiệp vụ backend.  

*Lợi ích và hoàn vốn đầu tư (ROI)*  
Giải pháp tạo nền tảng backend vững chắc để phát triển tính năng thương mại điện tử, đơn giản hóa quản lý dữ liệu, cải thiện độ tin cậy và bảo mật thông tin người dùng, đồng thời tối ưu hóa chi phí vận hành hạ tầng đám mây.  

### Kiến trúc giải pháp  
Nền tảng áp dụng kiến trúc AWS Multi-AZ với vùng mạng VPC (10.0.0.0/16). Yêu cầu từ người dùng đi qua CloudFront và WAF, tiếp tục qua ALB để phân phối vào các EC2 instance nằm trong private subnet, kết nối với RDS Primary và Standby DB.  

*Dịch vụ AWS sử dụng*  
- **Amazon API Gateway**: Cổng giao tiếp và quản lý API backend.  
- **Amazon S3**: Lưu trữ tài nguyên tĩnh, hình ảnh sản phẩm và assets của hệ thống.  
- **Amazon RDS (Primary & Standby DB)**: Lưu trữ cơ sở dữ liệu quan hệ đa vùng (Multi-AZ) đảm bảo an toàn dữ liệu giao dịch nước hoa.  
- **Amazon EC2 & Auto Scaling Group**: Chạy ứng dụng backend đặt trong các private subnet, tự động co giãn theo tải.  
- **Application Load Balancer (ALB) & Regional NAT Gateway**: Điều phối traffic nội bộ và kết nối ra internet an toàn.  
- **AWS CloudFront & WAF**: Tăng tốc phân phối nội dung và bảo mật hệ thống web.  
- **Shared Services**: CloudWatch (giám sát hệ thống), Secrets Manager (quản lý thông tin mật), KMS (mã hóa dữ liệu), IAM (quản lý phân quyền).  

### Triển khai kỹ thuật  
*Tập trung phần Backend*  
- Phát triển logic nghiệp vụ cửa hàng nước hoa (quản lý danh mục sản phẩm, giỏ hàng, đơn hàng, thanh toán và xác thực người dùng).  
- Tích hợp **Amazon API Gateway** và **RDS** cho các truy vấn dữ liệu backend.  
- Sử dụng **Amazon S3** để lưu trữ hình ảnh và tài nguyên tĩnh của các dòng sản phẩm nước hoa.  
- Đảm bảo bảo mật thông tin kết nối và xác thực thông qua **Secrets Manager**, **KMS** và **IAM**.  

### Lộ trình & Mốc triển khai  
- **Giai đoạn 1 (1 tuần)**: Thiết kế kiến trúc hạ tầng AWS (RDS, S3, API Gateway, EC2, ALB, WAF).  
- **Giai đoạn 2 (2.5 tuần)**: Phát triển mã nguồn backend, xây dựng API và cấu hình kết nối cơ sở dữ liệu quan hệ.  
- **Giai đoạn 3 (1.5 tuần)**: Kiểm thử hệ thống, tích hợp CI/CD và đưa vào vận hành thực tế.  

### Ước tính ngân sách theo mức sử dụng  
Dưới đây là ước tính chi phí hạ tầng AWS hàng tháng cho hệ thống E-commerce Perfume Store dựa trên 3 mức quy mô sử dụng mới (**1.000 user/tháng**, **5.000 user/tháng**, và **10.000 user/tháng**):  

| Dịch vụ AWS | Mức Thấp<br>*(1.000 user/tháng)* | Mức Trung bình<br>*(5.000 user/tháng)* | Mức Cao<br>*(10.000 user/tháng)* |
| :--- | :---: | :---: | :---: |
| **Amazon RDS** (Primary/Standby) | $15.00 | $18.00 | $25.00 |
| **Amazon S3** (Lưu trữ & Request) | $0.50 | $1.50 | $3.00 |
| **Amazon API Gateway** | $0.20 | $1.00 | $2.50 |
| **Amazon EC2 & ASG** | $8.50 | $12.00 | $20.00 |
| **Application Load Balancer (ALB)** | $16.00 | $16.00 | $18.00 |
| **Amazon CloudFront & Data Transfer** | $0.80 | $2.00 | $4.50 |
| **AWS WAF & Khác** (CloudWatch, Secrets Mgr) | $6.00 | $6.00 | $8.00 |
| **Tổng dự đoán (USD/tháng)** | **$47.00 / tháng** | **$56.50 / tháng** | **$81.00 / tháng** |

### Đánh giá rủi ro & Bảo mật  
- **Bảo mật hạ tầng**: Sử dụng VPC, Private Subnets, WAF và IAM để kiểm soát truy cập chặt chẽ.  
- **Tính sẵn sàng**: RDS Primary/Standby Multi-AZ và Auto Scaling Group giúp giảm thiểu rủi ro gián đoạn dịch vụ khi lượng truy cập tăng cao.  

### Kết quả kỳ vọng  
*Cải tiến kỹ thuật*: Hệ thống backend thương mại điện tử nước hoa vận hành ổn định, bảo mật cao, khả năng mở rộng tốt dựa trên hạ tầng AWS hiện đại.  
*Giá trị dài hạn*: Nền tảng dữ liệu và API vững chắc phục vụ việc mở rộng tính năng kinh doanh trực tuyến trong tương lai.