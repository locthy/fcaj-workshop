---
title : "Yêu cầu chuẩn bị"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---

## Tổng quan

Dưới đây là các **yêu cầu tiên quyết trên AWS** và **các bước chuẩn bị tại máy cục bộ** trước khi tiến hành đóng gói và triển khai dự án **Perfume Web** lên hạ tầng điện toán đám mây AWS.

---

## Yêu cầu tiên quyết trên AWS

Để đảm bảo quá trình triển khai diễn ra thuận lợi, bạn cần chuẩn bị tài khoản và các công cụ quản trị AWS như sau:

| Yêu cầu | Mô tả chi tiết | Mục đích sử dụng |
| :--- | :--- | :--- |
| **Tài khoản AWS** | Tài khoản AWS Root hoặc tài khoản IAM có toàn quyền quản trị (`AdministratorAccess`). | Quản lý và khởi tạo tài nguyên trên AWS Cloud. |
| **AWS CLI v2** | Cài đặt AWS Command Line Interface trên máy local và đã cấu hình `aws configure`. | Thao tác với các dịch vụ AWS (S3, EC2, RDS, Secrets Manager...) qua dòng lệnh. |
| **EC2 Key Pair** | Tạo sẵn một SSH Key Pair (định dạng `.pem` hoặc `.ppk`) tại Region dự định triển khai (ví dụ: `ap-southeast-1`). | Kết nối SSH an toàn vào máy chủ EC2 khi cần cấu hình hoặc kiểm tra. |
| **Quyền truy cập Dịch vụ** | Quyền hạn khởi tạo VPC, EC2, RDS, ALB, S3, CloudFront, WAF, Secrets Manager, KMS, IAM. | Tránh lỗi `AccessDenied` trong quá trình khởi tạo tài nguyên. |

---

## Các bước chuẩn bị tại máy local

Dưới đây là các bước xử lý mã nguồn tại máy cục bộ trước khi đẩy ứng dụng lên đám mây:

### Bước 1: Clone mã nguồn dự án
Mở terminal tại máy local và thực hiện clone repository mã nguồn Perfume Web về máy:

```bash
# Clone repository từ GitHub
git clone https://github.com/Thinkj07/perfume-web.git

# Di chuyển vào thư mục dự án
cd perfume-web
```

Cấu trúc mã nguồn cơ bản của dự án cần kiểm tra:
* Thư mục Frontend (React / Static Web)
* Thư mục Backend (Node.js / Express API)
* Tệp cấu hình ứng dụng (`package.json`, `.env.example`,...)

---

### Bước 2: Tách biệt biến môi trường & bảo mật thông tin
Trước khi đưa mã nguồn lên cloud, bạn **tuyệt đối không hardcode** các thông tin nhạy cảm (Database Password, Secret Key, API Key) trong mã nguồn.

1. **Kiểm tra file `.gitignore`:** Đảm bảo các file chứa thông tin nhạy cảm như `.env`, `.env.local`, file khóa SSH không bị commit lên Git.
2. **Chuẩn bị cấu hình mẫu (`.env.example`):** Định nghĩa sẵn danh sách các biến môi trường cần thiết để chuẩn bị đưa vào **AWS Secrets Manager**:
   * `DB_HOST`: Địa chỉ Endpoint của Amazon RDS Primary DB.
   * `DB_PORT`: Cổng kết nối CSDL (mặc định MySQL/PostgreSQL: `3306` hoặc `5432`).
   * `DB_NAME`: Tên cơ sở dữ liệu (`perfume_db`).
   * `DB_USER` & `DB_PASSWORD`: Lấy động từ AWS Secrets Manager.
   * `S3_BUCKET_NAME`: Tên bucket lưu trữ tài nguyên tĩnh.

---

### Bước 3: Đóng gói tài nguyên tĩnh
Ứng dụng Perfume Web có chứa các tệp tĩnh (hình ảnh sản phẩm nước hoa, banner, CSS, JS).

1. Tách riêng thư mục chứa hình ảnh sản phẩm (`/public/images` hoặc `/assets`).
2. Nén các tệp tĩnh hoặc chuẩn bị sẵn thư mục để đẩy lên **Amazon S3 Bucket** ở các bước tiếp theo bằng AWS CLI:
   ```bash
   # Lệnh tham khảo sẽ dùng ở bước triển khai S3
   aws s3 sync ./public s3://your-perfume-s3-bucket/ --acl public-read
   ```

---

### Bước 4: Đóng gói mã nguồn Backend & Script khởi tạo
Do bạn triển khai mã nguồn lên máy chủ EC2 trong Auto Scaling Group, hãy chuẩn bị kịch bản cài đặt tự động (**EC2 User Data Script**) tại máy local:

Tạo file `user-data.sh` tại máy local với nội dung mẫu:

```bash
#!/bin/bash
# Cập nhật hệ thống và cài đặt các phụ thuộc
sudo yum update -y
sudo yum install -y git nodejs

# Clone mã nguồn về máy chủ EC2
cd /home/ec2-user
git clone https://github.com/Thinkj07/perfume-web.git
cd perfume-web

# Cài đặt thư viện & khởi chạy ứng dụng
npm install
npm start
```

---

### Bước 5: Kiểm tra tính sẵn sàng

Trước khi chuyển sang bước dựng hạ tầng VPC trên AWS, hãy kiểm tra danh sách sau:

- Mã nguồn đã chạy thử thành công ở máy local.
- Không còn mã mật khẩu/bí mật hardcode trong file code.
- Đã cài đặt AWS CLI và test kết nối thành công (`aws sts get-caller-identity`).
- Đã tạo sẵn EC2 Key Pair trên AWS Management Console.
- Đã chuẩn bị sẵn file `user-data.sh` hoặc mã nguồn đóng gói.