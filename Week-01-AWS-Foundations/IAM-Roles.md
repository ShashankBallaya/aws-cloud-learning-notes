# IAM Roles for EC2 - AWS Identity and Access Management (IAM)

**Date Studied:** 20 March 2026  
**Week:** 1  |  **Day:** 5  |  **Status:**  Complete

---

## What Is It?
IAM Roles for EC2 let your instance securely access AWS services without storing credentials.

## How It Works (Key Concepts)
- IAM Role: A set of permissions that can be assumed by AWS services like EC2.
- Instance Profile: Container that attaches an IAM Role to an EC2 instance.
- Temporary Credentials: Auto-generated short-lived credentials provided by AWS.
- IMDS (Instance Metadata Service): Endpoint inside EC2 that provides credentials securely.
- Policy: Defines what actions are allowed (e.g., S3 read-only).
- Trust Policy: Defines which service (EC2) can assume the role.
- Least Privilege: Grant only required permissions, nothing extra.
- No Static Keys: Eliminates the need for access keys on EC2.

## What I Built Today (Hands-On)
- Launched an EC2 instance using AWS CLI (no console used).
- SSH’d into the instance.
- Ran `aws s3 ls` and received `Unable to locate credentials`.
- Confirmed that EC2 has no credentials by default.
- Created IAM Role `EC2-S3-ReadOnly`:
  - Trusted entity: EC2
  - Attached policy: `AmazonS3ReadOnlyAccess`
- Attached IAM Role to EC2 via Console:
  - Actions → Security → Modify IAM role
- SSH’d back into EC2.
- Ran `aws s3 ls` again - successfully listed buckets.
- Verified identity using `aws sts get-caller-identity` — saw assumed-role ARN.
- Detached IAM Role from EC2.
- Ran `aws s3 ls` - failed again with credentials error.
- Re-attached IAM Role - command worked again.
- Terminated EC2 using CLI.
- Deleted security group using CLI.

## Commands Used
```bash
aws s3 ls  
# Lists all S3 buckets (fails without credentials, works with IAM role)

aws sts get-caller-identity  
# Shows the current identity and confirms the assumed IAM role

aws ec2 terminate-instances --instance-ids i-XXXX  
# Terminates the EC2 instance

aws ec2 delete-security-group --group-id sg-XXXX  
# Deletes the specified security group
```
## What Broke / What Confused Me
Nothing broke - but I want to remember: IAM role attachment is not instant sometimes; there can be a short delay before credentials are available inside EC2 via IMDS.

## One-Line Summary
IAM Roles allow EC2 to securely access AWS services using temporary credentials without storing access keys.
