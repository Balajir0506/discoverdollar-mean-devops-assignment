# Discover Dollar – DevOps Internship Assignment

## Project Overview

This project demonstrates the containerization, CI/CD setup, and cloud deployment of a full-stack MEAN (MongoDB, Express, Angular, Node.js) application.

The application is deployed on an AWS EC2 Ubuntu instance using Docker Compose.  
CI/CD is implemented using GitHub Actions.  
Nginx is configured as a reverse proxy and the application is accessible via Port 80.


---

### Step 1: Repository Setup

- Created a new GitHub repository.
- Extracted the provided `crud-dd-task-mean-app.zip`.
- Pushed both `backend` and `frontend` folders to GitHub.
- Added a structured `README.md` file.

This repository is the source of truth for the application and triggers the CI/CD pipeline.

---

### Step 2: Backend Containerization

- Created a `Dockerfile` inside the backend folder.
- Used Node.js base image.
- Installed dependencies using `npm install`.
- Exposed backend port.
- Configured the container to run the server using `node server.js`.

This ensures the backend runs inside a Docker container instead of directly on the VM.

---

### Step 3: Frontend Containerization

- Created a multi-stage Dockerfile inside the frontend folder.
- Used Node.js image to build the Angular project.
- Generated production build.
- Used Nginx image to serve the built files.
- Exposed port 80.

This allows the Angular application to be served efficiently in production mode.

---

### Step 4: Docker Compose Setup

Created a `docker-compose.yml` file to manage all services together.

Services included:

- Backend
- Frontend
- MongoDB (official Docker image)
- Nginx (reverse proxy)

Docker Compose allows all containers to run together using a single command.

To start all services:

```bash
docker-compose up -d
```

To stop services:

```bash
docker-compose down
```

---

### Step 5: MongoDB Setup

Instead of installing MongoDB directly on the VM, the official MongoDB Docker image was used.

Advantages:
- Easy setup
- No manual installation required
- Portable and consistent environment

MongoDB runs as a container and is connected to the backend using Docker networking.

---

### Step 6: AWS EC2 Setup

- Launched an Ubuntu EC2 instance.
- Installed Docker.
- Installed Docker Compose.
- Opened Port 80 in the security group.
- Cloned the repository on the VM.

This VM acts as the production deployment server.

---

### Step 7: Manual Deployment on EC2

Initially, the application was tested manually by:

1. Pulling Docker images.
2. Running:

```bash
docker-compose up -d
```

3. Accessing the application via:

```
http://3.110.46.30
```

The application was verified to be working correctly.

---

### Step 8: Docker Hub Setup

- Created a Docker Hub account.
- Built backend and frontend images locally.
- Tagged images with Docker Hub username.
- Pushed images to Docker Hub.

This allows the EC2 server to pull updated images during deployment.

---

### Step 9: GitHub Secrets Configuration

The following secrets were added in GitHub:

- DOCKER_USERNAME
- DOCKER_PASSWORD
- EC2_HOST
- EC2_USER
- EC2_KEY

These are securely used inside the CI/CD workflow.

---

### Step 10: CI/CD Pipeline (GitHub Actions)

Created workflow file:

.github/workflows/deploy.yml

Pipeline flow:

1. Trigger on push to main branch.
2. Login to Docker Hub.
3. Build backend image.
4. Push backend image.
5. Build frontend image.
6. Push frontend image.
7. SSH into EC2 instance.
8. Pull latest images.
9. Restart containers using Docker Compose.

This ensures automatic deployment whenever code changes are pushed.

---

### Step 11: Nginx Reverse Proxy Configuration

Nginx is configured to:

- Listen on port 80.
- Serve frontend application.
- Forward API requests to backend container.

This makes the entire application accessible via a single public port.

The application is accessible at:

http://3.110.46.30

---

### How the Complete Flow Works

1. Developer pushes code to GitHub.
2. GitHub Actions builds and pushes Docker images.
3. EC2 pulls the latest images automatically.
4. Containers are restarted.
5. Updated application becomes live.

This setup provides automated build and deployment with minimal manual intervention.

---

### Infrastructure Status

The EC2 instance is not deleted and can be restarted for demonstration if required.
Containers can be brought up again using:

```bash
docker-compose up -d
```

---
## Screenshots are added in the screenshots folder 