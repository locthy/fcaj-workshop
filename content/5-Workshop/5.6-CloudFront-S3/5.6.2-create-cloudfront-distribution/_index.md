---
title : "Create CloudFront Distribution connected to S3 Origin"
date : 2026-07-29
weight : 2
chapter : false
pre : " <b> 5.6.2 </b> "
---

After storing your static frontend build on Amazon S3, the next step is creating an **Amazon CloudFront Distribution** to serve assets via AWS Content Delivery Network (CDN).

AWS has updated the CloudFront creation workflow to a step-by-step wizard. Below is the detailed guide matching the new interface.

---

### Step 1: Choose a plan

1. Open the **AWS Management Console** and navigate to **CloudFront**.
2. Click **Create distribution**.
3. On the **Choose a plan** screen, select the **Free ($0/month)** tier:

![CloudFront Free Tier Selection](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-choose-plan.png)

4. Click **Next** to proceed.

---

### Step 2: Get started

1. Review general details of the Distribution.
2. Enter a description name for the Distribution (or keep the default name suggested by AWS).

![Distribution Name Configuration](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-name.png)

3. Click **Next** to proceed to the next step.

---

### Step 3: Specify origin

1. **Origin type**: Select **Amazon S3**.
2. **S3 Origin**: Click the search box and select your S3 Bucket created in step 5.6.1:
   - Example: `monaperfume-frontend-bucket-2026.s3.us-east-1.amazonaws.com`
3. **Origin path**: Leave blank (assuming `index.html` resides at the root level of the S3 bucket).
4. **Settings**
   - Check **Allow private S3 bucket access to CloudFront (recommended)**.
   - Origin settings: Select **Use recommended origin settings**.
   - Cache settings: Select **Use recommended cache settings tailored to serving S3 content**.

![Specify Origin Domain and OAC](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-specify-origin.png)

5. Click **Next**.

---

### Step 4: Enable security

1. Review security settings (WAF / DDoS protections are integrated into the Free plan).
2. Retain default settings and click **Next**.

![Security Configuration](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-security.png)

---

### Step 5: Review and create

1. Review all configuration settings from Step 1 through Step 5.
2. Scroll to the bottom of the page and click **Create distribution**.

![Review Configuration and Create Distribution](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-review-create.png)

---

### Step 6: Add Default root object

1. Go to your created Distribution, in the **Settings** section click **Edit**.
2. Scroll down to the Default root object section, enter **index.html**.
3. Click **Save changes**.

![Add Root File](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-edit-setting.png)

---

### Step 7: Configure Custom Error Responses (Optional for SPA)

1. After creating the Distribution successfully, re-open the created Distribution and navigate to the **Error pages** tab.
2. Click **Create custom error response**:
   - **HTTP error code**: `403: Forbidden` or `404: Not Found`.
   - **Customize error response**: Select **Yes**.
   - **Response page path**: `/index.html`
   - **HTTP response code**: `200: OK`
3. Click **Create custom error response**.

![Configure Custom Error Page](/images/5-Workshop/5.6-CloudFront-S3/5.6.2-cloudfront-error-pages.png)
