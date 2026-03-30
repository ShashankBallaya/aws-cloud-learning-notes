# Docker Fundamentals - Images, Containers, Dockerfile 

**Date Studied:** 30 March 2026
**Week:** 3 | **Day:** 1 | **Status:** Complete

---

## What Is It?
Docker lets you package an application and its environment into a container so it runs the same everywhere.

## How It Works (Key Concepts)
- Image: Read-only template used to create containers.
- Container: Running instance of an image.
- Dockerfile: Instructions to build a custom image.
- Layers: Images are built in layers for efficiency and caching.
- Port Mapping: Maps container port to host port (e.g., 8080:80).
- Detached Mode: Runs container in background (`-d` flag).
- Tagging: Versioning images (v1, v2, latest).
- Exec: Run commands inside a running container.
- Logs: View container output for debugging.
- Cleanup: Remove unused containers/images to save space.

## What I Built Today (Hands-On)
- Installed Docker and verified using `docker --version`.
- Ran `hello-world` container to confirm setup.
- Pulled and ran Nginx container:
	- Ran in detached mode on port 8080.
	- Accessed via `http://localhost:8080`.
- Explored container operations:
	- Listed running and stopped containers.
	- Viewed logs and accessed container shell.
	- Navigated to `/usr/share/nginx/html/`.
- Cleaned up:
	- Stopped and removed containers.
	- Removed images.
	- Ran `docker system prune`.
- Created project folder `my-webapp` with `index.html`.
- Wrote Dockerfile:
	- Base image: `nginx:latest`
	- Copied HTML into container
	- Exposed port 80
- Built custom image:
	- `docker build -t my-webapp:v1 .`
- Ran container from custom image:
	- Served custom HTML on `https://localhost:8080`.
- Used `docker history` to inspect image layers.
- Tagged image:
	- `docker tag my-web-app:v1 my-webapp:latest`
- Modified HTML and rebuilt image as v2.
- Ran v1 and v2 container simultaneously:
	 - Verified both versions on different ports.

## Commands Used
```bash
docker --version
# Check Docker installation

docker run hello-world
# Test Docker setup 

docker run -d -p 8080:80 nginx
# Run nginx container in background

docker ps
# List running containers

docker ps -a 
# List all containers

docker logs <container-id>
# View logs 

docker exec -it <container-id> bash
# Access container shell

docker stop <container-id>
# Stop container

docker rm <container-id>
# Remove container

docker rmi <image-id>
# Remove image

docker system prune 
# Clean unused resources

docker build -t my-webapp:v1 .
# Build image from Dockerfile

docker tag my-webapp:v1 my-webapp:latest
# Tag image

docker history my-webbapp:v1
# Show image layers
```

## What Broke / What Confused Me
Nothing broke - but I want to remember: port mapping (`-p host:container`) is critical; if mapped incorrectly, the container runs but is not accessible from the browser.

## One-line Summary 
Docker packages applications into container using images and Dockerfiles to ensure consistent and portable execution across environments.

