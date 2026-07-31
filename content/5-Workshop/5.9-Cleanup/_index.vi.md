---
title: "Dọn dẹp tài nguyên"
date: 2026-07-30
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

#### Dọn dẹp tài nguyên

Trong phần này, chúng ta sẽ tiến hành dọn dẹp các tài nguyên AWS đã khởi tạo trong quá trình thực hành (**CloudFront Distribution** và **Amazon S3 Bucket**) để tránh phát sinh chi phí không cần thiết trên tài khoản AWS.

---

#### Các bước dọn dẹp

### Vô hiệu hóa (Disable) và Xóa CloudFront Distribution

1. Mở **AWS Management Console**, truy cập dịch vụ **CloudFront**.
2. Tại danh sách **Distributions**, tích chọn Distribution đã tạo cho dự án MonaPerfume.
3. Chọn nút **Disable** ở thanh công cụ phía trên.
4. Xác nhận vô hiệu hóa và chờ khoảng **1 - 3 phút** cho đến khi cột **Status** chuyển sang trạng thái `Disabled`.
5. Sau khi trạng thái đã là `Disabled`, chọn lại Distribution đó và nhấp nút **Delete**.
6. Một dòng thông báo sẽ xuất hiện thông báo phải huỷ plan để có thể xoá, chọn **Cancel plan**.
7. Chọn lại nút **Delete**, xác nhận xóa vĩnh viễn CloudFront Distribution.

![Disable và Xóa CloudFront Distribution](/images/5-Workshop/5.6-Cleanup/delete-cloudfront.png)

---

### Làm rỗng (Empty) và Xóa Amazon S3 Bucket

1. Mở **AWS Management Console**, truy cập dịch vụ **Amazon S3**.
2. Tìm và chọn S3 Bucket của bạn: **`monaperfume-frontend-bucket-2026`**.
3. Chọn nút **Empty** ở thanh công cụ.
4. Nhập từ khóa **`permanently delete`** vào ô xác nhận để xóa toàn bộ tệp tĩnh và thư mục chứa mã nguồn frontend.
5. Sau khi làm rỗng thành công, quay trở lại danh sách Bucket.
6. Chọn lại Bucket **`monaperfume-frontend-bucket-2026`** ➔ Chọn nút **Delete**.
7. Nhập chính xác tên Bucket **`monaperfume-frontend-bucket-2026`** vào ô xác nhận và bấm **Delete bucket**.

![Làm rỗng và Xóa S3 Bucket](/images/5-Workshop/5.6-Cleanup/delete-s3.png)
