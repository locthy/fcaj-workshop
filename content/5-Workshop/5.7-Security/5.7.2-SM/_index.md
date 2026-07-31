---
title : "Secret Manager"
date : 2026-07-28
weight : 1
chapter : false
pre : " <b> 5.7.2 </b> "
---

---
1. **AWS Secret Manager** -> **Store new secret** -> **Choose secret type**

- Secret type : **Credentials for Amazon RDS database**

-  Encryption key: use your KMS key or default

| Field                         | Value                        |
| ------------------------------ | ------------------------------ |
| User name | type your db's username           |
| Password | type your db's password           |


-  Database: MonaPefume-DB

![SM](/images/5-Workshop/5.7-Security/5.7.2-SM/sm1.png)

2. **Configure secret**

- Secret name and description

| Field                         | Value                        |
| ------------------------------ | ------------------------------ |
| Secret name | MonaPerfume-SM           |

![SM](/images/5-Workshop/5.7-Security/5.7.2-SM/sm2.png)

3. **Review**

Attach sample code into your backend to get secret and access to RDS

![SM](/images/5-Workshop/5.7-Security/5.7.2-SM/sm3.png)

4. **Store**