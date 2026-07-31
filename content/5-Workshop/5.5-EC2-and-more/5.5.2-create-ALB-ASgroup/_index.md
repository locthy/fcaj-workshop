---
title: "Create Auto Scaling Group and Application Load Balancer"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.5.2 </b> "
---

In this section, we will create an Auto Scaling Group and an Application Load Balancer (ALB).
---

## Create Launch Template

-    **EC2 -> Launch Templates -> Create launch template**

 - **Launch template name and description**


| Field                         | Value                        |
| ------------------------------ | ------------------------------ |
| Launch template name - require | `MonaPerfume-EC2-LT`           |
| Template version description   | `Template for MonaPerfume EC2` |

![Setting launch template](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/lt1.png)

- Select the AMI you previously created.
  ![Setting launch template](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/lt2.png)

| Field                         | Value                        |
| ------------------------------ | ------------------------------ |
| Instance type | `t3.micro`           |
| Key pair name   | Select the previously created key pair |

  ![Setting launch template](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/lt2.5.png)

- **Network settings**

| Field                     | Value                          |
| -------------------------- | -------------------------------- |
| Subnet                     | Don't include in launch template |
| Availability Zone          | Don't include in launch template |
| Firewall (security groups) | Select existing security group   |
| Security groups            | MonaPerfume-EC2-SG               |

![Setting launch template](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/lt3.png)

- **Advanced details**
  | Field | Value|
  | ---------- | -------- |
  | IAM instance profile | MonaPerfume-EC2-S3-SSM |

![Setting launch template](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/lt4.png)

2. **Create launch template**

## Create Target group

**EC2 -> Target groups -> Create target group**

1.  **Create target group**

- Settings - immutable

| Field                | Value          |
| --------------------- | ---------------- |
| **Target group name** | `MonaPerfume-TG` |
| **Protocol**          | HTTP             |
| **Port**              | 3000             |
| **IP address type**   | IPv4             |
| **VPC**               | MonaPerfume-VPC  |

![Setting target group](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/tg1.png)

- Health checks
  | Field | Value |
  | ------------------------- | ------------------------------ |
  | Health check protocol | HTTP |
  | Health check path | / (If a specific health check route exists in the backend, specify it here; otherwise, keep the default) |

![Setting target group](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/tg2.png)

- Advanced health check settings
  | Field | Value |
  | ------------------------- | ------------------------------ |
  | Interval | 10 |

2. Register targets - recommended

- Available instances (2)

Choose 2 instance created earlier with port **3000** then **Includes as pending below**

 **Next** -> **Create target group**

![Setting target group](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/tg3.png)
![Setting target group](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/tg4.png)

## Create Auto Scaling Group

- **EC2 -> Auto Scaling Group -> Choose launch template**

| Field                  | Value            |
| ----------------------- | ------------------ |
| Auto Scaling group name | `MonaPerfume-ASG`  |
| Launch template         | MonaPerfume-EC2-LT |

![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/asg1.png)

- **Choose instance launch options**

| Field                         | Value                                                                                |
| ------------------------------ | -------------------------------------------------------------------------------------- |
| VPC                            | `MonaPerfume-VPC`                                                                      |
| Availability Zones and subnets | MonaPerfume-VPC-subnet-private1-us-east-1a, MonaPerfume-VPC-subnet-private2-us-east-1b |

![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/asg2.png)

- **Configure group size and scaling - optional**

| Field               | Value |
| -------------------- | ------- |
| Desired capacity     | `2`     |
| Min desired capacity | `2`     |
| Max desired capacity | `4`     |

![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/asg3.png)

- **Add tags - optional**


| Field           | Value       |
| ---------------- | ------------- |
| Key              | `Name`        |
| Value - optional | `Scaling EC2` |

![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/asg4.png)

- **Create Auto Scaling Group**

## Create Application Load Balancer


**EC2 -> Load balancers -> Create load balancer**

1. Choose Application Load Balancer
   ![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb1.png)

2. **Basic configuration**
| Field           | Value       |
| ---------------- | ------------- |
| Load blancer name              | `MonaPerfume-ALB`        |

   ![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb2.png)

3. **Network mapping**
| Field           | Value       |
| ---------------- | ------------- |
| VPC              | `MonaPerfume-VPC`        |
| Availability Zones and subnets              | chọn tất cả public subnet        |

   ![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb3.png)

4. **Security groups**
| Field           | Value       |
| ---------------- | ------------- |
| Security groups              | `MonaPerfume-ALB-SG`        |
  
   ![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb4.png)

5. **Listener**
| Field           | Value       |
| ---------------- | ------------- |
| Protocol              | `HTTP`        |
| Port              | `80`        |
| Routing action              | `Forward to target group`        |
| Target group              | `MonaPerfume-TG`        |

   ![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb6.png)