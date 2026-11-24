AWS 3-Tier Web Application Architecture

Project Overview

This project demonstrates the design and deployment of a 3-Tier Web Application Architecture on Amazon Web Services (AWS).

The infrastructure separates the web, application, and database layers to support better security, scalability, and availability.

Architecture Diagram

"AWS 3-Tier Architecture" (architecture/aws-3-tier-architecture.png)

AWS Services Used

- Amazon VPC
- Public and Private Subnets
- Internet Gateway
- NAT Gateway
- Amazon EC2
- Application Load Balancer
- EC2 Auto Scaling
- Amazon RDS MySQL
- Security Groups
- Amazon CloudWatch

Architecture Design

1. Web Tier

The web tier uses Nginx servers to handle incoming web requests through an internet-facing Application Load Balancer.

2. Application Tier

The application tier runs the PHP application on EC2 instances placed in private subnets. An internal Load Balancer distributes traffic to the application servers.

3. Database Tier

Amazon RDS MySQL is deployed in private database subnets. Database access is restricted to the application tier.

Key Features

- VPC with public and private subnets
- Multi-Availability Zone network design
- Load balancing
- Auto Scaling
- Private database deployment
- Security Group-based access control

Project Screenshots

Deployment screenshots are available in the "screenshots" directory.

What I Learned

- Designing AWS network architecture
- Configuring public and private subnets
- Understanding Load Balancer traffic flow
- Working with EC2 Auto Scaling
- Connecting application servers to RDS
- Applying security practices in AWS

This repository documents my implementation and learning from the project.

Author

Sagar Chincholi

BCA Graduate | Cloud Architecture and DevOps

GitHub: "SagarChincholi" (https://github.com/SagarChincholi)

LinkedIn: "Sagar Chincholi" (https://www.linkedin.com/in/sagar-chincholi-ab548630a/)
