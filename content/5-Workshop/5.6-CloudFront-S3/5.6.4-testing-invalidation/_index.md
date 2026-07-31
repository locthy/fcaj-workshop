---
title : "Verification & Cache Invalidation"
date : 2026-07-28
weight : 4
chapter : false
pre : " <b> 5.6.4 </b> "
---

This final step verifies the complete setup of CloudFront and S3 for the **MonaPerfume** frontend application.

---

### Step 1: Retrieve CloudFront Distribution Domain Name

1. Open the **CloudFront Console**.
2. Select your distribution created for the MonaPerfume project.
3. Under the **Details** tab, locate **Distribution domain name**.
4. Copy the URL formatted like: **`https://d111111abcdef8.cloudfront.net`**

![CloudFront Domain Name](/images/5-Workshop/5.6-CloudFront-S3/5.6.4-cloudfront-domain.png)

---

### Step 2: Verify Website Access via Browser

1. Open a web browser (Chrome, Edge, or Firefox) and paste `https://d111111abcdef8.cloudfront.net` into the address bar.
2. Confirm that the **MonaPerfume** website renders correctly with all styling, scripts, and image assets.

![Verify Perfume Website via CloudFront CDN](/images/5-Workshop/5.6-CloudFront-S3/5.6.4-website-preview.png)

3. Press **F12** to open Developer Tools -> **Network** tab:
   - Select an asset (e.g., image or css file).
   - Inspect Response Headers for **`x-cache: Hit from cloudfront`** (or **`Miss from cloudfront`** on first load).

![Response Header x-cache from CloudFront](/images/5-Workshop/5.6-CloudFront-S3/5.6.4-network-headers.png)

---

### Step 3: Cache Invalidation Workflow for Code Updates

When redeploying updated frontend code for the Perfume application to S3, CloudFront may serve cached copies from Edge locations. To force CloudFront to fetch fresh content:

1. In the CloudFront Distribution details page, go to the **Invalidations** tab.
2. Click **Create invalidation**.

![Create CloudFront Invalidation](/images/5-Workshop/5.6-CloudFront-S3/5.6.4-create-invalidation.png)

3. In **Object paths**, enter:
   - **`/*`** *(To purge all cached files site-wide)*
   - Or specific paths like **`/index.html`**

![Configure Object Paths Invalidation](/images/5-Workshop/5.6-CloudFront-S3/5.6.4-invalidation-path.png)

4. Click **Create invalidation**.
5. Wait for the status to change from `In progress` to `Completed`. End-users will immediately receive the updated frontend build.
