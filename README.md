#  Fusionpact DevOps Gauntlet — Solution by Shiva Eduru

![CI Status](https://github.com/eduru-shiva/fusionpact-devops-challenge/actions/workflows/ci-cd.yml/badge.svg)

**Candidate:** Eduru Shiva Shankar Prasad  
**Position:** DevOps Intern  
**Date:** October 2025  

---

##  Project Overview

This repository contains my completed solution for the **Fusionpact DevOps Gauntlet Challenge**.  
The project demonstrates **containerization, observability, and CI/CD automation** using Docker, Prometheus, Grafana, and GitHub Actions — all deployed on an AWS EC2 instance.

---

## ☁️ Level 1 — Cloud Deployment (30%)

**Objective:** Deploy the full stack on the cloud using Docker and docker-compose.

**Steps Performed**
- Created Dockerfiles for both **frontend** and **backend**.
- Configured `docker-compose.yml` to orchestrate services.
- Ensured data persistence using Docker volumes.
- Deployed the stack on **AWS EC2 (Ubuntu)** instance.
- Verified both frontend and backend are publicly accessible.

**Public URLs**
- **Frontend:** http://52.66.249.177  
- **Backend:** http://52.66.249.177:8000/docs  

**Key Files**
- `frontend/Dockerfile`  
- `backend/Dockerfile`  
- `docker-compose.yml`  

---

##  Level 2 — Monitoring & Observability (30%)

**Objective:** Enable full observability using Prometheus and Grafana.

**Steps Performed**
- Configured **Prometheus** to scrape metrics from the backend at `/metrics`.
- Deployed **Grafana** via Docker to visualize real-time data.
- Created dashboards for:
  - **Infrastructure Metrics:** CPU, memory, disk, container usage.
  - **Application Metrics:** Request rate, latency, error counts.
- Tested alerting rules for backend memory usage in Grafana.

**Services**
- **Prometheus:** http://52.66.249.177:9090  
- **Grafana:** http://52.66.249.177:3000 (Login → admin / admin)

**Config File**
- `/prometheus/prometheus.yml` — defines scraping targets.

---

##  Level 3 — CI/CD Automation (30%)

**Objective:** Implement continuous integration and continuous deployment using GitHub Actions.

**Workflow Summary**
- On every push to the **main** branch:
  - Code checkout  
  - Build Docker images for frontend and backend  
  - Push images to Docker Hub  
  - SSH into EC2 and redeploy updated containers  

**Secrets Configured in GitHub**
- `DOCKER_USERNAME` — Docker Hub username  
- `DOCKER_PASSWORD` — Docker Hub access token  
- `EC2_HOST` — EC2 public IP  
- `EC2_SSH_KEY` — private SSH key for deployment  

**Key File**
- `.github/workflows/ci-cd.yml`  

---

##  Data Persistence

- Backend uses a volume mount:  
  `./backend/app/data:/app/data`  
  → Ensures data remains intact even if the container restarts.
- Prometheus and Grafana use named volumes (`prometheus-data`, `grafana-data`) to retain metrics and dashboards.

---

##  Commands Used

```bash
# SSH into EC2
ssh -i llm-portlal.key.pem ubuntu@52.66.249.177

# list files
ls

# Creating the directories and changing to dir
mkdir and cd


# Navigate to project folder
cd /home/ubuntu/fusionpact-devops-challenge

# Start containers (build + run)
docker-compose up -d --build

# Checking logs
 docker logs -f backend 
 docker logs -f frontend

# Verify containers
docker ps
