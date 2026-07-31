---
title : "Creat IAM role and EC2 "
date : 2026-07-26 
weight : 1 
chapter : false
pre : " <b> 5.5.1 </b> "
---

---

We need to create an IAM role that allows us to access EC2 instances residing in a private subnet via AWS Systems Manager Session Manager (SSM), as well as enable EC2 instances to interact with the S3 service.

### Tạo role

1. Login by root account or  IAM user Administrator privileges.
2. IAM console -> Roles
3. Create role

Configure the details as follows:

- **Select trusted entity** 
| Field       | Value| 
| ---------- | -------- | 
| Trusted entity type      | AWS service      | 
| Use case      | EC2      | 

- **Add permissions**

Search and choose `AmazonS3FullAccess`and `AmazonSSMManagedInstanceCore`

- **Name, review, and create**
| Field       | Value| 
| ---------- | -------- | 
| Role name      |  MonaPerfume-EC2-S3-SSM      | 
| Description      | Allow MonaPerfume's EC3 interact with S3 and can be accessed through SSM      | 

4. Chọn **Create role**


### Create first EC2

1.  EC2 console -> Instances -> **Launch instances**

2. **Name and tags**:
   - Name: `MonaPerfume-EC2-PRIVATE-01`

3. **Application and OS Images (AMI)**:
   - **Amazon Linux 2023 kernel-6.18 AMI**
   - Architecture: **64-bit (x86)**

![Chọn AMAZON LINUX AMI](/images/5-Workshop/5.5-EC2-and-more/5.5.1-create-EC2-Role/ec2-1.png)

4. **Instance type**:
   - Chọn **t3.micro** (Free Tier eligible)
   - 2 vCPU, 1 GiB RAM

5. **Key pair**: Select an existing key pair, or select **Create new key pair** to generate a new one.

6. **Network settings** → **Edit**:

| Field                    | Value                        |
| ------------------------- | ------------------------------ |
| **VPC**                   | MonaPerfume-VPC               |
| **Subnet**                | MonaPerfume-VPC-subnet-private1-us-east-1a     |
| **Auto-assign public IP** | Disable                         |
| **Firewall**              | Select existing security group |
| **Security group**        | MonaPerfume-EC2-SG            |

7. **Configure storage**:
   - **Root volume**: 8 GiB, gp3

![Setting network](/images/5-Workshop/5.5-EC2-and-more/5.5.1-create-EC2-Role/ec2-2.png)

8. **Advanced details**
    - **IAM instance profile**: MonaPerfume-EC2-S3-SSM

9.  **Launch instance**

![Setting network](/images/5-Workshop/5.5-EC2-and-more/5.5.1-create-EC2-Role/ec2-3.png)

**Launch success**
![Setting network](/images/5-Workshop/5.5-EC2-and-more/5.5.1-create-EC2-Role/ec2-4.png)


### Create the Second EC2 Instance (via AMI or Manually)
- You can create the second EC2 instance using an AMI created from the first instance after completing the steps in [Environment Setup & Deployment](/FCAJ-Workshop/vi/5-workshop/5.5-ec2-and-more/5.5.3-deploy/) or by following the same manual steps above with the following modified parameters:


| Field                    | Value                        |
| ------------------------- | ------------------------------ |
| **Name**                   | `MonaPerfume-EC2-PRIVATE-02`               |
| **Subnet**                | MonaPerfume-VPC-subnet-private2-us-east-1b     |

- If creating via AMI::

1. Select the instance you want to create an AMI from -> **Actions** -> **Images and templates** -> **Create Images**

![Setting ami](/images/5-Workshop/5.5-EC2-and-more/5.5.1-create-EC2-Role/ami1.png)

2. - **Image name**: `MonaPerfume-EC2-AMI`
   - Uncheck **Reboot instance**

![Setting ami](/images/5-Workshop/5.5-EC2-and-more/5.5.1-create-EC2-Role/ami2.png)

3. **Create image**