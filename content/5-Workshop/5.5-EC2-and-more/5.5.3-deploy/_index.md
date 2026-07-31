---
title : "Deploy environment setup"
date : 2026-07-28
weight : 3
chapter : false
pre : " <b> 5.5.3 </b> "
---

## 1. Goal

This section explains how to set up the development environment and deploy the perfume website system on AWS. After completion, the system will include:

- Backend running on Amazon EC2.
- PostgreSQL database using Amazon RDS.
- Frontend React deployed through Amazon S3 and Amazon CloudFront.
- Prisma ORM managing the database.
- Full application accessible via the Internet and communicating with the database in AWS.

---

## 2. Required tools

Before deployment, prepare the following tools:

- Node.js (LTS recommended)
- npm
- Git
- Prisma ORM
- PostgreSQL
- Docker and Docker Compose (if running local database)
- AWS account

---

## 3. Install Git and clone the project

On Amazon Linux EC2, install Git if it is not already installed:

```bash
yum install -y git
```

Change to the `ec2-user` home directory and clone the repository:

```bash
cd /home/ec2-user
git clone https://github.com/Thinkj07/perfume-web.git
```

If you want to work directly in the project folder:

```bash
cd /home/ec2-user/perfume-web
```

---

## 4. Install Node.js

On Amazon Linux EC2, use **NVM (Node Version Manager)** to install Node.js.

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

export NVM_DIR="$HOME/.nvm"
source "$NVM_DIR/nvm.sh"

nvm install --lts
nvm use --lts
```

Check the versions:

```bash
node -v
npm -v
```

---

## 5. Install project dependencies

Move into the backend folder:

```bash
cd backend
```

Install all packages:

```bash
npm install
```

---

## 6. Configure environment variables

Create the `.env` file:

```bash
cp .env.example .env
```

Example configuration:

```env
NODE_ENV=development
PORT=3000

DATABASE_URL=postgresql://postgres:password@database-1.xxxxx.ap-southeast-1.rds.amazonaws.com:5432/perfume_store?schema=public

JWT_SECRET=replace-with-secret-key
JWT_ISSUER=perfume-api
JWT_AUDIENCE=perfume-client

ACCESS_TOKEN_TTL_SECONDS=900
REFRESH_TOKEN_TTL_SECONDS=604800

BCRYPT_ROUNDS=12

AWS_REGION=ap-southeast-1
STAGE=production
```

In this file:

- `DATABASE_URL` is the connection string to Amazon RDS.
- `JWT_SECRET` is used to sign JWT tokens.
- `PORT` is the backend listening port.

---

## 7. Connect to Amazon RDS PostgreSQL

Check PostgreSQL connection:

```bash
nc -vz database-1.xxxxx.ap-southeast-1.rds.amazonaws.com 5432
```

If the connection succeeds, you will see:

```text
Connected to database-1.xxxxx.ap-southeast-1.rds.amazonaws.com:5432
```

---

## 8. Initialize the database

After configuring `.env`, run migrations:

```bash
npx prisma migrate deploy
```

If the project includes seed data:

```bash
npx prisma db seed
```

Run `db seed` only when you want to insert initial data into the system.

---

## 9. Run the backend

Start the server:

```bash
npm run dev
```

Expected output:

```text
API listening on port 3000
```

Check it at:

```
http://<EC2-Public-IP>:3000
```

---

## 10. Deployment architecture

The deployed system architecture is as follows:

```text
Internet
      │
      ▼
CloudFront
      │
      ▼
Amazon S3 (React Build)

Browser
      │
      ▼
Backend API (EC2)
      │
      ▼
Amazon RDS PostgreSQL
```

CloudFront distributes static assets (HTML, CSS, JavaScript, and images), while EC2 handles application logic and communicates with PostgreSQL on Amazon RDS.

---

## 11. Verify the system

After deployment completes, verify:

- Frontend is accessible through CloudFront or EC2.
- Backend returns data through the API.
- Prisma connects successfully to PostgreSQL.
- EC2 can access RDS.
- Users can register, log in, and interact with data.




