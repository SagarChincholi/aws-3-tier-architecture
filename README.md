AWS 3-Tier Web Application Architecture

Project Overview

This project demonstrates the design and deployment of a 3-Tier Web Application Architecture using Amazon Web Services (AWS).

The infrastructure separates the application into three logical layers: Web Tier, Application Tier, and Database Tier. This separation improves security, scalability, maintainability, and availability.

The project focuses on understanding cloud infrastructure design, network configuration, load balancing, Auto Scaling, and database connectivity.

Project Objectives

- Design a custom AWS Virtual Private Cloud.
- Configure public and private subnets across Availability Zones.
- Deploy web and application servers in separate tiers.
- Configure an internet-facing Application Load Balancer.
- Configure an internal Application Load Balancer.
- Implement EC2 Auto Scaling.
- Deploy Amazon RDS MySQL in private subnets.
- Establish secure communication between application layers.
- Understand application traffic flow.
- Document the architecture and deployment process.

Architecture Diagram

"AWS 3-Tier Architecture" (architecture/aws-architecture.png)

Architecture Overview

The infrastructure is divided into three main layers.

Web Tier

The web tier handles incoming web requests.

Components:

- Nginx web servers
- Amazon EC2 instances
- Private subnets
- Internet-facing Application Load Balancer
- Web Auto Scaling Group

Application Tier

The application tier processes requests received from the web tier.

Components:

- PHP application servers
- Amazon EC2 instances
- Private subnets
- Internal Application Load Balancer
- Application Auto Scaling Group

Database Tier

The database tier stores application information.

Components:

- Amazon RDS MySQL
- Private database subnets
- Database security group
- Restricted database access

Network Design and Planning

The network is designed using Amazon VPC to provide an isolated and controlled environment for the application infrastructure.

Network Components

Component| Purpose
VPC| Provides an isolated virtual network
Public Subnets| Host internet-facing infrastructure
Private Web Subnets| Host web-tier EC2 instances
Private Application Subnets| Host application-tier EC2 instances
Private Database Subnets| Host the RDS database
Internet Gateway| Provides internet connectivity to public resources
NAT Gateway| Allows private resources to access the internet outbound
Route Tables| Control network traffic routing
Security Groups| Restrict communication between resources

Subnet Planning

The architecture uses multiple Availability Zones to distribute resources and reduce dependency on a single Availability Zone.

Tier| Subnet Type| Purpose
Load Balancer| Public| Receives external traffic
Web Tier| Private| Runs Nginx servers
Application Tier| Private| Runs PHP application servers
Database Tier| Private| Hosts RDS MySQL

Network Addressing

The following section documents the network addressing plan used in the project.

Network| CIDR Range| Type
VPC| Add your actual CIDR| VPC
Public Subnet A| Add your actual CIDR| Public
Public Subnet B| Add your actual CIDR| Public
Web Subnet A| Add your actual CIDR| Private
Web Subnet B| Add your actual CIDR| Private
Application Subnet A| Add your actual CIDR| Private
Application Subnet B| Add your actual CIDR| Private
Database Subnet A| Add your actual CIDR| Private
Database Subnet B| Add your actual CIDR| Private

Application Traffic Flow

The application follows this traffic flow:

User
 |
 v
Internet
 |
 v
Internet Gateway
 |
 v
Internet-facing Application Load Balancer
 |
 v
Web Tier - Nginx
 |
 v
Internal Application Load Balancer
 |
 v
Application Tier - PHP
 |
 v
Amazon RDS MySQL

Traffic Explanation

1. A user accesses the application through the internet.
2. The internet-facing Application Load Balancer receives the request.
3. The Load Balancer forwards traffic to healthy web-tier targets.
4. Nginx forwards application requests to the internal Load Balancer.
5. The internal Load Balancer distributes traffic to application servers.
6. The application tier communicates with the RDS database.
7. The response travels back through the application and web tiers.

AWS Services Used

AWS Service| Purpose
Amazon VPC| Network isolation
Subnets| Network segmentation
Internet Gateway| Public internet connectivity
NAT Gateway| Outbound internet access for private resources
Amazon EC2| Compute infrastructure
Application Load Balancer| Traffic distribution
EC2 Auto Scaling| Automatic instance capacity management
Amazon RDS MySQL| Managed relational database
Security Groups| Traffic control
Amazon CloudWatch| Monitoring and metrics

Security Design

Security was considered at the network and application levels.

- Web and application servers are deployed in private subnets.
- The database is deployed in private database subnets.
- The database is not intended to be directly accessible from the internet.
- Security Groups control communication between tiers.
- Application and database access is restricted to required ports.
- Sensitive credentials are not stored in the public repository.

Security Group Communication

