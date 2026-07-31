---
title: "Create Security Group"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.3.2 </b> "
---

Security Group acts as a virtual firewall at the instance level to control inbound and outbound traffic. In this section, we will create a Security Group to attach to EC2 and ALB.

---

![Security Group diagram](/images/5-Workshop/5.3-vpc/5.3.2-creat-sg/ssg4.png)

#### Security Group for ALB

From the **VPC console**, go to **Security Groups** and choose **Create Security Group**.

1. **Basic details**
   | Field | Value |
   | ------------------------------ | ------------------ |
   | **Security group name** | `MonaPerfume-ALB-SG` |
   | **Description** | `Allow traffic from CloudFront to ALB` |
   | **VPC** | MonaPerfume-VPC |

2. **Inbound rules**
   | Type | Protocol | Port range | Source |
   | ---------- | -------- | --------- | --------- |
   | HTTPS | TCP | 443 | Anywhere-IPv4 | 0.0.0.0/0 |
   | HTTP | TCP | 80 | Anywhere-IPv4 | 0.0.0.0/0 |

3. **Outbound rules**

   | Type | Protocol | Port range | Destination |
   | ----------- | -------- | ---------- | ------------- |
   | All traffic | All | All | Anywhere-IPv4 | 0.0.0.0/0 |

#### Security Group for EC2

1. **Basic details**
   | Field | Value |
   | ------------------------------ | ------------------ |
   | **Security group name** | `MonaPerfume-EC2-SG` |
   | **Description** | `Allow traffic in and out EC2` |
   | **VPC** | MonaPerfume-VPC |

2. **Inbound rules**
   | Type | Protocol | Port range | Source |
   | ---------- | -------- | --------- | --------- |
   | Custom TCP | TCP | 3000 | MonaPerfume-ALB-SG |

3. **Outbound rules**

   | Type | Protocol | Port range | Destination |
   | ----------- | -------- | ---------- | ------------- |
   | All traffic | All | All | Anywhere-IPv4 | 0.0.0.0/0 |













