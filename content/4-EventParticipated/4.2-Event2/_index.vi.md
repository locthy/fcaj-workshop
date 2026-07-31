---
title: "Event 2"
date: 2026-07-11
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Bài thu hoạch Learning AWS Architecture”

### Mục Đích Của Sự Kiện

- Tìm ra đội thắng trận chung kết cuộc thi Cloud Architect
- Giới thiệu các mô hình kiến trúc đám mây

### Ngày diễn ra sự kiện

Ngày hôm đó là trận chung kết của cuộc thi kiến trúc AWS. Không khí buổi thi vừa trang trọng vừa hào hứng, với các đội thi, ban giám khảo và khán giả đều tập trung để lắng nghe từng phần trình bày và câu trả lời. Chương trình được tổ chức theo nhiều vòng, từ mở đầu bằng các câu hỏi cơ bản đến những thử thách phức tạp hơn, nhằm đánh giá toàn diện kiến thức và tư duy kiến trúc của từng thí sinh.

### Các vòng câu hỏi

- Dễ: Các câu hỏi khởi động nhằm kiểm tra nền tảng, như VPC là gì, public subnet khác private subnet ra sao, và vai trò của Internet Gateway. Mục tiêu là đảm bảo mọi người đều nắm chắc các khái niệm cơ bản.
- Trung bình: Những câu hỏi này đi sâu vào lựa chọn dịch vụ và thiết kế hệ thống, ví dụ nên dùng EC2 hay Lambda cho từng loại workload, cách cấu hình Auto Scaling để xử lý lưu lượng biến đổi, và so sánh ưu nhược điểm giữa S3, EBS và instance store.
- Khó: Vòng thách thức với các bài toán kiến trúc thực tiễn, chẳng hạn thiết kế hệ thống phân tán đa AZ để đảm bảo High Availability, xây dựng cấu hình IAM an toàn theo nguyên tắc least privilege, và tối ưu chi phí với Regional NAT Gateway trong khuôn khổ AWS Well-Architected Framework.
- Nâng cao: Vòng cuối cùng đặt ra các thử thách kiến trúc phức tạp hơn, như đề xuất cách xây dựng microservices theo event-driven pattern, tích hợp AI để cải thiện hành vi hệ thống, và xây dựng kế hoạch khôi phục khi một Availability Zone bị lỗi.

### Trải nghiệm chung kết

Trận chung kết không chỉ yêu cầu trả lời đúng mà còn cần trình bày rõ ràng, logic và thuyết phục. Những câu trả lời xuất sắc là những câu trả lời vừa chính xác về mặt kỹ thuật, vừa giải thích được vì sao chọn giải pháp đó trong bối cảnh yêu cầu cụ thể. Khi lắng nghe các đội khác trình bày, tôi học được nhiều cách tiếp cận mới và nhận ra rằng giải pháp tốt nhất thường là giải pháp đơn giản nhưng đầy đủ.

Không khí buổi thi có nhiều giây phút căng thẳng khi thí sinh phân tích yêu cầu và đề xuất kiến trúc dưới áp lực thời gian. Ban giám khảo đặc biệt chú trọng đến các yếu tố bảo mật, khả năng mở rộng, chi phí và tính dễ vận hành khi đánh giá các phương án.

### Bài học rút ra từ chung kết

- Nền tảng kiến thức rất quan trọng: nắm chắc VPC, subnet và IAM giúp giải quyết được các bài toán phức tạp hơn.
- Kiến trúc tốt nên cân bằng giữa độ phức tạp và tính hiệu quả; không nên làm quá tay nếu mục tiêu chỉ cần giải pháp đơn giản và dễ quản lý.
- Event-driven architecture và serverless đem lại nhiều lợi ích, nhưng cần áp dụng đúng bối cảnh và yêu cầu nghiệp vụ.
- Chuẩn bị cho sự cố là điều thiết yếu; thiết kế để phục hồi khi AZ gặp lỗi là tiêu chí của hệ thống được kiến trúc tốt.

### Kết quả và hình ảnh

![Đội chiến thắng nhận giải thưởng](/images/4-Events/4.2-Event2/workshop-2.1.jpg)
*Hình ảnh đội chiến thắng nhận giải thưởng trong trận chung kết.*

![Diễn giả trình bày mô hình kiến trúc đám mây](/images/4-Events/4.2-Event2/workshop-2.2.jpg)
*Hình ảnh các anh diễn giả đang trình bày về mô hình kiến trúc đám mây AWS.*

Trận chung kết đã giúp tôi củng cố kiến thức về kiến trúc AWS, rèn luyện khả năng tư duy theo trình tự từ dễ đến khó, và học cách trình bày phương án thiết kế một cách rõ ràng, thuyết phục hơn. Tôi cũng nhận thấy sự khác biệt giữa kiến thức lý thuyết và khả năng ứng dụng dưới áp lực thực tế.