Source| Destination| Port| Purpose
Internet| Public ALB| 80 / 443| Web access
Public ALB| Web Tier| Web application port| Forward web traffic
Web Tier| Internal ALB| Application port| Forward application requests
Internal ALB| Application Tier| Application port| Application processing
Application Tier| RDS| 3306| MySQL connectivity

The security rules should be adjusted according to the actual configuration. Unrestricted inbound access should be avoided wherever possible.

Project Screenshots

The screenshots document the deployment and configuration of the infrastructure.

Screenshot| Description
Architecture Diagram| Complete infrastructure overview
VPC Resource Map| VPC and subnet distribution
Load Balancer| ALB configuration and target health
Auto Scaling| Scaling group configuration
EC2 Instances| Web and application instances
RDS Database| Database deployment overview
Application| Successfully hosted application

Screenshots are available in the "screenshots" (screenshots/) directory.

Testing and Validation

The following checks were used to validate the deployment.

- Application accessibility through the public Load Balancer DNS name
- Web-tier target health
- Internal Load Balancer connectivity
- Application-to-database connectivity
- Database private accessibility
- Auto Scaling Group configuration
- Application availability during instance replacement

Only include tests that were actually completed and verified in the AWS environment.

Challenges and Troubleshooting

Building this architecture required understanding how multiple AWS services communicate with each other.

Load Balancer Target Health

Target health can be affected by incorrect health check paths, port mismatches, or security group rules.

Troubleshooting approach:

- Review target health details.
- Verify application responses.
- Check security group inbound rules.
- Confirm the correct target port.

Private Subnet Connectivity

Private instances may require appropriate routing and NAT configuration for outbound package installation or updates.

Troubleshooting approach:

- Verify route tables.
- Check NAT Gateway configuration.
- Confirm subnet route table associations.

Application-to-Database Connectivity

Database connections can fail because of incorrect credentials, database configuration, or security group rules.

Troubleshooting approach:

- Check connectivity from the application tier.
- Verify the database endpoint configuration.
- Confirm the allowed MySQL port.
- Review application connection settings.

Application Deployment

Web or application services may not start correctly because of configuration or service issues.

Troubleshooting approach:

- Review service status.
- Check configuration files.
- Inspect application logs.
- Verify the required packages and dependencies.

Add the specific errors encountered during your implementation and document how you resolved them.

Limitations

Although this architecture demonstrates important cloud concepts, it has some limitations.

- Infrastructure is configured manually rather than fully automated.
- Deployment may require manual intervention during initial setup.
- NAT Gateway, Load Balancers, and RDS can increase infrastructure costs.
- HTTPS and domain-based access may require additional configuration.
- Application deployment is not integrated with a complete CI/CD pipeline.
- Monitoring and alerting can be expanded.
- Backup and disaster recovery strategies require further development.

Future Improvements

The project can be enhanced with the following improvements.

Infrastructure Automation

- Implement Infrastructure as Code using Terraform.
- Automate VPC, subnet, ALB, EC2, and RDS provisioning.

CI/CD Integration

- Integrate GitHub Actions or AWS CodePipeline.
- Automate application deployment.
- Introduce version-controlled deployment workflows.

Security Enhancements

- Configure HTTPS using AWS Certificate Manager.
- Add AWS WAF.
- Store credentials in AWS Secrets Manager.
- Implement least-privilege IAM policies.

Monitoring and Reliability

- Create CloudWatch dashboards and alarms.
- Configure centralized logging.
- Improve health checks and failure recovery.
- Implement automated backup and recovery procedures.

Cost Optimization

- Review EC2 and RDS instance sizing.
- Monitor NAT Gateway and Load Balancer costs.
- Use appropriate scaling policies.
- Remove unused resources after testing.

Key Learning Outcomes

Through this project, I strengthened my understanding of:

- AWS VPC and network architecture
- Public and private subnet design
- Route tables and internet connectivity
- Application Load Balancer configuration
- EC2 deployment and Auto Scaling
- Multi-tier application architecture
- Amazon RDS and database connectivity
- Security Groups and network security
- Cloud infrastructure troubleshooting
- Architecture documentation

Cleanup and Cost Management

AWS resources may continue generating charges even when the application is not actively used.

After completing the project:

- Remove Auto Scaling Groups and associated resources.
- Delete Load Balancers and target groups.
- Delete RDS resources after backing up required data.
- Terminate EC2 instances.
- Remove NAT Gateways and unused Elastic IP addresses.
- Delete unused VPC resources.

Always verify the resources in your AWS account before cleanup.


This repository documents my implementation, configuration, and learning experience.

Author

Sagar Chincholi

BCA Graduate | Cloud Architecture and DevOps

GitHub: "SagarChincholi" (https://github.com/SagarChincholi)

LinkedIn: "Sagar Chincholi" (https://www.linkedin.com/in/sagar-chincholi-ab548630a/)
