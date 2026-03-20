# AWS IAM RBAC CloudTrail Lab

---

## Table of Contents
- [Overview](#overview)
- [Objectives](#objectives)
- [Architecture](#architecture)
- [IAM Configuration](#iam-configuration)
- [Testing and Validation](#testing-and-validation)
- [CloudTrail Monitoring](#cloudtrail-monitoring)
- [Security Principles Applied](#security-principles-applied)
- [Conclusion](#conclusion)

---

## Overview
This project demonstrates the implementation of **Role-Based Access Control (RBAC)** in AWS using IAM, with **least privilege principles** applied to Amazon S3 access. Permissions are validated through real-world testing scenarios, and all activity is monitored using AWS CloudTrail.

---

## Objectives
- Configure IAM users, groups, and policies  
- Enforce least privilege access control  
- Validate permissions through practical testing  
- Monitor and audit user activity using CloudTrail  

---

## Architecture

The environment consists of three IAM users assigned to distinct roles:

- **admin-user** — Full administrative access  
- **dev-user** — Permission to create S3 buckets  
- **auditor-user** — Read-only access to S3 resources  

### Services Used
- AWS IAM  
- Amazon S3  
- AWS CloudTrail  

---

## IAM Configuration

### Users
![IAM Users](images/users.png)

Three IAM users were created to represent different roles within the environment.

---

### Groups
![IAM Groups](images/groups.png)

Users were organised into groups to simplify permission management:
- AdminGroup  
- Developers  
- Auditors  

---

### User → Group Mapping

#### Developer Mapping
![Dev User Group](images/dev-user-group.png)

The **dev-user** is assigned to the **Developers** group.

#### Auditor Mapping
![Auditor User Group](images/auditor-user-group.png)

The **auditor-user** is assigned to the **Auditors** group.

---

### Permissions (Developers)
![Developer Permissions](images/dev-permissions.png)

The **Developers group** was assigned:
- Custom policy: AllowCreateS3Bucket  
- AmazonEC2ReadOnlyAccess  
- AmazonS3ReadOnlyAccess  

---

### Permissions (Auditors)
![Auditor Permissions](images/auditor-permissions.png)

The **Auditors group** was restricted to:
- AmazonS3ReadOnlyAccess  

This ensures no write operations can be performed.

---

### Custom Policy (S3 Bucket Creation)
![Custom Policy JSON](images/custom-policy.png)

A custom IAM policy was created to allow:
- `s3:CreateBucket`  
- `s3:ListAllMyBuckets`  

This enforces controlled write access for developers only.

---

### AWS Managed Policy (Read-Only Access)
![Read Only Policy](images/readonly-policy.png)

The auditor role uses an AWS-managed policy allowing:
- `s3:Get*`  
- `s3:List*`  

This restricts the role to read-only operations.

---

## Testing and Validation

### Denied Action (Auditor User)
![Access Denied](images/access-denied.png)

The **auditor-user** attempted to create an S3 bucket and received an **AccessDenied** error, confirming that write access is restricted.

---

### Successful Action (Developer User)
![Successful Bucket Creation](images/success.png)

The **dev-user** successfully created an S3 bucket, validating that permissions were correctly applied.

---

### Bucket Verification
![S3 Buckets](images/buckets.png)

The created buckets are visible in the S3 dashboard, confirming successful resource creation.

---

## CloudTrail Monitoring

### Event History
![CloudTrail Events](images/cloudtrail-events.png)

CloudTrail logs all activity, including both successful and failed operations.

---

### Successful Event Details
![Success Event](images/success-event.png)

Logs show details of a successful **CreateBucket** action performed by dev-user.

---

### Access Denied Event Details
![Denied Event](images/denied-event.png)

Logs capture the **AccessDenied** error when auditor-user attempted the same action.

---

## Security Principles Applied

- **Least Privilege** — Users are granted only the permissions required for their role  
- **Role-Based Access Control (RBAC)** — Permissions are assigned through groups  
- **Audit Logging** — All activity is recorded using CloudTrail  
- **Access Validation** — Both successful and denied actions were tested  

---

## Conclusion

This project demonstrates a practical implementation of AWS IAM security principles, including **RBAC**, **least privilege enforcement**, and **activity monitoring using CloudTrail**. The combination of successful and denied test cases provides strong validation of access control mechanisms in a real-world cloud environment.
