---
title : "Create IAM role and EC2"
date : 2026-07-26
weight : 1
chapter : false
pre : " <b> 5.5.1 </b> "
---

We need to create an IAM role that allows us to access the EC2 instance in the private subnet through Session Manager (SSM), and also enables the EC2 instance to interact with the S3 service.

### Create the role

1. Sign in with the root account or an IAM user that has Admin privileges.
2. Open the IAM console and select Roles.
3. Choose Create role.

### Select the trusted entity

| Field | Value |
| --- | --- |
| Trusted entity type | AWS service |
| Use case | EC2 |

### Add permissions

Search for AmazonS3FullAccess (for this exercise, we will use full access for simplicity; after deployment succeeds, we will change it) and AmazonSSMManagedInstanceCore, then select the checkbox on the left.

### Name, review, and create

| Field | Value |
| --- | --- |
| Role name | MonaPerfume-EC2-S3-SSM |
| Description | Allow MonaPerfume's EC2 instance to interact with S3 and be accessible through SSM |

4. Select Create role.

### Create the first EC2 instance

1. Open the EC2 console, select Instances on the right, and click Launch instances.

2. Name and tags:
   - Name: MonaPerfume-EC2-PRIVATE-01

3. Application and OS Images (AMI):
   - Choose Amazon Linux 2023 kernel-6.18 AMI.
   - Architecture: 64-bit (x86)

![Select AMAZON LINUX AMI](/images/5-Workshop/5.5-EC2-and-more/5.5.1-create-EC2-Role/ec2-1.png)

4. Instance type:
   - Choose t3.micro (Free Tier eligible)
   - 2 vCPU, 1 GiB RAM

5. Key pair: Choose an existing key pair; if none is available, select Create new key pair to create one.

6. Network settings → Edit:

| Field | Value |
| --- | --- |
| VPC | MonaPerfume-VPC |
| Subnet | MonaPerfume-VPC-subnet-private1-us-east-1a |
| Auto-assign public IP | Disable |
| Firewall | Select existing security group |
| Security group | MonaPerfume-EC2-SG |

7. Configure storage:
   - Root volume: 8 GiB, gp3

![Setting network](/images/5-Workshop/5.5-EC2-and-more/5.5.1-create-EC2-Role/ec2-2.png)

8. Advanced details:
   - IAM instance profile: MonaPerfume-EC2-S3-SSM

9. Click Launch instance.

![Setting network](/images/5-Workshop/5.5-EC2-and-more/5.5.1-create-EC2-Role/ec2-3.png)

Launch successful.

![Setting network](/images/5-Workshop/5.5-EC2-and-more/5.5.1-create-EC2-Role/ec2-4.png)

### Create the remaining EC2 instance

- You can create this EC2 instance using the AMI of the first EC2 instance after completing the steps in [Set up the environment and deploy](/FCAJ-Workshop/vi/5-workshop/5.5-ec2-and-more/5.5.3-deploy/) or by following the same steps above.
- Repeat steps 1 to 9, but change the following values:

1. Name: MonaPerfume-EC2-PRIVATE-02
2. Subnet: MonaPerfume-VPC-subnet-private2-us-east-1b