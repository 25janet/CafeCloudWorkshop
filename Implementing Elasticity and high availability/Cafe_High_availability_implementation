# Café Web Application: Scalable and Highly Available Environment on AWS

**Scenario:** The café anticipates a sudden surge in website traffic due to an upcoming TV feature. The existing web server runs in a single Availability Zone, which risks overloading the system. To ensure a smooth customer experience, the architecture needs to be highly available and scalable.

**Goal:** Implement a highly available and scalable AWS architecture for the café’s web application using EC2, Auto Scaling, and Application Load Balancer.

---

## Lab Overview and Objectives

After completing this lab, I should be able to:

* Inspect and evaluate an existing VPC
* Update network resources for multi-AZ deployment
* Create an Application Load Balancer (ALB)
* Create a launch template from an AMI
* Create an Auto Scaling group (ASG) with scaling policies
* Set a CPU-based scaling alarm
* Test load balancing and automatic scaling



**AWS Services Used:**

* Amazon EC2
* Elastic Load Balancing (Application Load Balancer)
* Auto Scaling Groups
* VPC, Subnets, NAT Gateways
* Security Groups
* IAM Roles

---

## Step-by-Step Implementation

### 1. Inspecting the Environment

* Explore the current VPC configuration, including public and private subnets.
* Verify existing NAT gateway, EC2 instance, security groups, and route tables.

**Significance:** Ensures understanding of network layout and prepares for multi-AZ deployment.

### 2. Updating Network for Multi-AZ

* Created a second NAT gateway in Public Subnet 2 for high availability.
* Updated Private Subnet 2 route tables to direct internet-bound traffic to the new NAT gateway.

**Significance:** Enables EC2 instances in multiple AZs to access the internet securely.

### 3. Creating a Launch Template

* Used the pre-created AMI (Cafe WebServer Image)
* Configured:

  * Instance type: t2.micro
  * Key pair: created new key pair
  * Security group: CafeSG
  * IAM instance profile: CafeRole
  * Resource tags: Name = webserver

**Significance:** Standardizes instance creation for Auto Scaling, ensuring consistent configurations.

### 4. Creating an Auto Scaling Group (ASG)

* Created ASG using the launch template
* Deployed instances across Private Subnet 1 and Private Subnet 2
* Desired capacity: 2, Min: 2, Max: 6
* Configured target tracking scaling policy (Average CPU utilization = 25%)

**Significance:** Maintains high availability, automatically adds/removes instances based on load.

### 5. Creating a Load Balancer

* Created an HTTP Application Load Balancer in the public subnets
* Security group allows HTTP traffic from anywhere
* Created a target group and attached it to the ASG

**Significance:** Distributes incoming traffic across private instances, improving performance and fault tolerance.

### 6. Testing Load Balancing and Auto Scaling

#### 6.1 Testing Without Load

* Accessed the café application via ALB DNS (`/cafe` path)
* Verified application loads correctly

#### 6.2 Testing Automatic Scaling Under Load

* Connected to a running instance via Systems Manager
* Installed `stress` tool and ran CPU stress test
* Verified ASG launched additional instances to meet CPU target

**Significance:** Confirms the architecture scales automatically under high traffic.

---

## Key Takeaways

* Multi-AZ deployment ensures high availability
* Auto Scaling and ALB provide resilience and traffic management
* Private subnets enhance security for application servers
* CPU-based scaling ensures responsive performance under varying loads
* NAT gateways in multiple AZs prevent single points of failure

**Outcome:** The café web application now scales automatically, handles increased traffic efficiently, and maintains high availability, providing a smooth experience for customers during peak usage periods.
