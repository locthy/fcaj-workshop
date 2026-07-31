---
title : "Các bài blogs đã đăng"
date : "2026-07-27"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

# Các bài blogs đã đăng

Dưới đây là các bài blog em đã đăng trên [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj) trong suốt quá trình thực tập tại Amazon Web Services Việt Nam.

### [Nên tiếp tục dùng Zonal NAT Gateway hay chuyển sang Regional NAT Gateway (RNAT)?](3.1-blog1/)

Blog này giới thiệu chế độ hoạt động mới của AWS NAT Gateway – Regional NAT Gateway (RNAT), cho phép một NAT Gateway duy nhất tự động mở rộng và thu hẹp phạm vi hoạt động qua nhiều Availability Zone trong cùng một VPC. Đây là bước tiến giúp đơn giản hóa đáng kể việc quản lý hạ tầng mạng so với mô hình NAT Gateway theo từng AZ trước đây.

### [Blog 2 - LỢI ÍCH CỦA REGIONAL NAT GATEWAY: BẢO MẬT, MỞ RỘNG VÀ TÍCH HỢP IPAM](3.2-blog2/)

Blog này phân tích sâu hơn các lợi ích của Regional NAT Gateway về mặt bảo mật, khả năng tự động mở rộng chống cạn kiệt cổng, và khả năng tích hợp với VPC IPAM để quản lý địa chỉ IP một cách có kiểm soát. Bài viết cũng đề cập đến khả năng giám sát qua CloudWatch và tích hợp với các giải pháp kiểm tra lưu lượng như AWS Network Firewall.

### [Blog 3 - AMAZON EVENTBRIDGE LÀ GÌ? XÂY DỰNG ỨNG DỤNG HƯỚNG SỰ KIỆN TRÊN AWS](3.3-blog3/)

Blog này giới thiệu Amazon EventBridge – dịch vụ serverless giúp xây dựng kiến trúc hướng sự kiện (event-driven architecture) trên AWS. Bài viết phân tích hai cơ chế chính là Event bus và Pipes, cách chúng phối hợp với nhau, cùng vai trò của EventBridge Scheduler trong việc lập lịch tác vụ tự động.