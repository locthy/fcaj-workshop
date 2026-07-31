---
title: "Creating a VPC and its Associated Resources/Features"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.3.1 </b> "
---

---


1.  Open **VPC Console** -> **Create VPC**

VPC configuration:

| Field                                      | Value            |
| ------------------------------------------- | ------------------ |
| **Resources to create**                     | VPC and more       |
| **Name tag auto-generation**                | `MonaPerfume-VPC`  |
| **IPv4 CIDR block**                         | `10.0.0.0/16`      |
| **IPv6 CIDR block**                         | No IPv6 CIDR block |
| **Tenancy**                                 | Default            |
| **Number of Availability Zones (AZs)**      | 2                  |
| **Number of public subnets**                | 2                  |
| **Number of private subnets**               | 2                  |
| **Public subnet CIDR block in us-east-1a**  | `10.0.0.0/22`      |
| **Public subnet CIDR block in us-east-1b**  | `10.0.4.0/22`      |
| **Private subnet CIDR block in us-east-1a** | `10.0.8.0/22`      |
| **Private subnet CIDR block in us-east-1b** | `10.0.12.0/22`     |
| **Private subnet CIDR block in us-east-1a** | `10.0.16.0/22`     |
| **Private subnet CIDR block in us-east-1b** | `10.0.20.0/22`     |
| **NAT gateways ($) - updated**              | Regional - new     |
| **VPC endpoints**                           | S3 Gateway         |

![vpc diagram](/images/5-Workshop/5.3-vpc/5.3.1-create-vpc-and-more/vpc7.png)

![vpc diagram](/images/5-Workshop/5.3-vpc/5.3.1-create-vpc-and-more/vpc8.png)

![vpc diagram](/images/5-Workshop/5.3-vpc/5.3.1-create-vpc-and-more/vpc9.png)

2. Choose **Create VPC**
