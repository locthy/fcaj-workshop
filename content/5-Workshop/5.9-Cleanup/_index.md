---
title : "Clean up resources"
date : 2026-07-30
weight : 9
chapter : false
pre : " <b> 5.9. </b> "
---

#### Clean up resources

In this section, we will clean up all AWS resources created during the lab (**CloudFront Distribution** and **Amazon S3 Bucket**) to avoid incurring unnecessary charges on your AWS account.

---

#### Cleanup Steps

### Disable and Delete CloudFront Distribution

1. Open the **AWS Management Console** and navigate to **CloudFront**.
2. From the **Distributions** list, select the distribution created for the MonaPerfume project.
3. Click **Disable** on the top toolbar.
4. Confirm disablement and wait **1 to 3 minutes** until the **Status** changes to `Disabled`.
5. Once the status shows `Disabled`, select the distribution again and click **Delete**.
6. A notification will appear stating that the plan must be cancelled before it can be deleted; select **Cancel plan**.
7. Choose **Delete** again, confirm permanent deletion of the CloudFront Distribution.

![Disable and Delete CloudFront Distribution](/images/5-Workshop/5.9-Cleanup/delete-cloudfront.png)

---

### Empty and Delete Amazon S3 Bucket

1. Open the **AWS Management Console** and navigate to **Amazon S3**.
2. Select your S3 Bucket: **`monaperfume-frontend-bucket-2026`**.
3. Click **Empty** on the toolbar.
4. Type **`permanently delete`** in the confirmation box to purge all static build files and folders.
5. Once emptied successfully, return to the Buckets list.
6. Select **`monaperfume-frontend-bucket-2026`** ➔ Click **Delete**.
7. Type the exact bucket name **`monaperfume-frontend-bucket-2026`** in the confirmation field and click **Delete bucket**.

![Empty and Delete S3 Bucket](/images/5-Workshop/5.9-Cleanup/delete-s3.png)