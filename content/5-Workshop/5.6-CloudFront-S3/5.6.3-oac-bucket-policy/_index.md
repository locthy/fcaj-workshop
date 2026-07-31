---
title : "Configure Origin Access Control (OAC) & Bucket Policy"
date : 2026-07-28
weight : 3
chapter : false
pre : " <b> 5.6.3 </b> "
---

After creating the CloudFront Distribution, CloudFront cannot read assets from the S3 Bucket because the bucket has `Block All Public Access` turned on.

In this step, we will apply an **S3 Bucket Policy** granting read access exclusively to the CloudFront service principal via **Origin Access Control (OAC)**.

---

### Step 1: Copy Bucket Policy from CloudFront

1. On the details page of your newly created CloudFront Distribution, go to the **Origins** tab, select your S3 origin, then click the **Edit** button above.
2. Scroll down to the **Origin access control** section to see the notification:
 > *"You must allow access to CloudFront using this policy statement. Learn more about giving CloudFront permission to access the S3 bucket."*

2. Click the **Copy policy** button right next to it.

![Copy Policy from CloudFront Console](/images/5-Workshop/5.6-CloudFront-S3/5.6.3-copy-policy-banner.png)

---

### Step 2: Update S3 Bucket Policy

1. Open **Amazon S3** in a new browser tab.
2. Select your S3 Bucket: **`monaperfume-frontend-bucket-2026`**.
3. Go to the **Permissions** tab.
4. Scroll down to **Bucket policy** and click **Edit**.

![S3 Edit Bucket Policy](/images/5-Workshop/5.6-CloudFront-S3/5.6.3-s3-edit-policy.png)

5. Paste the policy JSON copied from Step 1. Standard OAC bucket policy format:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCloudFrontServicePrincipalReadOnly",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudfront.amazonaws.com"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::monaperfume-frontend-bucket-2026/*",
      "Condition": {
        "StringEquals": {
          "AWS:SourceArn": "arn:aws:cloudfront::ACCOUNT_ID:distribution/DISTRIBUTION_ID"
        }
      }
    }
  ]
}
```

{{% notice info %}}
💡 **Note:**
- Replace `monaperfume-frontend-bucket-2026` with your exact S3 Bucket name.
- Replace `ACCOUNT_ID` with your AWS Account ID.
- Replace `DISTRIBUTION_ID` with your CloudFront Distribution ID (e.g., `E1A2B3C4D5E6F7`).
{{% /notice %}}

6. Click **Save changes**.

---

### Step 3: Security Verification

Your architecture now satisfies zero-trust security standards:
- ❌ **Direct S3 URL**: Accessing direct S3 URL `https://monaperfume-frontend-bucket-2026.s3.amazonaws.com/index.html` yields **`403 Access Denied`**.
- ✅ **CloudFront CDN URL**: Accessing via CloudFront domain returns the website correctly.
