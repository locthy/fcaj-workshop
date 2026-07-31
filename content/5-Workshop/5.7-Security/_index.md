---
title : "Configuring AWS KMS and Secrets Manager"
date : 2026-07-28
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

#### Overall

In this section, we will configure two core AWS security services: Key Management Service (KMS) and AWS Secrets Manager.

AWS KMS: Used to manage customer-managed encryption keys for encrypting objects uploaded to Amazon S3 buckets and securing Amazon RDS database instances at rest.

AWS Secrets Manager: Eliminates the need to hardcode database credentials directly into application source code or environment variables by securely storing and rotating RDS connection credentials on AWS.

---

1. [Key Management Service](5.7-Security/5.7.1-KMS)
1. [Secret Manager](5.7-Security/5.7.2-SM)