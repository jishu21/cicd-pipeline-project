# CI/CD Pipeline with GitHub Actions

Automated CI/CD pipeline that tests, builds a Docker image, pushes to DockerHub and deploys to AWS EKS automatically on every git push.

## 🏗️ Architecture
Developer pushes code to GitHub
↓
GitHub Actions triggers automatically
├── Job 1: Run Tests (Node.js)
├── Job 2: Build & Push Docker image to DockerHub
└── Job 3: Deploy to AWS EKS
↓
App running live on EKS cluster

## 🛠️ Tools & Technologies

| Category | Tool |
|---|---|
| CI/CD | GitHub Actions |
| Language | Node.js + Express |
| Containerization | Docker |
| Image Registry | DockerHub |
| Orchestration | AWS EKS |
| Deployment | kubectl |
| Cloud | AWS (EKS, IAM, VPC) |

## 📁 Project Structure
cicd-pipeline-project/
├── .github/
│   └── workflows/
│       └── cicd.yaml      # GitHub Actions pipeline
├── app.js                 # Node.js application
├── Dockerfile             # Container configuration
├── deployment.yaml        # Kubernetes deployment
├── service.yaml           # Kubernetes service
├── package.json           # Node dependencies
└── README.md              # This file

## 🚀 Pipeline Stages

### Stage 1 — Test
- Checks out code
- Sets up Node.js 18
- Installs dependencies
- Runs automated tests

### Stage 2 — Build & Push
- Builds Docker image
- Tags with commit SHA and latest
- Pushes to DockerHub

### Stage 3 — Deploy
- Configures AWS credentials
- Updates kubeconfig for EKS
- Creates cicd namespace
- Applies Kubernetes manifests
- Updates deployment with new image
- Verifies rollout status

## ✅ Features

- **Fully automated** — triggers on every push to main
- **Sequential jobs** — deploy only runs if tests and build pass
- **Image tagging** — each build tagged with commit SHA for traceability
- **Health checks** — liveness and readiness probes configured
- **Resource limits** — CPU and memory limits set for pods
- **Secure** — credentials stored as GitHub secrets

## 🔐 GitHub Secrets Required

| Secret | Purpose |
|---|---|
| `DOCKERHUB_USERNAME` | DockerHub login |
| `DOCKERHUB_TOKEN` | DockerHub authentication |
| `AWS_ACCESS_KEY_ID` | AWS authentication |
| `AWS_SECRET_ACCESS_KEY` | AWS authentication |

## 🐳 Docker Image
docker pull jiteshwar0124/cicd-pipeline-app:latest

## 📡 API Endpoints

| Endpoint | Response |
|---|---|
| `GET /` | App info and version |
| `GET /health` | Health check status |

## 🐛 Real-World Issues Solved

- EKS authentication mode updated to API_AND_CONFIG_MAP for IAM user access
- GitHub Actions IAM user granted EKS cluster admin access via access entries
- DockerHub token scope configured for read/write access

## 📚 Learnings

- How GitHub Actions workflows trigger automatically on git push
- How Docker images are built and tagged with commit SHAs for traceability
- How Kubernetes rolling updates work during deployment
- How to securely store credentials using GitHub secrets
- How IAM users authenticate to EKS using access entries
