# AWS CLI Commands - Master Reference

Personal reference of every AWS CLI command used during my 6-Week Cloud Learning Journey

**Note:** Updated through Week 2 Day 2 - Commands added progressively as the roadmap continues.

---

## Table of Contents
- IAM[](#iam)
- EC2 - Describe/Query[](#ec2--describe--query)
- EC2 - Instance Lifecycle[](#ec2--instance--lifecycle)
- EC2 - Security Groups[](#ec2--security-groups)
- S3[](#s3)
- CloudFront[](#cloudfront)
- VPC - NAT Gateway and Elastic IP[](#vpc---nat-gateway-and-elastic-ip)
- General/Utility[](#general-utility)
- Common Flags Reference[](#common-flags-refernce)

---
## IAM

### Configure AWS CLI 
```Bash
aws configure
```
**What it does:** Sets up AWS CLI credentials, region, and output format.
**When to use:** When initialising CLI on a new system or profile.


### Get Caller Identity
```Bash
aws sts get-caller-identity
```
**What it does:** Returns details about the IAM identity making the request.
**When to use it:** To verify which account/user is currently authenticated.



#### List IAM Users
```Bash
aws iam list-users
```
**What it does:** Lists all IAM users in the account.
**When to use it:** To audit or view existing IAM users.

---
## EC2 - Describe / Query


### List Running Instances
``` Bash
aws ec2 describe-instances --filters "Name=instance-state-name,Values=running" --output table
```
**What it does:** Shows only running EC2 instances in table format.
**When to use it:** To quickly check active instances.


### Get Public IP of Instance
``` Bash
aws ec2 describe-instances --instance-ids i-XXXX --query "Reservations[0].Instances[0].PublicIpAddress" --output text
```
**What it does:** Extracts the public IP of a specific instance.
**When to use it:** When connecting to EC2 via SSH.


### Get Instance State
```Bash
aws ec2 describe-instances --instance-ids i-XXXX --query "Reservations[0].Instances[0].State.Name" --output text
```
**What it does:** Returns the current state of an instance.
**When to use it:** To check if an instance is running, stopped, etc.


### List VPCs
```Bash 
aws ec2 describe-vpcs --output table
```
**What it does:** Lists all VPCs in the account.
**When to use it:** When working with networking setups.


### List Subnets in VPC
```Bash 
aws ec2 describe-subnets --filters "Name=vpc-id,Values=vpc-XXXX" --query "Subnets[*].{ID:SubnetId,CIDR:CidrBlock,AZ:AvailabilityZone}" --output table
```
**What it does:** Lists subnets with key details for a specific VPC.
**When to use it:** When selecting subnets for resources.


### List Security Groups
```Bash
aws ec2 describe-security-groups --output table
```
**What it does:** Displays all security groups in table format.
**When to use it:** To review firewall configurations.
 

### Describe Specific Security Group
```Bash
aws ec2 describe-security-groups --group-ids sg-XXXX
```
**What it does:** Shows detailed info about a specific security group.
**When to use it:** To inspect the rules of a particular group.


### List Key Pairs
```Bash
aws ec2 describe-key-pairs --output table
```
**What it does:** Lists all EC2 key pairs.
**When to use it:** When managing SSH access keys.


### Get Latest Amazon Linux AMI
```Bash
aws ec2 describe-images --owners amazon --filters "Name=name,Values=amzn2-ami-hvm-*-x86_64-gp2" --query "sort_by(Images,&CreationDate)[-1].ImageId" --output text
```
**What it does:** Retrieves the latest Amazon Linux 2 AMI ID.
**When to use it:** When launching updated EC2 instances.

---
## EC2 - Instance Lifecycle

### Launch EC2 Instance
```Bash
aws ec2 run-instances --image-id ami-XXXX --instance-type t3.micro --key-name KEY --security-group-ids sg-XXXX --subnet-id subnet-XXXX --associate-public-ip-address --tag-specifications "ResourceType=instance,Tags=[{Key=Name,Value=my-ec2}]"
```
**What it does:** Launches a new EC2 instance with specified configuration.
**When to use it:** When creating instances via CLI.


### Wait for Instance Running
```Bash
aws ec2 wait instance-running --instance-ids i-XXXX
```
**What it does:** Waits until the instance reaches running state.
**When to use it:** In scripts to ensure instance readiness.


### Terminate Instance (Single)
```Bash
aws ec2 terminates-instances --instance-ids i-XXXX
```
**What it does:** Terminates a specific EC2 instance.
**When to use it:** When cleaning up resources.


### Terminate Multiple Instances
```Bash
aws ec2 terminate-instances --instance-ids i-XXXX i-YYYY
```
**What it does:** Terminates multiple EC2 instances at once.
**When to use it:** For bulk cleanup operations.

---
## EC2 - Security Groups

### Create Security Group
```Bash
aws ec2 create-security-group --group-name NAME --description "DESC" --vpc-id vpc-XXXX
```
**What it does:** Creates a new security group in a VPC.
**When to use it:** Before launching instances with custom rules.


### Allow SSH Access
```Bash
aws ec2 authorize-security-group-ingress --group-ids sg-XXXX --protocol tcp --port 22 --cidr YOUR-IP/32
```
**What it does:** Allows SSH access from a specific IP.
**When to use it:** For secure remote access.


### Allow HTTP Access
```Bash
aws ec2 authorize-security-group-ingress --group-id sg-XXXX --protocol tcp --port 80 --cidr 0.0.0.0/0
```
**What it does:** Opens HTTP access to the internet.
**When to use it:** For web servers.


### Delete Security Group
```Bash
aws ec2 delete-security-group --group-id sg-XXXX
```
**What it does:** Deletes a security group.
**When to use it:** When no longer needed.

---
## S3

### List Buckets
```Bash
aws s3 ls
```
**What it does:** Lists all S3 buckets.
**When to use it:** To view available storage buckets.


### List Bucket Contents
```Bash 
aws s3 ls s3://bucket-name
```
**What it does:** Lists files inside a bucket.
**When to use it:** To inspect bucket contents.


### Create Bucket
```Bash
aws s3 mb s3://bucket-name --region ap-south-1
```
**What it does:** Creates a new S3 bucket.
**When to use it:** Before uploading data.


### Delete Bucket (Force)
```Bash
aws s3 rb s3://bucket-name --force
```
**What it does:** Deletes a bucket and all its contents.
**When to use it:** For cleanup operations.


### Upload File
```Bash
aws s3 cp file.txt s3://bucket-name/
```
**What it does:** Uploads a file to S3.
**When to use it:** For backups or hosting files.


### Download File
```Bash
aws s3 cp s3://bucket-name/file.txt ./
```
**What it does:** Downloads a file from S3.
**When to use it:** To retrieve stored data.


### Sync Local to S3
```Bash
aws s3 sync ./folder s3://bucket-name/
```
**What it does:** Sync local foldet to S3.
**When to use it:** For bulk uploads.


### Sync S3 to Local
```Bash
aws s3 sync s3://bucket-name/ ./folder
```
**What it does:** Syncs S3 contents to local folder.
**When to use it:** For backups or replication.


### Delete File 
```Bash
aws s3 rm s3://bucket-name/file.txt
```
**What it does:** Delets a file from S3.
**When to use it:** To remove unwanted objects.

---
## CloudFront


### List Distributions
```Bash
aws cloudfront list-distributions --query "DistributionList.Items[*].{ID:Id,DomainName}" --output table
```
**What it does:** Lists CloudFront distributions with IDs and domains.
**When to use it:** To view CDN endpoints.


### Invalidate Cache
```Bash 
aws cloudfront create-invalidation --distribution-id EXXXX --paths "/*"
```
**What it does:** Clears cached content from CloudFront.
**When to use it:** After updating content.


### Invalidate (Auto Fetch ID)
```Bash
aws cloudfront create-invalidation --distribution-id $(aws cloudfront list-distributions --query "Distribution.Items[0].Id" --output text) --paths "/*"
```
**What it does:** Invalidates cache using dynamically fetched distribution ID.
**When to use it:** In scripts or automation.

---
## VPC - NAT Gateway and Elastic IP

### List NAT Gateways
```Bash
aws ec2 describe-nat-gateways --output table
```
**What it does:** List NAT Gateways.
**When to use it:** To manage outbound internet access.


### Delete NAT Gateway
```Bash 
aws ec3 delete-nat-gateway --nat-gateway-id nat-XXXX
```
**What it does:** Deletes a NAT Gateway.
**When to use it:** To reduce cost after use.


### List Elastic IPs
```Bash
aws ec2 descibe-addresses --output-table
```
**What it does:** Lists Elastic IPs.
**When to use it:** To manage public IP allocations.


### Release Elastic IP
```Bash
aws ec2 release-address --allocation-id eipalloc-XXXX
```
**What it does:** Releases an Elastic IP.
**When to use it:** To avoid unnecessary charges.

---
### General / Utility

### Check AWS CLI Version
```Bash
aws --version
```
**What it does:** Displays the installed AWS CLI version.
**When to use it:** To verify installation.


### Configure CLI 
```Bash 
aws configure
```
**What it does:** Sets up credentials and defaults.
**When to use it:** During intial setup.


### List Config
```Bash
aws configure list
```
**What it does:** Shows current CLI configuration.
**When to use it:** To debug configuration issues.

---

## Common Flags Reference
- `--output table` - formats output as a readable table
- `--output text` - returns plain text (useful in scripts)
- `--output json` - return full JSON response (default)
- `--query "..."` - JMESPath filter to extract specific fields
- `--filters "...'` - server-side filter to narrow results
- `--region` - override default region in one command
- `--profile` - use a named AWS CLI profile
