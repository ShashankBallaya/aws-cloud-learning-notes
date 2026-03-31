# Dockerfile - Python Flask App

**Date Studied:** 31 March 2026
**Week:** 3 | **Day:** 2 | **Status:** Complete

---

## What Is It? 
A Dockerfile packages a Python Flask app into a container so it runs consistent anywhere.

## How It Works (Key Concepts)
- Base Image: `python:3.11-slim` provides minimal Python runtime.
- WORKDIR: Sets the working directory inside the container.
- Layer Caching: Docker reuses unchanged layers to speed up builds.
- COPY Order: Copy dependencies first to optimize caching.
- pip install: Installs required Python packages inside the image.
- EXPOSE: Documents the port the app runs on (5000).
- CMD: Defines the default commands to start the app.
- Port Mapping: Connects container port to host (5000:5000).
- Immutable Image: Image doesn't change after build - rebuild for updates.


## What I Built Today (Hands-On)
- Created Flask app with 3 routes:
	- `/` > main endpoint
	- `/health` > health check 
	- `/info` > app info 
- Created `requirements.txt`:
	- `flask==3.0.0`
- Wrote Dockerfile:
	- Used `python:3.11-slim` as base image
	- Set working directory to `/app`
	- Copied `requirements.txt` first
	- Installed dependencies using pip
	- Copied `app.py`
	- Exposed port 5000
	- Defined startup command using CMD
- Built Docker image:
	- `docker built -t flask-app:v1 .`
- Ran container:
	- `docker run -d -p 5000:5000 flask-app:v1`
- Tested endpoints using curl:
	- Verified all routes return correct responses
- Tested Docker caching:
	- Modified `app.py` and rebuilt image
	- Observed `pip install` layer reused (CACHED)
	- Only application layer rebuilt

## Commands Used
```bash
docker build -t flask-app:v1 .
# Build Docker image 

docker run -d -p 5000:5000 flask-app:v1
# Run Flask container

curl http://localhost:5000/
# Test root endpoint

curl http://localhost:500/health
# Test health endpoint 

curl http://localhost:5000/info
# Test info endpoint
```

## What Broke / What Confused Me 
Nothing broke - but I want to remember: Docker layer caching depends strictly on file changes. If `requirements.txt` changes, the pip install step will run again, increasing build time.

## One-Line Summary 
Dockerfile for Flask app uses layer caching and minimal base image to build efficient, fast, and reproducible containers.

