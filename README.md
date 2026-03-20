# AWS IAM RBAC CloudTrail Lab

## Overview
This project demonstrates the implementation of Role-Based Access Control (RBAC) in AWS using IAM, with least privilege principles applied to S3 access. It includes validation of permissions through real test scenarios and monitoring of activity using AWS CloudTrail.

## Objectives
- Configure IAM users, groups, and policies
- Enforce least privilege access control
- Validate permissions through practical testing
- Monitor and audit user activity using CloudTrail

## Architecture
The environment consists of three IAM users assigned to different roles:

- admin-user: Full administrative access
- dev-user: Permission to create S3 buckets
- auditor-user: Read-only access to S3 resources

Services used:
- AWS IAM
- Amazon S3
- AWS CloudTrail

## IAM Configuration

### User Groups and Permissions

| Group        | Permissions                     |
|-------------|--------------------------------|
| AdminGroup   | Full administrative access     |
| Developers   | S3 bucket creation permissions |
| Auditors     | Read-only access               |

### Policy Design
Permissions were assigned based on least privilege principles. The developer role was granted only the ability to create S3 buckets, while the auditor role was restricted to read-only actions. Administrative access was limited to the admin user.

## Testing and Validation

### Successful Action
The dev-user was able to successfully create S3 buckets, confirming that the assigned permissions were correctly configured.

### Denied Action
The auditor-user attempted to create an S3 bucket and received an AccessDenied error, confirming that write actions were properly restricted.

## CloudTrail Monitoring

AWS CloudTrail was enabled to log and monitor all user activity within the environment.

### Key Observations
- Successful S3 bucket creation events were recorded for dev-user
- AccessDenied events were recorded for auditor-user
- Logs included detailed metadata such as timestamps, user identity, and event source

### Example Event
- User: auditor-user  
- Event: CreateBucket  
- Result: AccessDenied  

## Security Principles Applied

- Least Privilege: Users were granted only the permissions required for their role
- Role-Based Access Control (RBAC): Permissions were assigned through groups rather than individually
- Audit Logging: All actions were recorded using CloudTrail
- Access Validation: Both successful and denied actions were tested and verified

## Screenshots

Include the following:
- IAM users and group configuration
- Successful S3 bucket creation by dev-user
- Access denied error for auditor-user
- CloudTrail event logs showing activity

## Conclusion

This project demonstrates the practical implementation of IAM-based access control in AWS, along with validation and monitoring of user actions. It reflects real-world cloud security practices, including enforcing least privilege, testing access controls, and auditing activity using CloudTrail.
