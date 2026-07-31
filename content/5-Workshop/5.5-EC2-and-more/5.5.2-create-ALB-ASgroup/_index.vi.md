---
title: "Tạo Auto Scaling Group và Application Balancer"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.5.2 </b> "
---

Trong phần này, ta sẽ tạo Auto Scaling Group và Application Balancer

---

## Tạo Launch Template

-    **EC2 -> Launch Templates -> Create launch template**

 - **Launch template name and description**


| Trường                         | Giá trị                        |
| ------------------------------ | ------------------------------ |
| Launch template name - require | `MonaPerfume-EC2-LT`           |
| Template version description   | `Template for MonaPerfume EC2` |

![Setting launch template](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/lt1.png)

- Chọn AMI bạn đã tạo
  ![Setting launch template](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/lt2.png)

| Trường                         | Giá trị                        |
| ------------------------------ | ------------------------------ |
| Instance type | `t3.micro`           |
| Key pair name   | chọn keypair đã tạo |

  ![Setting launch template](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/lt2.5.png)

- **Network settings**

| Trường                     | Giá trị                          |
| -------------------------- | -------------------------------- |
| Subnet                     | Don't include in launch template |
| Availability Zone          | Don't include in launch template |
| Firewall (security groups) | Select existing security group   |
| Security groups            | MonaPerfume-EC2-SG               |

![Setting launch template](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/lt3.png)

- **Advanced details**
  | Trường | Giá trị|
  | ---------- | -------- |
  | IAM instance profile | MonaPerfume-EC2-S3-SSM |

![Setting launch template](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/lt4.png)

2. **Create launch template**

## Tạo Target group

**EC2 -> Target groups -> Create target group**

1.  **Create target group**

- Settings - immutable

| Trường                | Giá trị          |
| --------------------- | ---------------- |
| **Target group name** | `MonaPerfume-TG` |
| **Protocol**          | HTTP             |
| **Port**              | 3000             |
| **IP address type**   | IPv4             |
| **VPC**               | MonaPerfume-VPC  |

![Setting target group](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/tg1.png)

- Health checks
  | Trường | Giá trị |
  | ------------------------- | ------------------------------ |
  | Health check protocol | HTTP |
  | Health check path | / (nếu trong backend có mục healthcheck thì thay vào, không thì giữ nguyên) |

![Setting target group](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/tg2.png)

- Advanced health check settings
  | Trường | Giá trị |
  | ------------------------- | ------------------------------ |
  | Interval | 10 |

2. Register targets - recommended

- Available instances (2)

Click chọn 2 instance ta đã tạo với port **3000** và **Includes as pending below**

Nhấn **Next** và **Create target group**

![Setting target group](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/tg3.png)
![Setting target group](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/tg4.png)

## Tạo Auto Scaling Group

- **EC2 -> Auto Scaling Group -> Choose launch template**

| Trường                  | Giá trị            |
| ----------------------- | ------------------ |
| Auto Scaling group name | `MonaPerfume-ASG`  |
| Launch template         | MonaPerfume-EC2-LT |

![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/asg1.png)

- **Choose instance launch options**

| Trường                         | Giá trị                                                                                |
| ------------------------------ | -------------------------------------------------------------------------------------- |
| VPC                            | `MonaPerfume-VPC`                                                                      |
| Availability Zones and subnets | MonaPerfume-VPC-subnet-private1-us-east-1a, MonaPerfume-VPC-subnet-private2-us-east-1b |

![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/asg2.png)

- **Configure group size and scaling - optional**

| Trường               | Giá trị |
| -------------------- | ------- |
| Desired capacity     | `2`     |
| Min desired capacity | `2`     |
| Max desired capacity | `4`     |

![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/asg3.png)

- **Add tags - optional**


| Trường           | Giá trị       |
| ---------------- | ------------- |
| Key              | `Name`        |
| Value - optional | `Scaling EC2` |

![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/asg4.png)

- **Create Auto Scaling Group**

## Tạo Application Load Balancer

**EC2 -> Load balancers -> Create load balancer**

1. Chọn Application Load Balancer
   ![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb1.png)

2. **Basic configuration**
| Trường           | Giá trị       |
| ---------------- | ------------- |
| Load blancer name              | `MonaPerfume-ALB`        |

   ![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb2.png)

3. **Network mapping**
| Trường           | Giá trị       |
| ---------------- | ------------- |
| VPC              | `MonaPerfume-VPC`        |
| Availability Zones and subnets              | chọn tất cả public subnet        |

   ![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb3.png)

4. **Security groups**
| Trường           | Giá trị       |
| ---------------- | ------------- |
| Security groups              | `MonaPerfume-ALB-SG`        |
  
   ![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb4.png)

5. **Listener**
| Trường           | Giá trị       |
| ---------------- | ------------- |
| Protocol              | `HTTP`        |
| Port              | `80`        |
| Routing action              | `Forward to target group`        |
| Target group              | `MonaPerfume-TG`        |

   ![Setting alb](/images/5-Workshop/5.5-EC2-and-more/5.5.2-create-ALB-ASgroup/alb6.png)
