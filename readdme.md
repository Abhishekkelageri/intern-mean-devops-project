# 🚀 MEAN Stack DevOps CI/CD Project

## 📌 Project Overview

This project demonstrates a complete CI/CD pipeline implementation for a Dockerized MEAN (MongoDB, Express, Angular, Node.js) application.

The project includes:

- 🐳 Dockerized Backend (Node.js + Express)
- 🌐 Dockerized Frontend (Angular + Nginx)
- 📦 Docker Compose for container orchestration
- 🔁 GitHub Actions for CI/CD automation
- 🐋 DockerHub for image storage
- ☁ AWS EC2 (Ubuntu) for deployment
- 🔐 SSH-based automated deployment

---

# 🏗 Project Structure

```
intern-mean-devops-project/
│
├── backend/
│   └── Dockerfile
│
├── frontend/
│   └── Dockerfile
│
├── docker-compose.yml
│
└── .github/workflows/
    └── main.yml
```

---

# 🐳 Docker Configuration

## 🔹 Backend Dockerfile

Location:
```
backend/Dockerfile
```

Configuration:

- Base Image: node:20
- Working Directory: /app
- Installs dependencies using npm install
- Exposes port 8080
- Starts application using:

```
node server.js
```

---

## 🔹 Frontend Dockerfile (Multi-Stage Build)

Location:
```
frontend/Dockerfile
```

### Stage 1 – Build
- Base Image: node:20
- Installs dependencies
- Builds Angular app using:
  ```
  npm run build --prod
  ```

### Stage 2 – Production
- Base Image: nginx:alpine
- Copies Angular build files to:
  ```
  /usr/share/nginx/html
  ```
- Exposes port 80
- Runs Nginx in foreground

---

# 📦 Docker Compose Setup

File:
```
docker-compose.yml
```

## Services:

### Backend
- Image: abhiii2211/mean-backend:latest
- Port Mapping: 3000:3000

### Frontend
- Image: abhiii2211/mean-frontend:latest
- Port Mapping: 80:80

---

## ▶ Run Application Locally

Start:
```
docker-compose up -d
```

Stop:
```
docker-compose down
```

---

# 🔁 CI/CD Pipeline (GitHub Actions)

Workflow File:
```
.github/workflows/main.yml
```

## 🚀 Trigger
Pipeline runs automatically on:
```
push to main branch
```

## 🛠 Pipeline Steps

1. Checkout source code
2. Login to DockerHub using secrets
3. Build Backend Docker image
4. Build Frontend Docker image
5. Push Backend image to DockerHub
6. Push Frontend image to DockerHub
7. SSH into AWS EC2 VM
8. Pull latest images
9. Restart containers using Docker Compose

---

# 🔐 GitHub Secrets Used

- DOCKER_USERNAME
- DOCKER_PASSWORD
- VM_HOST
- VM_USER
- VM_SSH_KEY

These secrets ensure secure authentication for:
- DockerHub login
- SSH deployment to EC2

---

# ☁ Deployment Architecture

Infrastructure:

- AWS EC2 (Ubuntu)
- Docker Installed
- Docker Compose Installed
- Nginx serving Angular frontend
- Backend running as Docker container
- Images pulled from DockerHub

---

# 🚀 Deployment Commands (Executed via CI/CD)

On EC2 VM:

```
cd /root/mean-project/intern-mean-devops-project
docker-compose pull
docker-compose down
docker-compose up -d
```

This ensures:
- Latest images are pulled
- Old containers are stopped
- Updated containers are deployed

---

# 📸 Screenshots

## 🔹 CI/CD Pipeline Execution

![CI/CD Pipeline](screenshots/cicd.png)

## 🔹 Docker Image Build & Push

![Docker Build](screenshots/docker-build.png)

## 🔹 Application Running UI

![Application UI](screenshots/ui.png)

## 🔹 Nginx & Infrastructure Setup

![Infrastructure](screenshots/infrastructure.png)

(Replace screenshot names if your filenames are different.)

---

# 🎯 Final Outcome

✔ Fully Dockerized MEAN application  
✔ Automated CI/CD pipeline  
✔ Automatic Docker image build & push  
✔ Auto deployment to AWS EC2  
✔ Production-ready Nginx configuration  

---

# 👨‍💻 Author

Abhishek Kelageri
