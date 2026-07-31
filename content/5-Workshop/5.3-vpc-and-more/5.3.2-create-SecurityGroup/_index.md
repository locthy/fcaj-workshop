---
title: "Create Security Group"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.3.2 </b> "
---

Security Groups act as virtual firewalls at the instance level to control inbound and outbound traffic. In this section, we will create Security Groups to attach to our EC2 instances and Application Load Balancer (ALB).

---

![Security Group diagram](/images/5-Workshop/5.3-vpc/5.3.2-creat-sg/ssg4.png)

#### Security Group cho ALB

From **VPC console** -> **Security Group** -> **Create Security Group**

1. **Basic details**
   | Field | Value |
   | ------------------------------| ------------------ |
   | **Security group name** | `MonaPerfume-ALB-SG`|
   | **Description** | `Allow traffic from CloudFont to ALB` |
   | **VPC** | MonaPerfume-VPC |

2. **Inbound rules**
   | Type | Protocol | Port range | Source | |
   | ---------- | -------- | --------- | --------- |--------- |
   | HTTPS | TCP | 443 | Anywhere-IPv4 |0.0.0.0/0 |
   | HTTP | TCP | 8 | Anywhere-IPv4 |0.0.0.0/0 |

3. **Outbound rules**

| Type        | Protocol | Port range | Destination   |           |
| ----------- | -------- | ---------- | ------------- | --------- |
| All traffic | All      | All        | Anywhere-IPv4 | 0.0.0.0/0 |

#### Security Group cho EC2

1. **Basic details**
   | Field | Value |
   | ------------------------------| ------------------ |
   | **Security group name** | `MonaPerfume-EC2-SG`|
   | **Description** | `Allow traffic in and out EC2` |
   | **VPC** | MonaPerfume-VPC |

2. **Inbound rules**
   | Type | Protocol | Port range | Source | |
   | ---------- | -------- | --------- | --------- |--------- |
   | Custom TCP | TCP | 3000 | MonaPerfume-ALB-SG | |

3. **Outbound rules**

| Type        | Protocol | Port range | Destination   |           |
| ----------- | -------- | ---------- | ------------- | --------- |
| All traffic | All      | All        | Anywhere-IPv4 | 0.0.0.0/0 |
