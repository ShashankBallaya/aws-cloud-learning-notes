# Week 2 Summary — March 23–28, 2025

## What I Built This Week

This week started with Advanced VPC. I added a private subnet to 
week1-vpc, created a NAT Gateway in the public subnet with an Elastic 
IP, and routed private subnet traffic through it. I set up a bastion 
host in the public subnet and an app server in the private subnet, 
SSH'd through the bastion into the private EC2, and confirmed outbound 
internet worked via curl and yum update. Enabled VPC Flow Logs to send 
traffic records to CloudWatch.

Next, I built an Application Load Balancer across two AZs with two EC2 instances, auto-configured via User Data. Verified that both targets are healthy, 
stopped one server, and watched ALB automatically reroute all traffic 
to the healthy instance.

Built an Auto Scaling Group with a launch template, scaling policies, 
and a CloudWatch CPU alarm with SNS email alerts. Tested scale-out to 
3 instances and scale into 1 manually.

For Project 2, I used Terraform to provision a full 3-tier HA 
architecture ALB in public subnets, EC2 ASG in private subnets, RDS 
MySQL in isolated DB subnets using modular Terraform with S3 remote 
state and DynamoDB locking.

On Day 5, I did a standalone RDS deep dive. Launched RDS MySQL in 
private DB subnets, connected from EC2 using mariadb105 (AL2023), and 
ran real SQL queries: CREATE TABLE, INSERT, SELECT, and UPDATE. Confirmed 
direct laptop connection timed out. RDS is private only.

## What Confused Me

The biggest challenge was Terraform. During Project 2, I hit a 
CIDR conflict because 10.0.2.0/24 already existed from the Week 1 manual 
labs. Fixed it by changing private subnet CIDRs to 10.0.10.0/24 and 
10.0.11.0/24 in terraform.tfvars. EC2 instances were also showing 
unhealthy in the target group because they had no outbound internet. Private subnets need a NAT Gateway to run yum install. Once I added 
The NAT Gateway module to Terraform and moved EC2 back to private 
Subnets everything worked.

## What I Am Most Proud Of

Project 2: a full 3-tier architecture provisioned with one Terraform 
apply command, with EC2 in private subnets behind a NAT Gateway, and 
RDS is completely isolated in DB subnets. It is live on GitHub with a 
complete README and architecture diagram.
