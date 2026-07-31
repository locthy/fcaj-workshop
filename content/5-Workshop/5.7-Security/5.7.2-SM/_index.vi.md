---
title : "Secret Manager"
date : 2026-07-28
weight : 1
chapter : false
pre : " <b> 5.7.2 </b> "
---
Ta sẽ tạo Secret để gắn vào database

---
#### Tổng quan
1. **AWS Secret Manager** -> **Store new secret** -> **Choose secret type**

- Secret type : **Credentials for Amazon RDS database**

-  Encryption key: chọn key KMS đã tạo hoặc default

| Trường                         | Giá trị                        |
| ------------------------------ | ------------------------------ |
| User name | nhập username của db           |
| Password | nhập password của db           |


-  Database: MonaPefume-DB

![SM](/images/5-Workshop/5.7-Security/5.7.2-SM/sm1.png)

2. **Configure secret**

- Secret name and description

| Trường                         | Giá trị                        |
| ------------------------------ | ------------------------------ |
| Secret name | MonaPerfume-SM           |

![SM](/images/5-Workshop/5.7-Security/5.7.2-SM/sm2.png)

3. **Review**

Gắn phần sample code vào mã nguuồn backend để lấy secret và truy cập vào RDS

![SM](/images/5-Workshop/5.7-Security/5.7.2-SM/sm3.png)

4. **Store**