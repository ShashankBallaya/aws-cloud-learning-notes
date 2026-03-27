# Project 2 - Architecture Diagram + README Documentation

**Date Studied:** 26 March 2026
**Week:** 2 | **Day:** 4 | **Status:** Complete

---

## What Is It?
This project documents a complete production-style AWS architecture and explains how to deploy it using Terraform.

## How It Works (Key Concepts)
- 3-Tier Architecture: Separation of web (ALB), app (EC2), and database (RDS)
- VPC Boundary: Logical isolation of all cloud resources.
- Public Subnet: Hosts internet-facing components like ALB and NAT Gateway.
- Private Subnet: Hosts application servers with no direct internet access.
- DB Subnet: Isolated layer for databases across multiple AZs.
- Security Groups Chain: Controlled traffic flow (ALB > EC2 > RDS).
- Infrastructure as a Code (IaC): Terraform provisions all resources.
- Remote State: Stored in S3 with DynameDB locking for consistency.
- High Availability: Multi-AZ deployment for resilience.
- Documentation: README explains architecture, setup, and decisions.

## What I Built Today (Hands-On)
- Designed full 3-tier architecture diagram using draw.io:
  - Created VPC as outer dashed boundary.
  - Added public subnets with ALB and NAT Gateway.
  - Added private subnets with Auto Scaling EC2 instances.
  - Added DB subnets with RDS MySQL across AZs.
  - Included S3 and DynamoDB for Terraform remote state (outside VPC).
  - Drew arrows showing traffic flow and ports.
  - Annotated security group rules in diagram.
- Wrote complete README for `terraform-aws-webapp`:
  - Embedded architecture diagram.
  - Added tech stack table (AWS + Terraform components).
  - Documented security design using 3-layer SG chain.
  - Wrote step-by-step deployment instructions.
  - Added `terraform.tfvars.example` (no secrets).
  - Included "What I learned" and "Challenges" sections.
- Pinned project repository to GitHub profile.

## Commands Used
```bash
terraform init
# Initialize Terraform working directory 

terraform plan 
# Preview infrastructure changes

terraform apply 
# Create infrastructure

terraform destroy 
# Tear down infrastructure
```

## One-Line Summary 
> Built and documented a production-grade 3-tier AWS architecture using Terraform with clear networking, security, and deployment design.
