# Top 25 Interview Questions - Junior Cloud Engineer

## Q1: What is the Shared Responsibility Model?
AWS secures the cloud - things like physical data centres, hardware, networking, and the hypervisor.
I'm responsible for securing what I run in the cloud - like OS patching, IAM, application security, and network configurations.
A simple way to think about it:
- "If AWS built it and I can't control it > AWS owns it"
- "If I configure it > I own it"
In my projects, I handled IAM roles, security groups, and S3 bucket policies - that's my side of the model.

## Q2: Security Group vs NACL
Security Groups are stateful, attached to instances, and only allow rules.
NACLs are stateless, attached to subnets, and support both allow and deny rules.
In practice: 
- "Security Groups are the main control"
- "NACLs act as a secondary layer"
In my projects, I used Security Groups extensively (ALB>EC2>RDS flow) and used NACLs mainly during VPC testing.

## Q3: Public vs Private Subnet
A public subnet has a route to an Internet Gateway, so resources can receive internet traffic.
A private subnet does not - resources use a NAT Gateway for outbound access only.
In my architecture:
- "ALB > public subnet"
- "EC2 and RDS > private subnets"
This ensures no direct internet access to backend resources.

## Q4: EC2 Instances Families
EC2 instances are categorised by use case:
- "T-series > burstable, low-cost (dev/tets, small apps)"
- "M-series > balances (general production workloads)"
- "C-series > compute-heavy (batch processing)"
- "R-series > memory-heavy (databases, caching)"
In my project, I used t3.micro for cost-effective testing

## Q5: IAM Best Practices
Key practices:
- Never use the root account for daily tasks
- Enable MFA
- USE IAM Roles instead of access keys 
- Follow least privilege
- Rotate credentials
- Never hardcode secrets
In my project, I used IAM Roles for EC2 instead of storing credentials.

## Q6: S3 Storage Classes 
S3 has multiple storage classes based on cost and access:
- Standard - frequent access
- Standard-IA - Infrequent access
- One Zone-IA - cheaper, single AZ
- Glacier - archival
- Intelligent-Tiering - auto optimisation
I also used lifecycle rules to move data to cheaper tiers 

## Q7: What is a VPC?
A VPC is a logically isolated network in AWS where I define IP ranges, subnets, routing, and security.
In my project:
- Created VPC with CIDR block
- Added public/private subnets
- Configured IGW, NAT, and route tables

