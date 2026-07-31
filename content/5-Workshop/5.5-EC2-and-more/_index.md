---
title : "Setup Backend Server on EC2"
date : 2026-07-26
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

# Setup Backend Server on EC2

In this section, we will deploy the compute infrastructure for the Perfume Store Backend application inside the VPC Private Subnet, including creating IAM Roles, launching EC2 instances, setting up an Application Load Balancer (ALB), and deploying the Node.js/Express application.

#### Steps Included:

1. [Create IAM Role and EC2 Instance](5.5.1-create-EC2-Role/) - Create an IAM Role for SSM Session Manager & S3 access, then launch an EC2 instance in a Private Subnet.
2. [Create Target Group and Application Load Balancer](5.5.2-create-ALB-ASgroup/) - Configure Target Group (Port 3000) and Application Load Balancer (ALB) across Public Subnets.
3. [Environment Setup and Application Deployment](5.5.3-deploy/) - Connect to EC2 via SSM, install Node.js 22, Git, PM2, configure environment variables for RDS/S3, run database migrations, and launch the backend server.
