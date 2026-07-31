---
title : "Create S3 Bucket & Upload Perfume Frontend Code"
date : 2026-07-28
weight : 1
chapter : false
pre : " <b> 5.6.1 </b> "
---

In this step, we will create an **Amazon S3 Bucket** to serve as the origin store containing the compiled static frontend files of the **MonaPerfume** application.

---

### Step 1: Create Amazon S3 Bucket

1. Sign in to the **AWS Management Console** and navigate to the **S3** service.
2. On the S3 dashboard, click **Create bucket**.
3. Configure general settings:

| Setting | Suggested Value | Notes |
| :--- | :--- | :--- |
| **Bucket name** | `monaperfume-frontend-bucket-2026` | Bucket name must be globally unique |
| **AWS Region** | `us-east-1` (US East - N. Virginia) | Choose the same region as your workshop resources |
| **Object Ownership** | `ACLs disabled (recommended)` | Recommended by AWS for easier permission management |

![Create S3 Bucket - General Settings](/images/5-Workshop/5.6-CloudFront-S3/5.6.1-s3-create-1.png)

4. **Block Public Access settings for this bucket**:
   - Check **Block *all* public access**.
   - *Rationale*: We strictly adhere to AWS Security Best Practices. The S3 bucket should not be exposed to the public internet directly; access is granted exclusively through CloudFront CDN using Origin Access Control (OAC).

![Block All Public Access](/images/5-Workshop/5.6-CloudFront-S3/5.6.1-s3-block-public.png)

5. Leave default settings for **Bucket Versioning** and **Default encryption** (SSE-S3).
6. Scroll down and click **Create bucket**.

---

### Step 2: Upload Perfume Frontend Assets to S3

Once the bucket is successfully created:

1. Click on **`monaperfume-frontend-bucket-2026`** to open its details.
2. In the **Objects** tab, click **Upload**.
3. Drag and drop the contents of your compiled **Perfume** project (including `index.html`, `assets/`, `css/`, `js/`, and image files).

![Upload Frontend Code to S3](/images/5-Workshop/5.6-CloudFront-S3/5.6.1-s3-upload.png)

4. Alternatively, use the **AWS CLI** to synchronize your build files:

```bash
# Command to sync local dist files to S3 Bucket
aws s3 sync ./perfume/dist s3://monaperfume-frontend-bucket-2026/ --delete
```

5. Verify that `index.html` resides at the root level of the S3 Bucket.

![Objects list in S3 Bucket](/images/5-Workshop/5.6-CloudFront-S3/5.6.1-s3-objects-list.png)
