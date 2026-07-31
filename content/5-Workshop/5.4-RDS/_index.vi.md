---
title : "Thiết database trên RDS"
date : 2026-07-28
weight : 4
chapter : false
pre : " <b> 5.4 </b> "
---

## Hướng dẫn tạo RDS PostgreSQL

### 1. Vào trang chính RDS, chọn Databases và Create database

Truy cập AWS Console, mở dịch vụ **Amazon RDS** và vào phần **Databases**.

Trên trang chính của RDS, chọn **Create database** để bắt đầu cấu hình.

![RDS Create Database](/images/5-Workshop/5.4-RDS/rds-1.png)

Ở bước này, nếu muốn cấu hình đầy đủ, chọn chế độ **Create database** với **full configuration** để vào giao diện tùy chỉnh toàn bộ thông số.

### 2. Chọn PostgreSQL engine và Easy create

Ở phần chọn engine, hãy chọn **PostgreSQL**.

Nếu AWS hiển thị tùy chọn **Easy create**, bạn có thể bật để sử dụng cấu hình nhanh. Với Easy create, RDS sẽ đề xuất cấu hình mặc định, nhưng vẫn đảm bảo engine là PostgreSQL.

![Chọn PostgreSQL và Easy create](/images/5-Workshop/5.4-RDS/rds-2.png)

### 3. Nhập tên database và chọn self-managed password + master username

Tiếp theo, nhập tên database mong muốn vào trường **DB instance identifier** hoặc **Database name**.

Chọn phương thức quản lý mật khẩu là **Self-manage password**.

Nhập:

- **Master username**: tên người dùng quản trị (ví dụ: `admin`)
- **Password** và **Confirm password**: mật khẩu do bạn tự chọn

![Nhập tên database và self-manage password](/images/5-Workshop/5.4-RDS/rds-3.png)

### 4. Chọn kết nối với EC2 có sẵn và bấm Create database

Ở bước cấu hình kết nối, chọn kết nối đến **EC2 instance** đã có sẵn trong cùng VPC hoặc subnet phù hợp.

Đảm bảo security group và network settings cho phép EC2 truy cập tới RDS.

Cuối cùng, kiểm tra lại thông tin và bấm **Create database** để khởi tạo RDS PostgreSQL.

![Kết nối EC2 và Create database](/images/5-Workshop/5.4-RDS/rds-4.png)

Sau khi hoàn thành, RDS sẽ bắt đầu tạo instance PostgreSQL. Bạn có thể dùng endpoint được cung cấp để kết nối từ EC2.

