# Amazon RDS - Relational Database Service

**Date Studied:** 27 March 2026
**Week:** 2 | **Day:** 5 | **Status:** Complete

---

## What Is It?
RDS is a managed database service that lets you run realtional databses without handling servers yourself.

## How It Works (Key Concepts)
- RDS Instance: Managed database server (MySQL, PostgreSQL, etc.).
- DB Subnet Group: Defines which subnets (usually private) the DB runs in.
- Endpoint: DNS name used to connect to the database.
- Security Group: Controls access (e.g., allow MySQL port 3306).
- Private Access: RDS can be isolated inside VPC (no public access).
- Multi-AZ: High availability with automatic failover to standby.
- Read Replica: Improves read performance using asynchronous copies.
- Automated Backups: Snapshots + point-in-time recovery.
- Monitoring: CloudWatch metrics for DB performance.
- Managed Services: AWS handles patching, backups, failover.

## What I Built Today (Hands-On)
- Created RDS MySQL instance:
  - Engine: MySQL 8.0
  - Instance type: db.t3.micro
  - Deployedin private DB subnets (no public access)
- Created DB subnet group:
  - Included private subnets across 2 AZs
- Configured security group `rds-lab-sg`:
  - Allowed port 3306 only from inside VPC
- Launched EC2 instance in public subnet as jump server
- Installed MySQL client on EC2:
  - Used `dnf install -y mariadb105` (Amazon Linux 2023)
- Connected to RDS from EC2 using endpoint:
  - `mysql -h <rds-endpoint> -u admin -p`
- Executed SQL operations:
  - Listed databases
  - Created database and table
  - Inserted, updated, and queried records
  - Described table structure
- Performed security test:
  - Attempted connection from local machine > failed (expected)
- Explored RDS Monitoring test:
  - Observed metrics like CPU, connections, IOPS, storage
- Verified automated backups enabled (1-day retention)
- Stopped RDS instance after testing to save cost

## Commands Used
```bash
sudo dnf install -y mariadb105
# Install MySQL-compatible client on Amazon Linux 2023

mysql -h <rds-endpoint> -u admin -p
# Connect to RDS instance

SHOW DATABASES;
# List all databases

USE labdb;
# Select database

CREATE TABLE users (id INT AUTO_INCREMENT PRIMARY KEY,
name VARCHAR(50), email VARCHAR(100),
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP);
# Create table

INSERT INTO users (name, email) VALUES ('Shashank', 'shashank@example.com');
# Insert data

SELECT * FROM users;
# Query data

UPDATE users SET email = 'updated@example.com' WHERE name = 'Shashank';
# Update record

DESCRIBE users;
# Show table schema
```

## What Broke / What Confused Me
Amazon Linux 2023 does not include `mysql` package directly.
Had to install `mariadb105` using `dnf` instead of `yum`.
The `mysql` command still works the same - only the package name differs.

## One-Line Summary
RDS is a managed realtional database service that provides secure, scalable, and highly available databases without manual infrastructure management.

