---
title: " Cài đặt môi trường và Deploy"
date: 2026-07-28
weight: 3
chapter: false
pre: "<b>5.5.3</b>"
---

## 1. Mục tiêu

Phần này hướng dẫn cài đặt môi trường phát triển và triển khai hệ thống website bán nước hoa trên nền tảng AWS. Sau khi hoàn thành, hệ thống sẽ bao gồm:

- Backend chạy trên Amazon EC2.
- Cơ sở dữ liệu PostgreSQL sử dụng Amazon RDS.
- Frontend React được triển khai thông qua Amazon S3 và Amazon CloudFront.
- Prisma ORM quản lý cơ sở dữ liệu.
- Toàn bộ ứng dụng có thể truy cập thông qua Internet và giao tiếp với cơ sở dữ liệu trong môi trường AWS.

---

## 2. Yêu cầu môi trường

Trước khi triển khai hệ thống, cần chuẩn bị các công cụ sau:

- Node.js (khuyến nghị phiên bản LTS)
- npm
- Git
- Prisma ORM
- PostgreSQL
- Docker và Docker Compose (nếu chạy cơ sở dữ liệu cục bộ)
- Tài khoản AWS

---

## 3. Cài đặt Git và clone dự án

Trên Amazon Linux EC2, cài đặt Git nếu chưa có:

```bash
yum install -y git
```

Di chuyển vào thư mục người dùng `ec2-user` và clone repository:

```bash
cd /home/ec2-user
git clone https://github.com/Thinkj07/perfume-web.git
```

Nếu muốn làm việc ngay trong thư mục dự án:

```bash
cd /home/ec2-user/perfume-web
```

---

## 4. Cài đặt Node.js

Trên Amazon Linux EC2, sử dụng **NVM (Node Version Manager)** để cài đặt Node.js.

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

export NVM_DIR="$HOME/.nvm"
source "$NVM_DIR/nvm.sh"

nvm install --lts
nvm use --lts
```

Kiểm tra phiên bản:

```bash
node -v
npm -v
```

---

## 4. Cài đặt thư viện dự án

Di chuyển vào thư mục backend:

```bash
cd backend
```

Cài đặt toàn bộ package:

```bash
npm install
```

---

## 5. Cấu hình biến môi trường

Tạo file `.env`

```bash
cp .env.example .env
```

Ví dụ:

```env
NODE_ENV=development
PORT=3000

DATABASE_URL=postgresql://postgres:password@database-1.xxxxx.ap-southeast-1.rds.amazonaws.com:5432/perfume_store?schema=public

JWT_SECRET=replace-with-secret-key
JWT_ISSUER=perfume-api
JWT_AUDIENCE=perfume-client

ACCESS_TOKEN_TTL_SECONDS=900
REFRESH_TOKEN_TTL_SECONDS=604800

BCRYPT_ROUNDS=12

AWS_REGION=ap-southeast-1
STAGE=production
```

Trong đó:

- `DATABASE_URL` là chuỗi kết nối đến Amazon RDS.
- `JWT_SECRET` dùng để ký JWT Token.
- `PORT` là cổng chạy Backend.

---

## 6. Kết nối PostgreSQL Amazon RDS

Kiểm tra kết nối PostgreSQL:

```bash
nc -vz database-1.xxxxx.ap-southeast-1.rds.amazonaws.com 5432
```

Nếu kết nối thành công sẽ hiển thị:

```text
Connected to database-1.xxxxx.ap-southeast-1.rds.amazonaws.com:5432
```

---

## 7. Khởi tạo cơ sở dữ liệu

Sau khi cấu hình `.env`, thực hiện migrate:

```bash
npx prisma migrate deploy
```

Nếu dự án có dữ liệu mẫu:

```bash
npx prisma db seed
```

Lệnh `db seed` chỉ cần thực hiện khi muốn thêm dữ liệu ban đầu vào hệ thống.

---

## 8. Chạy Backend

Khởi động server:

```bash
npm run dev
```

Kết quả:

```text
API listening on port 3000
```

Kiểm tra:

```
http://<EC2-Public-IP>:3000
```

---


## 9. Kiến trúc triển khai

Hệ thống sau khi triển khai có kiến trúc như sau:

```text
Internet
      │
      ▼
CloudFront
      │
      ▼
Amazon S3 (React Build)

Browser
      │
      ▼
Backend API (EC2)
      │
      ▼
Amazon RDS PostgreSQL
```

CloudFront chịu trách nhiệm phân phối các file tĩnh (HTML, CSS, JavaScript và hình ảnh), trong khi EC2 xử lý toàn bộ nghiệp vụ của hệ thống và giao tiếp với cơ sở dữ liệu PostgreSQL trên Amazon RDS.

---

## 10. Kiểm tra hệ thống

Sau khi triển khai hoàn tất, kiểm tra:

- Frontend truy cập thành công qua CloudFront hoặc EC2.
- Backend trả về dữ liệu thông qua API.
- Prisma kết nối được PostgreSQL.
- EC2 có thể truy cập RDS.
- Người dùng có thể đăng ký, đăng nhập và thao tác với dữ liệu.