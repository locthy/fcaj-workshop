---
title : "Key Management Service"
date : 2026-07-28
weight : 1
chapter : false
pre : " <b> 5.7.1 </b> "
---
Trong phần này ta sẽ tạo KMS key và gắn vào S3 Bucket

---
### Tạo KMS key

1. **KMS Console** -> **Create a key**
![KMS](/images/5-Workshop/5.7-Security/5.7.1-KMS/kms1.png)

2. **Add labels**
| Trường                         | Giá trị                        |
| ------------------------------ | ------------------------------ |
| Alias | `MonaPerfume-KMS`           |

![KMS](/images/5-Workshop/5.7-Security/5.7.1-KMS/kms2.png)

3. **Define key administrative permissions - optional**

- Search và chọn IAM User bạn đang dùng

![KMS](/images/5-Workshop/5.7-Security/5.7.1-KMS/kms3.png)

4. **Define key usage permissions - optional**
- Search và chọn IAM User bạn đang dùng

![KMS](/images/5-Workshop/5.7-Security/5.7.1-KMS/kms4.png)

5. **Create key**
![KMS](/images/5-Workshop/5.7-Security/5.7.1-KMS/kms5.png)

### Gắn vào S3 Bucket

1. Chọn Bucket bạn muốn gắn -> **Properties**

![KMS](/images/5-Workshop/5.7-Security/5.7.1-KMS/kms6.png)

2. **Default encryption** -> Edit
![KMS](/images/5-Workshop/5.7-Security/5.7.1-KMS/kms7.png)

3. Default encryption
| Trường                         | Giá trị                        |
| ------------------------------ | ------------------------------ |
| Encryption type | Server-side encryption with AWS Key Management Service keys (SSE-KMS)           |
| AWS KMS key | Choose from your AWS KMS keys           |
| Available AWS KMS keys | `MonaPerfume-KMS`           |

![KMS](/images/5-Workshop/5.7-Security/5.7.1-KMS/kms8.png)

4. Save changes
