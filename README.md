#  Cloud Architecture for Café Web Application

## Project Overview

This project demonstrates the design and implementation of a **secure, scalable, and highly available cloud architecture** for a café web application owned by **Sofia and Nikhil**, who want their services to be accessible online.

The goal of the project is to design an AWS-based architecture that supports:
- Online customer access
- Secure user and application access
- Reliable data storage
- Elastic scaling based on demand
- High availability and monitoring

This architecture follows **AWS best practices** and applies the **principle of least privilege** throughout.

---

## Business Scenario

Sofia and Nikhil own a café and want to:
- Make their café services available online
- Allow customers to access the web application reliably
- Secure customer and business data
- Handle traffic spikes during busy hours
- Monitor application performance and availability

---

## Architecture Layers

The solution is designed using a **layered cloud architecture approach**.

---

##  Network Layer

The network layer provides isolation, connectivity, and traffic control.

- Amazon VPC with CIDR block
- Public and private subnets across multiple Availability Zones
- Internet Gateway for public access
- Route Tables to control traffic flow
- Security Groups and Network ACLs for traffic filtering

**Purpose:**  
Ensures secure network segmentation and controlled access to resources.

---

##  Compute Layer

The compute layer hosts the café web application.

- Amazon EC2 instances for application hosting
- Instances deployed in private subnets
- Application Load Balancer (ALB) in public subnets
- Auto Scaling Group for elasticity

**Purpose:**  
Provides scalable and highly available application hosting.

---

##  Storage Layer

The storage layer manages application and static data.

- Amazon EBS for EC2 instance storage
- Amazon S3 for static assets (images, menus, backups)

**Purpose:**  
Ensures durable and cost-effective data storage.

---

##  Database Layer

The database layer stores application data securely.

- Amazon RDS (managed relational database)
- Database hosted in private subnets
- Security groups restricting access to application servers only
- Automated backups and snapshots

**Purpose:**  
Provides secure, managed, and reliable data persistence.

---

##  Security & Access Control

Security is enforced at multiple levels.

### IAM (Identity and Access Management)
- IAM users and groups with least-privilege permissions
- IAM roles attached to EC2 instances
- Read-only and admin access separated by role

### Application & Data Access Security
- HTTPS via load balancer
- No direct public access to databases
- Security groups limiting traffic flow
- Encrypted storage (EBS and RDS)

**Purpose:**  
Protects users, applications, and sensitive data.

---

##  Connectivity & Networking

- Secure communication between application and database layers
- Controlled inbound and outbound traffic
- Internal communication restricted to private subnets

**Purpose:**  
Ensures safe and efficient communication between system components.

---

##  Monitoring & Logging

- Amazon CloudWatch for metrics and logs
- Monitoring EC2 CPU, memory, and network usage
- Health checks via Application Load Balancer
- Alarms for performance thresholds

**Purpose:**  
Maintains visibility into system health and performance.

---

##  Elasticity & High Availability

- Auto Scaling adjusts compute capacity based on demand
- Resources distributed across multiple Availability Zones
- Load balancing for fault tolerance

**Purpose:**  
Ensures the application remains available during traffic spikes and failures.

---


## Conclusion

This project demonstrates the design of a **real-world cloud architecture** for a small business transitioning to online services. By combining networking, compute, storage, database, security, monitoring, and scalability, the café web application for Sofia and Nikhil is built to be **secure, reliable, and ready for growth**.

---

## Technologies Used

- AWS VPC
- Amazon EC2
- Elastic Load Balancing
- Auto Scaling
- Amazon RDS
- Amazon S3
- AWS IAM
- Amazon CloudWatch
