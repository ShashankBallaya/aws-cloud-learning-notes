# Amazon ECS Fargate - Container Deployment

**Date Studied:** 01 April 2026
**Week:** 3 | **Day:** 3 | **Status:** Complete

---

## What Is It?
ECS Fargate lets you run containers without managing servers - AWS handles the infrastructure.

## How It Works (Key Concepts)
- ECS Cluster: Logical group where services and tasks run.
- Fargate: Serverless compute for containers (no EC2 needed).
- Task Definition: Blueprint (CPU, memory, image, ports).
- Task: Running instance of a task definition.
- Service: Maintains desired number of running tasks.
- ALB Integration: Routes traffic to containers.
- Target Type (IP): Required for Fargate (not instance-based).
- Security Group Chain: ALB > ECS tasks controls access.
- Public vs Private Subnets: Controls internet accessibility.
- Image Pull: Tasks must reach ECR (via internet or VPC ecdpoints).

## What I Built Today (Hands-On)
- Created ECS cluster `flask-cluster-w3-d3` using Fargate.
- Created task definition `flask-task`:
	- CPU: 0.25 vCPU, Memory: 0.5 GB
	- Container: `flask-container`
	- Image: ECR URI
	- Port: 5000
- Created security groups:
	- `ecs-alb-sg`: HTTP (80) from anywhere
	- `ecs-tasks-sg`: TCP 5000 only from `ecs-alb-sg`
- Created target group `flask-tg`:
	- Target type: IP 
	- Port: 5000
	- Health check path: `/health`
- Created ALB `flask-alb`:
	- Internet-facing
	- Attached to 2 public subnets
	- Listener HTTP 80 > `flask-tg`
- Created ECS service `flask-service`:
	- Desired tasks: 2
- Debugged deployment issues:
	- Fixed invalid ECR images URI (removed `https://`)
	- Resolved networking issue (tasks couldn't reach ECR in private subnet)
- Moved tasks to public subnets with public IP enabled.
- Verified both tasks reached RUNNING state.
- Confirmed both targets healthy in target group.
- Tested endpoints via ALB BND:
	- `/`, `/health`, `/info` all working
- Set desired tasks to 0 to stop charges.
- Deleted ALB after testing.

## Commands Used 
```bash
# No major CLI usage - setup done via AWS Console
```

## What Broke / What Confused Me
ECR image URI must not include `https://` - only repository URI format works.
Tasks in private subnets failed to pull image due to no outbound internet access.
This reinforced that private subnets require NAT Gateway or VPC endpoints to access AWS services like ECR.

## One-Line Summary 
ECS Fargate runs container without servers using task definitions and services, with ALB routing and secure networking via VPC design.

