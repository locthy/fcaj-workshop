---
title : "Blog 1"
date : "2026-07-27"
weight : 1
chapter : false
pre : " <b> 3.1. </b> "
---

# Nên tiếp tục dùng Zonal NAT Gateway hay chuyển sang Regional NAT Gateway (RNAT)? 

Nếu hệ thống của bạn có nhiều Private Subnets ở các Availability Zone (AZ) khác nhau cần ra Internet, từ trước đến nay chúng ta thường chỉ có 2 lựa chọn — và lựa chọn nào cũng có nhược điểm:
1. Dùng 1 NAT Gateway duy nhất cho 1 AZ (Point toàn bộ route về nó):
- Dính phí Cross-AZ Data Transfer Cost. Traffic outbound càng lớn, bill cuối tháng càng lớn.
- Mất tính High Availability (HA).  Nếu AZ chứa NAT Gateway bị sập thi toàn bộ Private Subnets ở các AZ khác lập tức không kết nối ra được Internet.
 2. Mỗi AZ có 1 con NAT Gateway riêng:
-	Giải quyết được bài toán HA và Cross-AZ Data Transfer...
-	Nhưng tốn tiền duy trì cố định (Hourly rate) cho tối thiểu 2-3 con NAT cùng lúc, dù traffic ở một số AZ có thể cực kỳ ít.

 ## Bước ngoặt từ AWS: Regional NAT Gateway (RNAT). 
 Để giải quyết sự khó chịu này, AWS đã ra mắt Regional NAT Gateway (RNAT) hoạt động ở cấp độ VPC với các lợi ích:

1. Với Rnat bạn đã có thể: 
- Tạo chỉ 1 con NAT và vẫn duy trì HA tự động: Không còn nỗi lo Single Point of Failure (SPOF) vì AWS tự quản lý tính sẵn sàng đa AZ ở phía sau.
- Chỉ cần 1 Route Table duy nhất trỏ 0.0.0.0/0 về RNAT cho toàn bộ VPC, không cần phân tách Route Table phức tạp theo từng AZ.
- Bài toán AZ không còn phức tạp

2. RNAT mang danh nghĩa là một tài nguyên cấp Region, nhưng bên dưới hạ tầng vật lý nó lại được phân tán trên nhiều AZ. Nhờ kiến trúc này, AWS sẽ tự động đảm nhận 3 việc mà trước đây team DevOps phải tự làm thủ công:
- Tự động phát hiện sự cố: Nhận biết ngay lập tức nếu một hạ tầng/AZ gặp trục trặc.

- Tự động điều hướng lưu lượng: Lập tức lái traffic sang hạ tầng khỏe mạnh mà không làm gián đoạn kết nối.

- Tự động co giãn theo tải: Tự tăng/giảm năng lượng xử lý tùy thuộc vào lượng outbound traffic thực tế của hệ thống.

3. Tiết kiệm chi phí:

- Giảm số lượng NAT Gateway phải quản lý nên sẽ giảm thiểu phí duy trì theo giờ.

- Triệt tiêu phí Cross-AZ Data Processing: Không còn những khoản phí "chui" ẩn mình dưới dạng Cross-AZ Data Transfer ở cuối tháng.

- Hóa đơn minh bạch: Outbound traffic đi qua đâu, tính tiền ở đó, không còn sự chồng chéo phức tạp giữa các AZ.

![RNAT](/images/3-BlogsPosted/3.1-Blog1/1.png)

---

### Nguồn tham khảo

- [Introducing Amazon VPC Regional NAT Gateway ](https://aws.amazon.com/blogs/networking-and-content-delivery/introducing-amazon-vpc-regional-nat-gateway)
- [Regional NAT gateways for automatic multi-AZ expansion](https://docs.aws.amazon.com/vpc/latest/userguide/nat-gateways-regional.html)