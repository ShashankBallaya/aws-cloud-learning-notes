# ☁️ AWS Cloud Learning Notes

**Author:** Shashank Ballaya
**Focus:** Amazon Web Services (AWS) | Cloud Infrastructure | Networking & Security | CLI Automation

> A structured, week-by-week documentation of my AWS cloud learning journey — covering core services, networking, security, and hands-on CLI usage. Built as both a personal knowledge base and a demonstration of practical AWS skills for cloud roles.

---

## 📁 Repository Structure

```
aws-cloud-learning-notes/
│
├── Week-01-AWS-Foundations/        # Core AWS concepts: IAM, EC2, S3, global infrastructure
├── Week-02-Networking-Security/    # VPC, subnets, security groups, NAT, CloudFront
├── CLI-Commands.md                 # Master reference of AWS CLI commands (progressively updated)
└── README.md
```

> 🗓️ **This is an active, in-progress repository.** Currently updated through **Week 2** of a planned **6-Week Cloud Learning Roadmap**. New content is added progressively as the roadmap advances.

---

## 📚 Weekly Breakdown

### Week 01 — AWS Foundations
Core building blocks of AWS, establishing a solid foundation before moving into advanced services.

- AWS global infrastructure: Regions, Availability Zones, Edge Locations
- Identity and Access Management (IAM) — users, groups, roles, and policies
- Elastic Compute Cloud (EC2) — instance types, AMIs, key pairs, instance lifecycle
- Simple Storage Service (S3) — buckets, objects, storage classes, access policies
- AWS CLI setup and authentication (`aws configure`, `sts get-caller-identity`)

---

### Week 02 — Networking & Security
Building secure, production-ready network architecture on AWS.

- Virtual Private Cloud (VPC) — design, CIDR blocks, public/private subnets
- Security Groups and Network ACLs — inbound/outbound rule management
- NAT Gateway and Elastic IP — enabling secure outbound access for private subnets
- CloudFront CDN — content delivery and cache invalidation
- EC2 security best practices — SSH key management, least-privilege access

---

### 📄 CLI-Commands.md — Master CLI Reference

A comprehensive, service-by-service reference of every AWS CLI command used throughout this journey. Organised for quick lookup and reuse in real-world workflows.

**Sections covered:**
- **IAM** — configure credentials, list users, verify caller identity
- **EC2 (Describe/Query)** — list instances, get IPs, inspect VPCs and subnets, check security groups
- **EC2 (Instance Lifecycle)** — launch, wait, terminate instances via CLI
- **EC2 (Security Groups)** — create, configure ingress rules, delete groups
- **S3** — list, create, delete buckets; upload, download, sync files
- **CloudFront** — list distributions, trigger cache invalidations
- **VPC / NAT / Elastic IP** — manage NAT gateways and public IP allocations
- **General / Utility** — version checks, config management, common flags (`--output`, `--query`, `--filters`)

---

## 🛠️ Key Skills Demonstrated

- Hands-on AWS CLI proficiency across core services
- IAM policy design and access control
- EC2 provisioning and lifecycle management
- S3 storage configuration and file operations
- VPC architecture with public/private subnet design
- Network security with security groups and NACLs
- CloudFront content delivery and CDN management
- NAT Gateway configuration for private subnet routing
- Scripting-friendly CLI patterns using `--query` (JMESPath) and `--output` flags

---

## 🎯 Learning Outcomes

By following this repository, you will be able to:

- **Understand** the core AWS services and how they interact in real architectures
- **Apply** IAM best practices for secure, least-privilege access control
- **Build** and manage VPC networks with proper subnet segmentation
- **Operate** AWS infrastructure confidently through the CLI — not just the console
- **Prepare** for AWS certifications:
  - ✅ AWS Certified Cloud Practitioner (CLF-C02)
  - ✅ AWS Certified Solutions Architect – Associate (SAA-C03)

---

## 🗺️ Roadmap

| Week | Topic | Status |
|------|-------|--------|
| Week 01 | AWS Foundations (IAM, EC2, S3) | ✅ Complete |
| Week 02 | Networking & Security (VPC, CloudFront) | ✅ Complete |
| Week 03 | Databases & Storage (RDS, DynamoDB, EBS) | 🔄 Upcoming |
| Week 04 | Serverless & Application Services | 🔄 Upcoming |
| Week 05 | Monitoring, Logging & Cost Management | 🔄 Upcoming |
| Week 06 | Architecture Patterns & Exam Prep | 🔄 Upcoming |

---

## 💼 About This Repository

This repository represents a deliberate, structured approach to cloud learning — not just knowing what AWS services exist, but understanding *how* they fit together and *how to operate them* through both the console and the CLI.

For cloud recruiters and hiring managers: this repository demonstrates practical, working knowledge of the AWS ecosystem, disciplined documentation habits, and a commitment to continuous learning — all signals of readiness for cloud engineer, DevOps, or solutions architect roles.

---

## 👤 About the Author

**Shashank Ballaya** is actively building expertise in AWS cloud infrastructure, networking, and DevOps practices, intending to transition into a cloud or solutions architecture role.

📬 [LinkedIn](https://www.linkedin.com/in/shashankballaya) · 💻 [GitHub](https://github.com/ShashankBallaya)

---

*Last updated: Week 2, March 2026 — Updated progressively as the 6-week roadmap continues.*
