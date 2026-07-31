---
title : "Cấu hình Origin Access Control (OAC) & Bucket Policy"
date : 2026-07-28
weight : 3
chapter : false
pre : " <b> 5.6.3 </b> "
---

Sau khi tạo xong CloudFront Distribution, CloudFront vẫn chưa thể lấy dữ liệu từ S3 Bucket vì S3 Bucket đang bật chế độ khóa hoàn toàn Public Access (`Block All Public Access`).

Trong bước này, chúng ta sẽ áp dụng **S3 Bucket Policy** cho phép duy nhất dịch vụ CloudFront (với ARN cụ thể) được quyền truy cập các Object trong S3 Bucket qua chuẩn **OAC (Origin Access Control)**.

---

### Bước 1: Sao chép Bucket Policy từ CloudFront

1. Tại trang chi tiết của CloudFront Distribution vừa tạo, vào tab **Origins**, chọn vào S3 của bạn, sau đó bấm nút Edit phía trên
2. Kéo xuống mục **Origin access control** sẽ thấy thông báo: 
 > *"You must allow access to CloudFront using this policy statement. Learn more about giving CloudFront permission to access the S3 bucket."*

2. Chọn nút **Copy policy** ngay bên cạnh.

![Copy Policy từ CloudFront Console](/images/5-Workshop/5.6-CloudFront-S3/5.6.3-copy-policy-banner.png)

---

### Bước 2: Cập nhật Policy trong S3 Bucket

1. Mở một tab mới, truy cập vào dịch vụ **Amazon S3**.
2. Chọn S3 Bucket của dự án: **`monaperfume-frontend-bucket-2026`**.
3. Chuyển sang tab **Permissions**.
4. Cuộn xuống mục **Bucket policy**, chọn nút **Edit**.

![S3 Edit Bucket Policy](/images/5-Workshop/5.6-CloudFront-S3/5.6.3-s3-edit-policy.png)

5. Dán đoạn JSON Policy đã copy ở Bước 1 vào ô chỉnh sửa. Cấu trúc chuẩn của S3 Bucket Policy với OAC như sau:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCloudFrontServicePrincipalReadOnly",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudfront.amazonaws.com"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::monaperfume-frontend-bucket-2026/*",
      "Condition": {
        "StringEquals": {
          "AWS:SourceArn": "arn:aws:cloudfront::ACCOUNT_ID:distribution/DISTRIBUTION_ID"
        }
      }
    }
  ]
}
```

{{% notice info %}}
💡 **Lưu ý:**
- Thay thế `monaperfume-frontend-bucket-2026` bằng đúng tên S3 Bucket của bạn.
- Thay thế `ACCOUNT_ID` bằng ID tài khoản AWS của bạn.
- Thay thế `DISTRIBUTION_ID` bằng ID của CloudFront Distribution vừa tạo (ví dụ: `E1A2B3C4D5E6F7`).
{{% /notice %}}

6. Chọn **Save changes** để lưu chính sách.

---

### Bước 3: Kiểm tra tính bảo mật

Lúc này kiến trúc bảo mật đạt chuẩn hoàn chỉnh:
- ❌ **Truy cập S3 trực tiếp**: Nếu bạn thử lấy liên kết S3 URL dạng `https://monaperfume-frontend-bucket-2026.s3.amazonaws.com/index.html` và dán vào trình duyệt, hệ thống sẽ trả về lỗi **`403 Access Denied`**.
- ✅ **Truy cập qua CloudFront**: Người dùng truy cập qua tên miền CloudFront CDN sẽ xem được nội dung trang web bình thường.
