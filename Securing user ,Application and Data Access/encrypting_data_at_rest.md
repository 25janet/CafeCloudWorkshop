# AWS KMS Encryption with Amazon S3, EBS, EC2, and CloudTrail

## Lab Overview
This lab demonstrates how AWS encrypts data at rest using **Amazon S3 default encryption** and **AWS Key Management Service (AWS KMS)**.  
It explores how encrypted Amazon EBS volumes interact with Amazon EC2 instances and how encryption key usage is monitored using **AWS CloudTrail**.

By the end of this lab, encryption behavior, key access control, and audit logging are clearly observed in a real AWS environment.

---

## Duration
**Approximately 30 minutes**

---

## Services Used
- Amazon S3  
- Amazon EC2  
- Amazon EBS  
- AWS Key Management Service (KMS)  
- AWS CloudTrail  

---

## Architecture

### Initial Architecture
- An Amazon S3 bucket for storing images  
- An EC2 instance  
- An AWS KMS key (to be created during the lab)

### Final Architecture
- An S3 bucket containing an object encrypted using **SSE-S3**
- An EC2 instance with:
  - An unencrypted root volume
  - An encrypted EBS data volume using a **customer managed KMS key**
- AWS KMS handling encryption and decryption requests
- AWS CloudTrail logging KMS and EC2 API activity

---

## Encryption Flow (EBS + KMS)

1. An encrypted EBS volume is attached to an EC2 instance.
2. The EC2 instance requests AWS KMS to decrypt the encrypted data key.
3. AWS KMS validates permissions and returns the plaintext data key.
4. The EC2 instance stores the key in memory and uses it for encryption and decryption operations.

---

## Task 1: Reviewing Default Encryption for Amazon S3

- Uploaded an image (`clock.png`) to an S3 bucket.
- Verified that **Server-Side Encryption with Amazon S3 managed keys (SSE-S3)** is enabled by default.
- Granted public-read access to the object.
- Accessed the object using its public URL.

**Key Observation:**  
Even though the object is encrypted at rest, Amazon S3 transparently decrypts it when accessed.

---

## Task 2: Creating an AWS KMS Customer Managed Key

- Created a **symmetric AWS KMS key**
- Assigned:
  - **Key administrators:** voclabs role
  - **Key users:** voclabs role
- Assigned alias: `MyKMSKey`

**Key Insight:**  
Customer managed keys provide full control over key usage, permissions, and rotation.

---

## Task 3: Creating and Attaching an Encrypted EBS Volume

- Observed the EC2 root volume (unencrypted).
- Created a new **1 GiB encrypted EBS volume** using `MyKMSKey`.
- Attached the encrypted volume to the EC2 instance.

**Result:**  
The EC2 instance successfully accessed the encrypted volume using AWS KMS.

---

## Task 4: Disabling the KMS Key and Observing Effects

- Disabled the `MyKMSKey`.
- Detached and attempted to reattach the encrypted EBS volume.

**Result:**  
Attachment failed because AWS KMS could not decrypt the data key while the key was disabled.

- Reviewed CloudTrail logs:
  - `DisableKey`
  - `AttachVolume` (failed)

- Re-enabled the KMS key.
- Successfully reattached the encrypted volume.

---

## Task 5: Analyzing AWS KMS Activity Using CloudTrail

Filtered CloudTrail event history by `kms.amazonaws.com` and reviewed:

- **CreateGrant**  
  Allows EC2 to use the KMS key for cryptographic operations.
- **Decrypt**  
  Used to decrypt the encrypted data key for EBS.
- **GenerateDataKeyWithoutPlaintext**  
  Used when generating encryption keys for EBS volumes.

**Key Insight:**  
CloudTrail provides a full audit trail of all KMS key usage.

---

## Task 6: Reviewing Key Rotation

- Enabled **automatic yearly key rotation** for `MyKMSKey`.

**Note:**  
Key rotation applies only to symmetric customer managed keys and occurs annually.

---

## Conclusion

In this lab, the following were successfully completed:

- Reviewed default encryption in Amazon S3
- Accessed encrypted S3 objects
- Created and used a customer managed AWS KMS key
- Encrypted and attached an EBS volume to an EC2 instance
- Observed the impact of disabling a KMS key
- Audited encryption activity using AWS CloudTrail
- Enabled automatic KMS key rotation

This lab highlights AWS best practices for **data encryption at rest, access control, and audit logging**.

---

## Author
**Shiru**  
AWS Student | Cloud & Security Enthusiast
