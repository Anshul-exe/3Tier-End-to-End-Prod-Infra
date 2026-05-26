# Three Tier End-to-End Production Infrastructure

Production-grade, three-tier application deployed on AWS EKS with ALB Ingress and private ECR images.

## Highlights
- EKS cluster with managed node group
- ALB Ingress (TLS) routing `/` to frontend and `/api` to backend
- MongoDB running in-cluster with PVC
- Dockerized React + Node/Express services

## Tech Stack
**Frontend:** React 17  
**Backend:** Node.js 14, Express, Mongoose  
**Database:** MongoDB 4.4.6  
**Infra:** Kubernetes (EKS), ALB, ECR, ACM, IAM, VPC (eksctl)  

## Repository Layout
- `frontend/` React UI
- `backend/` Express API
- `manifests/` Kubernetes resources (Ingress, Deployments, Services, PV/PVC, Secrets)

## Live Environment (Observed)
- **Cluster:** `three-tier-cluster` (ap-south-1)
- **Ingress Host:** `assignment.anshulfml.me`
- **ALB:** internet-facing, TLS-enabled
- **ECR:** `three-tier-lab-frontend`, `three-tier-lab-backend`

## Local Run (Quick Start)
```
docker run -d -p 27017:27017 --name mongo mongo:4.4.6

cd backend && npm install
export MONGO_CONN_STR="mongodb://localhost:27017/todo"
node index.js

cd ../frontend && npm install
export REACT_APP_BACKEND_URL="http://localhost:3500/api/tasks"
npm start
```

## Cloud Deploy (Summary)
1. Build & push images to ECR.
2. Apply manifests in `manifests/` to the `three-tier` namespace.
3. ALB is created by AWS Load Balancer Controller.

## Architecture Placeholders
- **Kubernetes Resource Relationship Diagram:** _subah add krdenge diagram_
- **Request Flow Diagram:** _subah add krdenge diagram_
- **Deployment Workflow Diagram:** _subah add krdenge diagram_
