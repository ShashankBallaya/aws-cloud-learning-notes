# GitHub Actions - CI/CD Pipeline for ECS Fargate

**Date Studied:** 03 April 2026
**Week:** 3 | **Day:** 5 | **Status:** Complete

---

# What Is It?
GitHub Actions automates build and deployment so every code push can update your application without manual steps.

## How It Works (Key Concepts)
- Workflow: YAML file defining CI/CD steps.
- Trigger: Runs pipeline on events (e.g., push to main).
- Runner: VM (ubuntu-latest) where jobs execute.
- Secrets: Secure storage for credentials (AWS keys).
- Build & Push: Docker image built and pushed to ECR.
- Image Tagging: Uses git SHA for traceability.
- Task Definition Revision: New version created for each deploy.
- Service Update: ECS replaces old tasks with new ones.
- wait-for-service-stability: Ensures deployment success before pipeline completes.
- CI/CD: Continuous Integration + Continuous Deployment pipeline.

## What I Built Today (Hands-On)
- Created GitHub Actions workflow:
	- Path: `.github/workflow/deploy.yml`
- Configured trigger:
	- Runs only on push to `main` branch
- Added GitHub Secrets:
	- `AWS_ACCESS_KEY_ID`
	- `AWS_SECRET_ACCESS_KEY`
- Ran first pipeline:
	- Verified all steps executed successfully 
- Performed end-to-end deployment test:
	- Updated home route text to `Version 2 - Auto Deployed via CI/CD`
	- Pushed code to `main`
	- Pipeline triggered automatically 
- Observed pipeline steps:
	- Code checkout
	- AWS authentication 
	- ECR login 
	- Docker build and push 
	- ECS task definition update
	- ECS service deployment
- Verfied deployment:
	- Accessed ALB DNS
	- Confirmed updated version live
- Measured deployment time:
	- ~5 minutes from push to production

## Commands Used 
```bash
git add .
git commit -m "Update home route - version 2"
git push origin main
# Triggers GitHub Actions pipeline
```

## One-Line Summary 
GitHub Actions automates Docker build, push to ECR, and ECS deployment, enabling fast and reliable CI/CD for containerised applications.

