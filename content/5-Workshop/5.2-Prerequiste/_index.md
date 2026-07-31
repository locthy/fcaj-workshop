---
title : "Preparation Requirements"
date : 2024-01-01
weight : 2
chapter : false
pre : "  5.2.  "
---

## Overview
Below are the **AWS prerequisites** and **local machine preparation steps** before proceeding to package and deploy the **Perfume Web** project onto the AWS cloud computing infrastructure.

## AWS Prerequisites

To ensure a smooth deployment process, you need to prepare your AWS account and administrative tools as follows:

| Requirement | Detailed Description | Purpose of Use |
| --- | --- | --- |
| **AWS Account** | An AWS Root account or an IAM account with full administrative privileges (`AdministratorAccess`). | Manage and provision resources on the AWS Cloud. |
| **AWS CLI v2** | Install the AWS Command Line Interface on your local machine and configure it using `aws configure`. | Interact with AWS services (S3, EC2, RDS, Secrets Manager, etc.) via the command line. |
| **EC2 Key Pair** | Create an SSH Key Pair (`.pem` or `.ppk` format) in your intended deployment Region (e.g., `ap-southeast-1`). | Securely SSH into EC2 instances for configuration or troubleshooting when needed. |
| **Service Access Permissions** | Permissions to provision VPC, EC2, RDS, ALB, S3, CloudFront, WAF, Secrets Manager, KMS, and IAM. | Avoid `AccessDenied` errors during resource provisioning. |

---

## Local Machine Preparation Steps

Below are the source code preparation steps on your local machine before pushing the application to the cloud:

### Step 1: Clone the Project Source Code

Open a terminal on your local machine and clone the Perfume Web source code repository:

```bash
# Clone the repository from GitHub
git clone https://github.com/Thinkj07/perfume-web.git

# Move into the project directory
cd perfume-web

```

Basic project source code structure to verify:

* Frontend directory (React / Static Web)
* Backend directory (Node.js / Express API)
* Application configuration files (`package.json`, `.env.example`, etc.)

---

### Step 2: Separate Environment Variables & Security Information

Before pushing source code to the cloud, you **must absolutely avoid hardcoding** sensitive information (Database Password, Secret Key, API Key) in your source code.

1. **Check the `.gitignore` file:** Ensure that files containing sensitive information such as `.env`, `.env.local`, and SSH key files are not committed to Git.
2. **Prepare a sample configuration (`.env.example`):** Define the list of necessary environment variables to be fed into **AWS Secrets Manager**:
* `DB_HOST`: The endpoint address of the Amazon RDS Primary DB.
* `DB_PORT`: The database connection port (MySQL/PostgreSQL default: `3306` or `5432`).
* `DB_NAME`: The database name (`perfume_db`).
* `DB_USER` & `DB_PASSWORD`: Dynamically retrieved from AWS Secrets Manager.
* `S3_BUCKET_NAME`: The name of the bucket storing static assets.



---

### Step 3: Package Static Assets

The Perfume Web application contains static files (perfume product images, banners, CSS, JS).

1. Isolate the directory containing product images (`/public/images` or `/assets`).
2. Compress static files or prepare the directory structure to be uploaded to an **Amazon S3 Bucket** in subsequent steps using the AWS CLI:
```bash
# Reference command to be used in the S3 deployment step
aws s3 sync ./public s3://your-perfume-s3-bucket/ --acl public-read

```



---

### Step 4: Package Backend Source Code & Initialization Script

Since you will deploy the source code to EC2 instances within an Auto Scaling Group, prepare an automated installation script (**EC2 User Data Script**) on your local machine:

Create a `user-data.sh` file on your local machine with the following template content:

```bash
#!/bin/bash
# Update system and install dependencies
sudo yum update -y
sudo yum install -y git nodejs

# Clone source code onto the EC2 instance
cd /home/ec2-user
git clone https://github.com/Thinkj07/perfume-web.git
cd perfume-web

# Install libraries & start the application
npm install
npm start

```

---

### Step 5: Checkiness Readiness

Before moving on to building the VPC infrastructure on AWS, check the following checklist:

* The source code has been successfully tested and run locally.
* No hardcoded passwords or secrets remain in the codebase.
* AWS CLI is installed and connection testing is successful (`aws sts get-caller-identity`).
* An EC2 Key Pair has been pre-created on the AWS Management Console.
* The `user-data.sh` file or packaged source code is ready.
