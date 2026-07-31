---
title : "Introduction"
date : 2026-07-16 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

## Project Overview

The **Perfume Web** project is an e-commerce web application designed for online perfume retail. This workshop guides you through building and deploying a cloud infrastructure for the Perfume Web system on **Amazon Web Services (AWS)**, meeting standards for **High Availability**, **Auto Scaling**, and **Defense-in-Depth security**.

---
## System Architecture

![Architecture Overview](/images/5-Workshop/5.1-Workshop-overview/architecture.jpg)

---

## Core Components

The system is fully contained within an **Amazon VPC (`10.0.0.0/16`)** deployed across 2 **Availability Zones (AZ)**, integrated with AWS Edge and Managed Services:

* **Edge Security & Content Delivery:**
  * **AWS WAF (Web Application Firewall):** A web application firewall that helps prevent common security vulnerabilities (SQL Injection, XSS, DDoS).
  * **Amazon CloudFront:** A content delivery network (CDN) that accelerates data transmission speed and reduces latency for end users.
  * **Amazon S3:** Stores static resource files (perfume product images, static web assets).

* **Compute & Networking Layer:**
  * **Application Load Balancer (ALB):** Distributes traffic load from users to the backend application group.
  * **Auto Scaling Group (EC2):** A group of EC2 instances handling Perfume Web application logic placed in **Private Subnets** (`10.0.8.0/22` and `10.0.12.0/22`), automatically scaling the number of instances up or down based on actual load.
  * **Regional NAT Gateway:** Allows EC2 instances located in Private Subnets to securely access the Internet for software updates or external API calls.

* **Database Layer:**
  * **Amazon RDS (Primary & Standby DB):** A relational database with **Multi-AZ** configuration located in independent **Private Subnets** (`10.0.16.0/22` and `10.0.20.0/22`). Data is continuously synchronized to the Standby DB to ensure automatic disaster recovery (Failover) capabilities.

* **Shared Services & Governance:**
  * **AWS IAM:** Manages identity and access permissions according to the Principle of Least Privilege.
  * **AWS KMS (Key Management Service):** Manages encryption keys for data-at-rest.
  * **AWS Secrets Manager (SM):** Securely stores and manages database credentials and API keys.
  * **Amazon CloudWatch:** Collects logs, monitors performance, and triggers system alerts.

---

## Request Flow

The data processing flow of the Perfume Web system is executed sequentially from steps **1 to 7** on the architecture diagram:

1. **Sending Requests:** Users/Admins send access requests via the Internet. Requests pass through **AWS WAF** to check for safety before reaching **Amazon CloudFront**.
2. **Handling Static Assets:** **CloudFront** routes and directly responds to static assets (images, CSS, JavaScript) retrieved from **Amazon S3**.
3. **Forwarding Dynamic Requests:** API queries and business logic are pushed by CloudFront across the network boundary into the **VPC**.
4. **Load Balancing:** Dynamic access requests are forwarded to the **Application Load Balancer (ALB)**.
5. **Application Processing:** The **ALB** coordinates access to **EC2** servers running within the **Auto Scaling Group** at the Private Subnets.
6. **Database Querying:** Product and order data read/write operations are sent by EC2 to the **Amazon RDS Primary DB**. Data is simultaneously synchronized automatically to the **RDS Standby DB**.
7. **Outbound Connections:** When EC2 servers need software updates or external API integrations, traffic goes through the **Regional NAT Gateway** to reach the Internet.

---

## Workshop Objectives

Upon completing this workshop, you will master:
* Designing and planning standard **Amazon VPC Multi-AZ** network infrastructure.
* Building a multi-layered security architecture with **WAF**, **Private Subnets**, **KMS**, and **Secrets Manager**.
* Configuring load balancing and application auto-scaling mechanisms with **ALB** and **Auto Scaling Group**.
* Deploying a highly available **Amazon RDS Multi-AZ** database.
* Optimizing e-commerce application performance by separating static asset processing flows (S3/CloudFront) and dynamic processing flows (ALB/EC2).

---

## Estimated Duration

The table below details the step-by-step roadmap and estimated time to complete the practical workshop:

| Step | Content | Estimated Duration |
| :--- | :--- | :--- |
| 1 | Environment Preparation | ~30 minutes |
| 2 | VPC Setup | ~20 minutes |
| 3 | RDS Deployment | ~25 minutes |
| 4 | EC2 + App Deployment | ~45 minutes |
| 5 | S3 Configuration | ~20 minutes |
| 6 | Cognito Integration | ~30 minutes |
| 7 | Cleanup | ~15 minutes |
| **Total** | | **~3 hours** |

---

## Estimated Cost

The table below estimates the monthly maintenance cost for each AWS service in the system architecture (when operating 24/7 at a small/testing scale):

| AWS Service | Configuration / Estimated Specs | Estimated Cost / Month |
| :--- | :--- | :--- |
| **Amazon EC2 & Auto Scaling** | 2x `t3.micro` / `t3.small` running continuously across 2 AZs | ~$15.00 - $25.00 |
| **Amazon RDS Multi-AZ** | `db.t3.micro` (Primary + Standby DB) | ~$25.00 - $35.00 |
| **Application Load Balancer (ALB)** | 1 ALB + basic LCU | ~$18.00 - $22.00 |
| **Regional NAT Gateway** | 1 NAT Gateway (~$0.045/hour + data transfer fees) | ~$32.00 - $38.00 |
| **AWS WAF & CloudFront** | 1 Web ACL + Basic Rules & CDN Caching | ~$5.00 - $10.00 |
| **Amazon S3** | Static file storage & product images (< 10 GB) | ~$0.20 - $1.00 |
| **AWS Secrets Manager & KMS** | Database secret storage + Encryption keys | ~$1.50 - $2.50 |
| **Amazon CloudWatch** | Logs, Metrics, and basic monitoring Dashboards | ~$2.00 - $5.00 |
| **Total (Running 24/7)** | | **~$100.00 - $140.00 / month** |

> **Note:** If you only deploy this system for **hands-on practice/testing for about 2 - 3 hours** and clean up all resources immediately after completion, the actual incurred cost is about **$1.50 - $3.00 USD**.