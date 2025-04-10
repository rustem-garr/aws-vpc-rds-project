Secure Multi-Tier AWS Architecture with EC2 and RDS

This project demonstrates how to build a secure, scalable, and production-grade multi-tier network architecture on AWS using VPC, subnets, EC2 instances, RDS, and NAT/Internet Gateways.

📌 Project Overview

Designed and deployed a secure three-tier architecture inside a custom VPC. It includes:

A public subnet hosting a bastion EC2 instance

A private subnet hosting an internal EC2 app server

A second private subnet hosting a MySQL RDS instance

Secure communication and routing via NAT Gateway and Internet Gateway

🧱 VPC Configuration

VPC: 618998-vpc-1 | CIDR: 10.10.20.0/24

Subnet 1 (Public): 618998-subnet-1 | 10.10.20.0/28 | Availability Zone: us-east-1a

Subnet 2 (Private EC2): 618998-subnet-2 | 10.10.20.16/28 | AZ: us-east-1c

Subnet 3 (Private RDS): 618998-subnet-3 | 10.10.20.32/28 | AZ: us-east-1d

Internet Gateway: 618998-igw

NAT Gateway: 618998-nat-gw

Elastic IP: Allocated for NAT Gateway

Route Tables:

Public route table with 0.0.0.0/0 → IGW

Private route table for EC2 with 0.0.0.0/0 → NAT GW

Private route table for RDS with only local routing

🛡️ Security Configuration

Public EC2 Security Group:

SSH (port 22) from specific IPs

Private EC2 Security Group:

SSH only from the public EC2’s SG

MySQL (3306) access to RDS

RDS Security Group:

Accepts MySQL traffic from private EC2 only

No public access to RDS — fully private

🗃️ RDS Database Configuration

Engine: MySQL 8.0

DB Instance Identifier: my-rds-database

Subnet Group: subnet-group-for-rds (subnets 2 & 3)

Database Created: 618998db

Table: students

CREATE TABLE students (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  program VARCHAR(100)
);

INSERT INTO students (name, program) VALUES
('Michael', 'MSCS'),
('John', 'MBA');

🧪 Testing & Connectivity

SSH into public EC2 (bastion)

From there, SSH into private EC2 (app)

Connect to RDS via MySQL CLI:

mysql -h <rds-endpoint> -u admin -p

Query the students table to verify inserts

🧼 Cost Optimization

All resources were deleted post-testing:

RDS, EC2s, NAT Gateway, EIP, IGW, VPC, Subnets

Avoided all running charges

🧠 Lessons Learned

VPC/subnet design fundamentals

Routing logic with NAT vs IGW

Subnet groups and secure RDS architecture

IAM, security groups, and bastion SSH

📈 Future Improvements

Infrastructure as Code using Terraform

Add CloudWatch Monitoring & Alerts

Integrate a Flask/Django app that connects to RDS

Use Boto3 or AWS SDK for automation

📸 Architecture Diagram

![Architecture Diagram](project-diagram.png)

👨‍💻 Author

Rustem Garryyev

Software Engineer | Cloud Enthusiast