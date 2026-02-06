# Securing Applications Using Amazon Cognito

## Lab Overview
User authentication and authorization are critical components of modern web applications. Managing these securely and efficiently can be complex. **Amazon Cognito** simplifies this process by providing managed user authentication, authorization, and temporary AWS credentials.

In this guided lab, Amazon Cognito is integrated into an existing **Birds web application** to secure protected pages and control access to AWS resources such as **Amazon DynamoDB**.

---

## Objectives
By completing this lab, you will be able to:

- Create an Amazon Cognito user pool
- Add and manage users in the user pool
- Integrate user authentication into a web application
- Configure an Amazon Cognito identity pool
- Use temporary AWS credentials for authorization
- Secure application access using role-based access control (RBAC)

---


---

## AWS Services Used
- Amazon Cognito (User Pools & Identity Pools)
- Amazon S3
- Amazon CloudFront
- Amazon DynamoDB
- AWS Cloud9
- AWS Identity and Access Management (IAM)
- Node.js

---

## Application Scenario
The **Birds web application** allows students to view and report bird sightings. It consists of:

### Public Pages
- Home page
- Birds educational page

### Protected Pages (Authentication Required)
- Sightings page
- Reporting page
- Administrator page

Authentication is implemented using an **Amazon Cognito user pool**, while authorization to access AWS services (DynamoDB) is handled using an **Amazon Cognito identity pool**.

---

## Architecture Overview

### Starting Architecture
- Node.js application running on AWS Cloud9
- Static website hosted in an Amazon S3 bucket
- CloudFront distribution for secure content delivery

### Intermediate Architecture (Authentication)
- Amazon Cognito User Pool added
- Cognito Managed UI for sign-in
- JWT tokens used for session validation

### Final Architecture (Authentication + Authorization)
- Amazon Cognito Identity Pool
- Temporary AWS credentials issued to authenticated users
- DynamoDB access controlled using IAM roles

---

## Authentication Flow (User Pool)

1. User requests a protected page.
2. Request reaches the Node.js application.
3. User is redirected to the Amazon Cognito Managed UI.
4. Cognito authenticates the user and returns an access token.
5. Token is validated by the application.
6. Protected content is returned through CloudFront.

---

## Authorization Flow (Identity Pool)

1. Authenticated user accesses administrator functionality.
2. Application sends the Cognito token to the identity pool.
3. Identity pool validates the token.
4. Temporary AWS credentials are issued.
5. Application uses credentials to access DynamoDB.
6. Data is returned securely to the user.

---

## Task Summary

### Task 1: Preparing the Lab Environment
- Downloaded application code
- Deployed static website to Amazon S3
- Started Node.js server in AWS Cloud9
- Verified CloudFront distribution

---

### Task 2: Reviewing the Birds Website
- Verified public access to educational pages
- Confirmed restricted access to protected pages
- Observed authentication requirement before Cognito integration

---

### Task 3: Configuring the Amazon Cognito User Pool
- Created a Cognito user pool (`bird_app`)
- Configured OAuth settings and login flows
- Created users:
  - `testuser` (student)
  - `admin` (administrator)
- Created an `Administrators` group and assigned admin user

---

### Task 4: Integrating User Pool Authentication
- Updated application configuration files
- Integrated Cognito user pool IDs and client IDs
- Restarted Node.js server
- Verified user authentication via Cognito Managed UI

---

### Task 5: Testing Authentication
- Logged in as `testuser` to access protected pages
- Verified access restriction for admin-only pages
- Logged in as `admin` to access administrator page

---

### Task 6: Configuring the Identity Pool
- Integrated Cognito user pool with identity pool
- Assigned default authenticated IAM role
- Enabled credential federation

---

### Task 7: Integrating Identity Pool Authorization
- Updated application to request temporary AWS credentials
- Passed Cognito tokens to identity pool
- Enabled DynamoDB access using IAM roles

---

### Task 8: Testing Authorization
- Logged in as admin
- Retrieved temporary AWS credentials
- Successfully accessed DynamoDB table
- Verified table row count through application

---

## Key Security Concepts Demonstrated
- Authentication vs Authorization
- Token-based authentication (JWT)
- Role-based access control (RBAC)
- Temporary AWS credentials
- Secure frontend-backend communication

---

## Conclusion
In this lab, the Birds application was successfully secured using Amazon Cognito. Authentication was handled through a Cognito user pool, while authorization to AWS resources was managed through an identity pool. This architecture demonstrates AWS best practices for securing web applications.

---

## Author
**Shiru**  
AWS Student | Cloud & Security Enthusiast
