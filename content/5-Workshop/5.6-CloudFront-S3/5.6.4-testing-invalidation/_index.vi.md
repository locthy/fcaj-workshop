---
title : "Kiểm tra truy cập và vô hiệu hóa Cache (Invalidation)"
date : 2026-07-28
weight : 4
chapter : false
pre : " <b> 5.6.4 </b> "
---

Đây là bước cuối cùng để nghiệm thu toàn bộ quy trình thiết lập CloudFront và S3 cho ứng dụng **MonaPerfume**.

---

### Bước 1: Lấy thông tin CloudFront Domain Name

1. Mở trang điều khiển **CloudFront Console**.
2. Nhấp vào Distribution vừa tạo cho dự án MonaPerfume.
3. Tại tab **Details**, tìm mục **Distribution domain name**.
4. Sao chép địa chỉ domain có dạng: **`https://d111111abcdef8.cloudfront.net`**

![CloudFront Domain Name](/images/5-Workshop/5.6-CloudFront-S3/5.6.4-cloudfront-domain.png)

---

### Bước 2: Kiểm tra kết quả hiển thị trên trình duyệt

1. Mở trình duyệt web (Chrome, Edge hoặc Firefox) và dán địa chỉ `https://d111111abcdef8.cloudfront.net` vào thanh địa chỉ.
2. Kiểm tra trang web **MonaPerfume** hiển thị đầy đủ giao diện, hình ảnh, các tệp CSS và JavaScript.

![Kiểm tra giao diện website Perfume qua CloudFront CDN](/images/5-Workshop/5.6-CloudFront-S3/5.6.4-website-preview.png)

3. Nhấn **F12** để mở Developer Tools -> Tab **Network**:
   - Chọn một tài nguyên (file image hoặc css).
   - Kiểm tra Response Headers: bạn sẽ thấy trường **`x-cache: Hit from cloudfront`** hoặc **`Miss from cloudfront`** (khi tải lần đầu).

![Response Header x-cache từ CloudFront](/images/5-Workshop/5.6-CloudFront-S3/5.6.4-network-headers.png)

---

### Bước 3: Hướng dẫn Vô hiệu hóa Cache (CloudFront Invalidation) khi cập nhật Code

Khi bạn thực hiện cập nhật mã nguồn ứng dụng Perfume (ví dụ: sửa đổi giao diện hoặc đăng bản build mới lên S3), CloudFront có thể vẫn giữ bản cache cũ tại các Edge Location. Để ép CloudFront cập nhật ngay lập tức:

1. Tại chi tiết CloudFront Distribution, chọn tab **Invalidations**.
2. Chọn nút **Create invalidation**.

![Create CloudFront Invalidation](/images/5-Workshop/5.6-CloudFront-S3/5.6.4-create-invalidation.png)

3. Tại ô **Object paths**, nhập:
   - **`/*`** *(Nếu muốn làm mới toàn bộ tài nguyên trên website)*
   - Hoặc tên file cụ thể: **`/index.html`**

![Cấu hình Object Paths Invalidation](/images/5-Workshop/5.6-CloudFront-S3/5.6.4-invalidation-path.png)

4. Nhấp nút **Create invalidation**.
5. Đợi trạng thái chuyển từ `In progress` sang `Completed`. Lúc này toàn bộ người dùng truy cập trang web sẽ lập tức nhận được phiên bản giao diện mới nhất.
