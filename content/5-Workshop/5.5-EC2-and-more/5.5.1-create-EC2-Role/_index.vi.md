---
title : "Tạo IAM role và EC2 "
date : 2026-07-26 
weight : 1 
chapter : false
pre : " <b> 5.5.1 </b> "
---

---

Ta cần tạo **IAM role** cho phép ta truy cập EC2 nằm trong private subnet thông qua **Session Manager(SSM)** cũng như để EC2 có thể tương tác với dịch vụ **S3**
### Tạo role

1. Đăng nhập bằng tài khoản root hoặc IAM user có quyền Admin
2. Vào IAM console và chọn Roles
3. Create role

Chọn thông tin

3.1 **Select trusted entity** 
| Trường       | Giá trị| 
| ---------- | -------- | 
| Trusted entity type      | AWS service      | 
| Use case      | EC2      | 

3.2 **Add permissions**

Search `AmazonS3FullAccess`(ở phần này ta sẽ chọn full access cho dễ thao tác, sau khi deploy thành công ta sẽ đổi lại) và `AmazonSSMManagedInstanceCore` và tick chọn bên trái

3.3 **Name, review, and create**
| Trường       | Giá trị| 
| ---------- | -------- | 
| Role name      |  MonaPerfume-EC2-S3-SSM      | 
| Description      | Allow MonaPerfume's EC3 interact with S3 and can be accessed through SSM      | 

4. Chọn **Create role**


### Tạo EC2 đầu tiên

1. Vào EC2 console, chọn mục Instances bên phải và click **Launch instances**

2. **Name and tags**:
   - Name: `MonaPerfume-EC2-PRIVATE-01`

3. **Application and OS Images (AMI)**:
   - Chọn **Amazon Linux 2023 kernel-6.18 AMI**
   - Architecture: **64-bit (x86)**

![Chọn AMAZON LINUX AMI](/images/5-Workshop/5.5-EC2-and-more/5.5.1-create-EC2-Role/ec2-1.png)

4. **Instance type**:
   - Chọn **t3.micro** (Free Tier eligible)
   - 2 vCPU, 1 GiB RAM

5. **Key pair**: Chọn key pair sẵn có, nếu không có thì chọn **Create new key pair** để tạo mới

6. **Network settings** → **Edit**:

| Trường                    | Giá trị                        |
| ------------------------- | ------------------------------ |
| **VPC**                   | MonaPerfume-VPC               |
| **Subnet**                | MonaPerfume-VPC-subnet-private1-us-east-1a     |
| **Auto-assign public IP** | Disable                         |
| **Firewall**              | Select existing security group |
| **Security group**        | MonaPerfume-EC2-SG            |

7. **Configure storage**:
   - **Root volume**: 8 GiB, gp3

![Setting network](/images/5-Workshop/5.5-EC2-and-more/5.5.1-create-EC2-Role/ec2-2.png)

8. **Advanced details**
    - **IAM instance profile**: MonaPerfume-EC2-S3-SSM

9. Nhấn **Launch instance**

![Setting network](/images/5-Workshop/5.5-EC2-and-more/5.5.1-create-EC2-Role/ec2-3.png)

**Launch thành công**
![Setting network](/images/5-Workshop/5.5-EC2-and-more/5.5.1-create-EC2-Role/ec2-4.png)


### Tạo EC2 còn lại
- Ta có thể tạo con EC2 này bằng AMI của con EC2 đầu tiên sau khi hoàn thành các bước ở [Cài đặt môi trường và Deploy](/FCAJ-Workshop/vi/5-workshop/5.5-ec2-and-more/5.5.3-deploy/) hoặc làm tương tự các bước trên
- Lặp lại các bước từ 1- 9 nhưng thay các thông tin sau: 

1.  **Name**: `MonaPerfume-EC2-PRIVATE-02`
2. **Subnet**: MonaPerfume-VPC-subnet-private2-us-east-1b