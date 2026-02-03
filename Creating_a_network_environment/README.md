# Networking Environment for the Café

##  Overview

This project documents the creation of a **secure, nonproduction networking environment** for the Café application using **Amazon VPC**. The goal is to design and test a **two-tier architecture** with enhanced security controls, without affecting the production environment.

The architecture separates the **application layer** and **database layer** into different private subnets, uses a **bastion host** for secure administrative access, and enables controlled internet access for private resources using a **NAT Gateway**.

---

##  Scenario Background

Sofía and Nikhil migrated the café’s database from a MariaDB instance on Amazon EC2 to **Amazon RDS**, and moved the database from a public subnet to a private subnet.

After consulting Mateo, an AWS systems administrator, they decided to further enhance security by:

* Placing the **application server in a separate private subnet**
* Using a **bastion host (jump box)** for administrative access
* Allowing private resources to **download patches securely**
* Testing the design in a **nonproduction VPC**

---

## Lab Objectives

By completing this lab, the following objectives are achieved:

* Create a **custom VPC** to securely host private resources
* Configure **public and private subnets**
* Enable **internet access** for private resources
* Add an extra security layer using a **NAT Gateway**
* Implement **least-privilege network access** using security groups and routing

---

##  Architecture Components

### 1. Virtual Private Cloud (VPC)

* Custom VPC created to isolate the café’s nonproduction environment
* Provides full control over networking configuration

### 2. Subnets

* **Public Subnet**:

  * Bastion Host
  * NAT Gateway
* **Private Subnet (Application Tier)**:

  * Application EC2 instance
* **Private Subnet (Database Tier)**:

  * Amazon RDS database instance

### 3. Bastion Host

* EC2 instance in the public subnet
* Used for **secure SSH access** to private EC2 instances
* Restricts administrative access to a single controlled entry point

### 4. NAT Gateway

* Deployed in the public subnet
* Allows private subnet resources to:

  * Download software updates
  * Access AWS services and the internet securely
* Prevents inbound internet access to private resources

### 5. Internet Gateway

* Attached to the VPC
* Enables internet connectivity for public subnet resources

---

##  Security Design

### Network-Level Security

* **Public Subnet** routes traffic through the Internet Gateway
* **Private Subnets** route outbound traffic through the NAT Gateway

### Instance-Level Security

* **Security Groups**:

  * Bastion Host: Allows SSH from trusted IPs only
  * Application Server: Allows SSH only from Bastion Host
  * Database: Allows traffic only from Application Server

This layered approach ensures:

* No direct internet access to private resources
* Reduced attack surface
* Strong separation of concerns

---

##  Final Architecture (High Level)

```
Internet
   |
Internet Gateway
   |
Public Subnet
 ┌───────────────┐
 | Bastion Host  |
 | NAT Gateway   |
 └───────────────┘
        |
        v
Private Subnet (App Tier)
 ┌────────────────────┐
 | Application EC2    |
 └────────────────────┘
        |
        v
Private Subnet (DB Tier)
 ┌────────────────────┐
 | Amazon RDS         |
 └────────────────────┘
```

---

##  Key Takeaways

* Private subnets greatly improve security by isolating critical resources
* Bastion hosts provide controlled administrative access
* NAT Gateways enable outbound internet access without exposing private resources
* AWS VPC makes it easy to experiment safely in nonproduction environments

---

##  Services Used

* Amazon VPC
* Amazon EC2
* Amazon RDS
* Internet Gateway
* NAT Gateway
* Security Groups
* Route Tables

---

