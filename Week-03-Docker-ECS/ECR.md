# Amazon ECR - Elastic Container Registry

**Date Studied:** 31 March 2026
**Week:** 3 | **Day:** 2 | **Status:** Complete

---

## What Is It?
ECR is a private Docker image registry where you store and manage container images in AWS.

## How It Works (Key Concepts)
- Repository: Storage location for Docker images.
- Image URI: Full path used to push/pull images.
- Authentication: Required to push/pull (token-based login).
- Image Tagging: Versioning images (v1, v2 - avoid latest in prod).
- Image Scanning: Detects vulnerabilities on push.
- Lifecycle Policy: Automatically deletes old/unused images.
- Private Registry: Access controlled via IAM.
- Push/Pull: Upload/download images between local and ECR.
- Token Expiry: Auth token valid for ~12 hours.
- Integration: Used by ECS, EKS, CI/CD pipelines.

## What I Built Today (Hands-On)
- Created private ECR repository `flask-app`:
	- Enabled image scan on push
- Authenticated Docker to ECR:
	- Used `aws ecr get-login-password` with Docker login
- Tagged local image for ECR:
	- `flask-app:v1` > ECR URI format
- Pushed image to ECR:
	- Verified successful upload
- Confirmed image in ECR console:
	- Checked image size and tag
- Configured lifecycle policy:
	- Delete untagged images older than 1 day
- Performed pull test:
	- Deleted local image
	- Pulled image from ECR
	- Ran container and verified app works
- Saved image URI for ECS usage:
	- `004970146731.dkr.ecr.ap-south-1.amazonaws.com/flask-app:v2`

## Commands Used 
```bash
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 004970146731.dkr.ecr.ap-south-1.amazonaws.com
# Authenticate Docker to ECR

docker tag flask-app:v1 004970146731.dkr.ecr.ap-south-1.amazonaws.com/flask-app:v1
# Tag image for ECR

docker push 004970146731.dkr.ecr.ap-south-1.amazonaws.com/flask-app:v1
# Push image to ECR

docker pull 004970146731.dkr.ecr.ap-south-1.amazonaws.com/flask-app:v1
# Pull image from ECR
```

## What Broke / What Confused Me
Nothing broke I want to remember: ECR authentication expires every ~12 hours, so Docker push/pull will fail unless re-authenticated, especially in CI/CD pipelines.

## One-Line Summary
ECR is a secure, managed Docker registry in AWS used to store, version, and deploy container images reliably.

