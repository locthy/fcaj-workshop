---
title : "Setup CloudFront and S3 for Frontend"
date : 2026-07-28
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

#### Overview

In this section, we will establish a static content delivery infrastructure for the **MonaPerfume** frontend application using **Amazon S3** and **Amazon CloudFront**.

This architecture optimizes page loading speed and reduces latency through CloudFront's global network of Edge Locations, while ensuring absolute security for data stored in the S3 Bucket via **Origin Access Control (OAC)**.

![S3 and CloudFront Architecture](/images/5-Workshop/5.6-CloudFront-S3/architecture-overview.png)

#### Benefits of CloudFront + S3:

1. **High Performance**: Static assets (HTML, CSS, JS, images) are cached at CloudFront Edge locations closest to end-users.
2. **Enhanced Security**: The S3 Bucket remains completely private (`Block Public Access` enabled 100%). Users can only access content via CloudFront CDN using **Origin Access Control (OAC)**.
3. **Cost Efficiency**: Reduces direct read operations on the S3 bucket and minimizes backend load on EC2 instances.
4. **Free HTTPS Support**: Encrypts in-transit data automatically using SSL/TLS certificates provided by AWS Certificate Manager (ACM) or CloudFront default domain.

---

#### Contents

1. [Create S3 Bucket & Upload Perfume Frontend Code](5.6.1-create-s3-bucket/)
2. [Create CloudFront Distribution connected to S3 Origin](5.6.2-create-cloudfront-distribution/)
3. [Configure Origin Access Control (OAC) & Bucket Policy](5.6.3-oac-bucket-policy/)
4. [Verification & Cache Invalidation](5.6.4-testing-invalidation/)
