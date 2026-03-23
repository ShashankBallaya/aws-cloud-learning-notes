# Advanced VPC - NAT Gateway + Private Subnets + Bastion Host + VPC Flow Logs

**Date Studied:** 23 March 2026
**Week:** 2 | **Day:** 1 | **Status:** Complete

---

## What Is It?
Advanced VPC setup lets you run private servers securely while still allowing controlled internet access and monitoring network traffic.

## How It Works (key Concepts)
- Private Subnet: Subnet without direct internet access (no IGW route).
- NAT Gateway: Allows outbound internet access from private subnet.
- Elastic IP: Static public IP used by NAT Gateway.
- Bastion Host: Public EC2 used as a secure entry point to private instances.
- Security Group Referencing: Allows traffic only from another SG instead of an IP.
- Route Table (Private): Routes internet-bound traffic only from another SG instead of an IP.
- No Public IP: Ensures the instance is not directly reachable from the internet.
- VPC Flow Logs: Captures network traffic metadata for monitoring and debugging.
- CloudWatch Logs: Stores and visualises flow logs.
- Cost Awareness: NAT Gateway and EIP incur charges if not cleaned up.

## What I Built Today (Hands-On)
- Added private subnet `10.0.2.0/24` to `week1-vpc` without public IP auto assign.
- Created NAT Gateway in `public-subnet-1a` with an Elastic IP.
- Created private route table:
	- Added route `0.0.0.0/0 > NAT Gateway`.
- Associated private route table with private subnet.
- Created security group `bastion-sg`.
	- Allowed SSH only from my IP.
- Created security group `app-server-sg`:
	- Allowed SSH only from `bastion-sg`.
- Launched Bastion Host EC2 in public subnet with public IP.
- Launched app server EC2 in a private subnet without a public IP.
- SSH'd into bastion host using public IP.
- From bastion, SSH'd into app server using private IP.
- Tested outbound internet from private EC2:
	- Ran `curl https://checkip.amazonaws.com` - received response.
	- Ran `sudo yum update -y` - packages downloaded successfully.
- Enables VPC Flow Logs on `week1-vpc` and sends logs to CloudWatch.
- Verified ACCEPT entries for SSH traffic in flow logs.
- Deleted the NAT Gateway and released the Elastic IP after testing to avoid costs.

## Commands Used 
```bash 
ssh -i your-key.pem ec2-user@bastion-public-ip
# SSH into bastion host

ssh -i your-key.pem ec2-user@<private-ip>
# SSH from bastion to private EC2

curl https://checkip.amazonaws.com
# Check outbound internet I (viw NAT Gatewat)

sudo yum update -y
# Test outbound connectivity by installing updates
```

## What Broke / What Confused ME
Nothing broke - but I want to remember: private subnet instances cannot access the internet unless the route table is correctly configured to use a NAT Gateway.

## One_Line Summary 
Advanced VP setups use NM Gateway, bastion host, and private subnets to isolate systems while maintaining controlled internet access securely.

