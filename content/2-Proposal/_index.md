---
title: "Proposal"
date: 2026-06-20
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# E-Commerce Perfume Store Backend Architecture  
## Optimized AWS Infrastructure Solution for a Perfume E-Commerce System  

### Executive Summary  
The E-commerce Perfume Store Backend System (`uyentrn/web-project`) is designed to provide a high-performance, secure, and scalable e-commerce platform specializing in perfume products. The platform focuses on optimizing the backend tier, managing product data, shopping carts, orders, users, and integrating AWS cloud services to ensure high availability and stable operations.  

### Problem Statement  
*Current Issues*  
Standalone e-commerce systems often struggle with load scaling, securing transaction data, managing static resources (such as perfume product images), and ensuring business continuity during traffic fluctuations.  

*Solution*  
The platform utilizes **Amazon API Gateway** as the API gateway, **Amazon S3** for static asset storage, and **Amazon RDS** (Primary & Standby) for relational databases. The architecture implements a secure Virtual Private Cloud (VPC), leverages **Amazon CloudFront** combined with **AWS WAF** for content delivery and security protection, and employs **EC2** instances running in an **Auto Scaling Group** behind an **Application Load Balancer (ALB)** to handle backend operations.  

*Benefits and Return on Investment (ROI)*  
This solution establishes a robust backend foundation for developing e-commerce features, simplifies data management, improves reliability and user data security, while optimizing cloud infrastructure operational costs.  

### Solution Architecture  
The platform implements an AWS Multi-AZ architecture within a VPC network (10.0.0.0/16). User requests pass through CloudFront and WAF, then route via ALB to EC2 instances located in private subnets, which securely connect to the RDS Primary and Standby databases.  

*AWS Services Used*  
- **Amazon API Gateway**: Gateway and management service for backend APIs.  
- **Amazon S3**: Storage for static assets, product images, and system files.  
- **Amazon RDS (Primary & Standby DB)**: Multi-AZ relational database service ensuring secure perfume transaction data.  
- **Amazon EC2 & Auto Scaling Group**: Backend application servers hosted in private subnets, scaling automatically based on load.  
- **Application Load Balancer (ALB) & Regional NAT Gateway**: Internal traffic routing and secure outbound internet connectivity.  
- **AWS CloudFront & WAF**: Content acceleration and comprehensive web security.  
- **Shared Services**: CloudWatch (system monitoring), Secrets Manager (secrets management), KMS (data encryption), IAM (access control and permission management).  

### Technical Implementation  
*Backend-Centric Focus*  
- Develop core business logic for the perfume store (product catalog management, shopping cart, orders, checkout, and user authentication).  
- Integrate **Amazon API Gateway** and **RDS** for backend data queries and processing.  
- Utilize **Amazon S3** to store high-resolution images and static assets for perfume product lines.  
- Ensure secure database connections and authentication using **Secrets Manager**, **KMS**, and **IAM**.  

### Roadmap & Milestones  
- **Phase 1 (1 week)**: AWS infrastructure architecture design (RDS, S3, API Gateway, EC2, ALB, WAF).  
- **Phase 2 (2.5 weeks)**: Backend source code development, API implementation, and relational database configuration.  
- **Phase 3 (1.5 weeks)**: System testing, CI/CD pipeline integration, and production deployment.  

### Budget Estimation by Usage Tier  
Below is the estimated monthly AWS infrastructure cost for the E-commerce Perfume Store based on three user scale tiers (**1,000 users/month**, **5,000 users/month**, and **10,000 users/month**):  

| AWS Service | Low Tier<br>*(1,000 users/month)* | Medium Tier<br>*(5,000 users/month)* | High Tier<br>*(10,000 users/month)* |
| :--- | :---: | :---: | :---: |
| **Amazon RDS** (Primary/Standby) | $15.00 | $18.00 | $25.00 |
| **Amazon S3** (Storage & Requests) | $0.50 | $1.50 | $3.00 |
| **Amazon API Gateway** | $0.20 | $1.00 | $2.50 |
| **Amazon EC2 & ASG** | $8.50 | $12.00 | $20.00 |
| **Application Load Balancer (ALB)** | $16.00 | $16.00 | $18.00 |
| **Amazon CloudFront & Data Transfer** | $0.80 | $2.00 | $4.50 |
| **AWS WAF & Others** (CloudWatch, Secrets Mgr) | $6.00 | $6.00 | $8.00 |
| **Total Estimated Cost (USD/month)** | **$47.00 / month** | **$56.50 / month** | **$81.00 / month** |

### Risk Assessment & Security  
- **Infrastructure Security**: Leverage VPC, Private Subnets, WAF, and IAM to enforce strict access control.  
- **High Availability**: RDS Primary/Standby Multi-AZ deployment and Auto Scaling Groups mitigate the risk of service disruption during traffic spikes.  

### Expected Results  
*Technical Improvements*: A stable, highly secure, and scalable e-commerce perfume backend built on modern AWS infrastructure.  
*Long-Term Value*: A robust data and API foundation to support future business expansion and online retail features.