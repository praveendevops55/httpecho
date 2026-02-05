📌 **Project Overview**

This project implements a complete CI/CD pipeline with GitOps to deploy the hashicorp/http-echo application on a Kubernetes cluster (AKS) using:

GitHub Actions for CI

Azure Container Registry (ACR) for images

Kubernetes (AKS) for runtime

ArgoCD for GitOps-based CD

The deployment is fully automated and Git-driven — no manual kubectl apply is required after setup

🏗 **Architecture Flow (High Level)**
Developer
   ↓
Git Push
   ↓
GitHub Actions (CI)
   ├── Build Docker Image
   ├── Tag with Commit SHA
   ├── Push to ACR
   └── Update Kubernetes Manifest (Git)
          ↓
        ArgoCD
          ↓
     AKS Cluster

**♻️ Rollback Strategy **
🔁 Rollback via Git (Primary)
git revert <commit-id>
git push


➡ ArgoCD auto-syncs
➡ Cluster rolls back safely

**🔁 Rollback via ArgoCD UI / CLI**
argocd app history http-echo
argocd app rollback http-echo <REVISION>


✔ Instant rollback
✔ No downtime
✔ Production safe
