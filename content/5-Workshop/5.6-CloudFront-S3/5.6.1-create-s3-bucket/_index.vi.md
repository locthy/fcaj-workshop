---
title : "Tạo S3 Bucket & Upload ứng dụng Perfume"
date : 2026-07-28
weight : 1
chapter : false
pre : " <b> 5.6.1 </b> "
---

Trong bước này, chúng ta sẽ khởi tạo một **Amazon S3 Bucket** đóng vai trò là nơi lưu trữ nguồn (Origin) chứa toàn bộ mã nguồn frontend đã được build của dự án **MonaPerfume**.

---

### Bước 1: Tạo Amazon S3 Bucket

1. Đăng nhập vào **AWS Management Console** và tìm kiếm dịch vụ **S3**.
2. Tại bảng điều khiển S3, nhấp vào nút **Create bucket**.
3. Cấu hình thông tin cơ bản cho Bucket:

| Trường / Thiết lập | Giá trị gợi ý | Ghi chú |
| :--- | :--- | :--- |
| **Bucket name** | `monaperfume-frontend-bucket-2026` | Tên Bucket phải là duy nhất trên toàn cầu (Globally Unique) |
| **AWS Region** | `us-east-1` (US East - N. Virginia) | Chọn cùng Region với các tài nguyên workshop |
| **Object Ownership** | `ACLs disabled (recommended)` | Khuyên dùng bởi AWS để đơn giản quản lý quyền |

![Tạo S3 Bucket - Thông tin cơ bản](/images/5-Workshop/5.6-CloudFront-S3/5.6.1-s3-create-1.png)

4. **Block Public Access settings for this bucket**:
   - Tích chọn **Block *all* public access**.
   - *Lý do*: Chúng ta tuân thủ chuẩn bảo mật AWS. Dữ liệu tĩnh sẽ không được mở trực tiếp ra ngoài Internet mà chỉ cho phép duy nhất CloudFront CDN truy cập thông qua OAC.

![Block All Public Access](/images/5-Workshop/5.6-CloudFront-S3/5.6.1-s3-block-public.png)

5. Các mục còn lại (**Bucket Versioning**, **Default encryption**) giữ nguyên mặc định (Default encryption: SSE-S3).
6. Cuối cùng, cuộn xuống dưới và chọn **Create bucket**.

---

### Bước 2: Tải Source Code Frontend (Perfume App) lên S3

Sau khi Bucket được tạo thành công:

1. Nhấp vào tên Bucket **`monaperfume-frontend-bucket-2026`** để truy cập chi tiết.
2. Tại tab **Objects**, chọn nút **Upload**.
3. Bạn có thể kéo thả toàn bộ thư mục `dist` hoặc các file của dự án **Perfume** (bao gồm `index.html`, thư mục `assets/`, `css/`, `js/`, hình ảnh...) vào khung upload.

![Upload Frontend Code lên S3](/images/5-Workshop/5.6-CloudFront-S3/5.6.1-s3-upload.png)

4. Hoặc sử dụng **AWS CLI** từ máy cục bộ để đồng bộ code lên S3:

```bash
# Lệnh sync thư mục build của dự án perfume lên S3 Bucket
aws s3 sync ./perfume/dist s3://monaperfume-frontend-bucket-2026/ --delete
```

5. Kiểm tra đảm bảo file `index.html` nằm ngay tại thư mục gốc (Root) của S3 Bucket.

![Danh sách Object sau khi upload](/images/5-Workshop/5.6-CloudFront-S3/5.6.1-s3-objects-list.png)
