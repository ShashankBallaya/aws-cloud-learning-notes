# AWS CLI Deep Dive - Amazon Web Services Command Line Interface

**Date Studied:** 20 March 2026
**Week1:** 1 | **Day:** 5 | **Status:** Complete

---

## What Is It?
AWS CLI is a command-line tool that lets you manage AWS services directly from your terminal.

## How It Works (Key Concepts)
- CLI Commands: Structured commands to interact with AWS services (e.g., ec2, s3).
- Profiles: Store credentials and configurations locally.
- --query: Filters JSON output to return only required data.
- Idempotency: Running commands safely without unintended side effects.
- wait Command: Pauses execution until a resource reaches a desired state.
- Automation: CLI is used in scripts for repeatable infrastructure taks.
- AMI: Pre-configured OS image used to launch EC2 instances.
- Security Group via CLI: Full control over firewall rules programmatically.

## What I Built Today (Hands-On)
- Explored AWS resources using describe commands:
	- Listed VPCs using `describe-vpcs`.
	- Listed subnets with filtered output using `--query`.
	- Listed security groups in table format.
	- Checked CloudFront distributions.
- Created a security group entirely using CLI:
	- Used `create-security-group` with VPC ID.
	- Added SSH rule (port 22) for my IP.
	- Added HTTP rule (port 800) for all traffic.
- Retrieved latest Amazon Linux 2 AMI ID using `describe-images` with query filtering.
- Launched EC2 instance using only CLI (`run-instances`).
- Used `aws ec2 wait instance-running` to pause execution untill instane was ready.
- Retrieved public IP using `describe-instances` with query.
- Connected to EC2 using SSH and verified access.
- Terminated EC2 instance using CLI.
- Verified termination state using `describe-instances`,
- Deleted the security group using CLI.
- Understood command differences in Windows CMD (single-line, double quoted).

## Commands Used
``bash
aws ec2 describe-vpcs --output table
# Lists all VPCs in table format

aws ec2 describe-subnets --query "Subnets[*].SubnetId"
# Filters and returns only subnet IDs

aws ec2 describe-security-groups --output table
# Lists all security groups 

aws cloudfront list-distributions --output table
# Lists CloudFront distributions

aws ec2 create-security-group --group-name my-sg --description "CLI SG" --vpc-id vpc-XXXX
# Creates a new security group

aws ec2 authorize-security-group-ingress --group-id sg-XXXX --protocol tcp --port 22 --cidr YOUR_IP/32
# Allows SSH from you IP

aws ec2 authorize-security-group-ingress --group-id sg-XXXX --protocol tcp --port 80 --cidr 0.0.0.0/0
# Allows HTTP from anywhere 

aws ec2 describe-images --owners amazon --query "Images[*].ImageId"
# Fetches AMI IDs

aws ec2 run-instances --image-id ami-XXXX --instance-type t3.micro --key-names your-key --security-groups-ids sg-XXXX --subnet-id subnet-XXXX
# Launches EC2 Instance

aws ec2 wait instance-running --instance-id i-XXXX
# Waits untill instance is running

aws ec2 describe-instances --instance-id i-XXXX --query
"Reservations[*].Instances[*].PublicIpAddress"
# Retrieves public IP

aws ec2 terminate-instances --instance-ids i-XXXX
# Terminates EC2 instance

aws ec2 describe-instances --instance-ids i-XXXX --query
"Reservations[*].Instances[*].State.Name"
# Checks instance state

aws ec2 delete-security-group --group-id sg-XXXX
# Deleted security group
