---
title : "RDS Database Setup"
date : 2026-07-28
weight : 4
chapter : false
pre : " <b> 5.4 </b> "
---

## RDS PostgreSQL Setup Guide

### 1. Open the main RDS page, choose Databases and Create database

Go to the AWS Console, open the **Amazon RDS** service, and go to the **Databases** section.

On the main RDS page, choose **Create database** to start the configuration.

![RDS Create Database](/images/5-Workshop/5.4-RDS/rds-1.png)

At this step, if you want the full setup, choose the **Create database** option with **full configuration** to access the full settings page.

### 2. Select PostgreSQL engine and Easy create

At the engine selection step, choose **PostgreSQL**.

If AWS shows the **Easy create** option, you can enable it to use a quick setup. Easy create will use default settings while still ensuring the engine is PostgreSQL.

![Choose PostgreSQL and Easy create](/images/5-Workshop/5.4-RDS/rds-2.png)

### 3. Enter database name and choose self-managed password + master username

Next, enter the desired database name in the **DB instance identifier** or **Database name** field.

Choose the password management method as **Self-manage password**.

Enter:

- **Master username**: the admin user name (for example: `admin`)
- **Password** and **Confirm password**: the password you choose

![Enter database name and self-manage password](/images/5-Workshop/5.4-RDS/rds-3.png)

### 4. Choose connect to an existing EC2 and click Create database

At the connectivity setup step, select the existing **EC2 instance** in the same VPC or subnet.

Make sure the security group and network settings allow EC2 to connect to RDS.

Finally, review the settings and click **Create database** to launch the PostgreSQL RDS instance.

![Connect EC2 and Create database](/images/5-Workshop/5.4-RDS/rds-4.png)

After completion, RDS will start creating the PostgreSQL instance. You can use the provided endpoint to connect from EC2.