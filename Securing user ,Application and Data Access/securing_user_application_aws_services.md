# Securing User Applications on AWS – Learning Summary

## Overview
This document summarizes key concepts I have learned about securing user applications on AWS. It covers **identity and access management**, **user federation**, **encryption**, **multi-account governance**, and **AWS security services** used to protect applications, data, and infrastructure.

---

## 1. Managing Permissions on AWS

### Identity and Access Management (IAM)
AWS IAM is the core service used to manage **who can access AWS resources and what actions they can perform**. IAM works using policies written in JSON.

### IAM Groups
IAM groups are collections of users. Permissions are assigned to the group instead of individual users, making access management easier and more scalable.

### Role-Based Access Control (RBAC)
RBAC assigns permissions based on a user’s role (for example: admin, developer, or auditor).  
Users or services assume roles to gain the permissions required to perform tasks.

### Attribute-Based Access Control (ABAC)
ABAC uses **tags and attributes** (such as department, environment, or project) to control access.  
Permissions are evaluated dynamically based on matching attributes rather than fixed roles.

---

## 2. Federating Users

User federation allows external users to access AWS without creating IAM users.

### IAM
IAM can be used to federate users from external identity providers by allowing them to assume IAM roles.

### AWS IAM Identity Center (SSO)
IAM Identity Center provides **centralized single sign-on** access to multiple AWS accounts and applications using existing identity providers.

### Amazon Cognito
Cognito is designed for **application users**, not administrators.  
It provides sign-up, sign-in, authentication, and authorization for web and mobile apps.

### AWS SSO (now IAM Identity Center)
AWS SSO simplifies user access across AWS accounts and integrated SaaS applications.

---

## 3. OpenID Connect (OIDC) and SAML

### OpenID Connect (OIDC)
OIDC is an identity layer built on OAuth 2.0.  
It is commonly used for **modern web and mobile applications** to authenticate users and issue tokens.

### SAML (Security Assertion Markup Language)
SAML is an XML-based protocol used mainly in **enterprise environments** for single sign-on.  
It allows users to authenticate with an external identity provider and access AWS resources.

---

## 4. Managing Multiple AWS Accounts

### AWS Organizations
AWS Organizations allows you to **centrally manage multiple AWS accounts**.

#### Advantages
- Centralized billing
- Improved security isolation
- Account-level governance
- Easier compliance management

### Service Control Policies (SCPs)
SCPs define the **maximum permissions** allowed in accounts within an organization.  
They do not grant permissions but **restrict what IAM users and roles can do**.

### SCPs and IAM Policies Together
Permissions are granted only when:
- The action is **allowed by the IAM policy**
- The action is **not denied by the SCP**

Both must allow the action for it to succeed.

---

## 5. Permission Boundaries

Permission boundaries define the **maximum permissions an IAM role or user can have**.

### Permission Boundaries vs SCPs
- **Permission Boundaries:** Apply to individual IAM users or roles
- **SCPs:** Apply to entire AWS accounts or organizational units

Both act as guardrails but at different scopes.

---

## 6. AWS Control Tower
AWS Control Tower provides **automated landing zones** for multi-account environments.  
It sets up accounts with built-in security, logging, and governance best practices using guardrails.

---

## 7. Encrypting Data at Rest

### Key Management Service (KMS)
AWS KMS is a managed service used to **create, manage, and use encryption keys**.

### Types of Encryption
- **Symmetric encryption:** Same key used for encryption and decryption (most common)
- **Asymmetric encryption:** Uses a public and private key pair

### Envelope Encryption
Envelope encryption uses:
- A **data key** to encrypt data
- A **master key (KMS key)** to encrypt the data key

This improves performance and security.

---

## 8. Encryption Methods

### Client-Side Encryption
Data is encrypted **before** it is sent to AWS.  
The customer controls encryption keys.

### Server-Side Encryption
AWS encrypts data **after it is received** and stores it encrypted at rest.

---

## 9. AWS KMS Operations
- **Encrypt:** Encrypts data using a KMS key
- **Decrypt:** Decrypts encrypted data
- **GenerateDataKey:** Creates data keys for envelope encryption

---

## 10. AWS Security Services Overview

### Identity & Access
- **IAM:** Access control for AWS resources
- **IAM Identity Center:** Centralized SSO access

### Governance & Monitoring
- **AWS Organizations:** Multi-account management
- **CloudTrail:** Logs API activity
- **AWS Config:** Tracks resource configuration changes
- **Audit Manager:** Helps with compliance audits

### Threat Detection & Protection
- **Inspector:** Scans workloads for vulnerabilities
- **Detective:** Investigates security findings
- **Security Hub:** Central security findings dashboard

### Network & DDoS Protection
- **AWS Shield:** DDoS protection
- **AWS WAF:** Web application firewall
- **AWS Network Firewall:** Network traffic filtering

### Data Protection
- **KMS:** Encryption key management
- **Secrets Manager:** Secure storage for secrets
- **Amazon Macie:** Data discovery and PII detection
- **AWS Artifact:** Compliance reports

---

## Conclusion
This learning journey covers how AWS secures applications using **identity management, encryption, governance, and security monitoring services**. Combining IAM, Cognito, encryption, Organizations, and AWS security services ensures applications remain secure, scalable, and compliant.

---

## Author
**Shiru**  
AWS Student | Cloud & Security Enthusiast 
