# 🚀 DevOps CI/CD Pipeline on AWS with Terraform, EKS, Kubernetes, and ArgoCD

## 🎯 Objective

This project simulates a complete CI/CD infrastructure pipeline using AWS EKS, Terraform, Kubernetes, and ArgoCD. It includes Terraform code to provision an EKS cluster and Kubernetes manifests to deploy a sample NGINX application managed via ArgoCD.

---

## 🧰 Tech Stack

- **AWS** – Cloud provider for infrastructure
- **Terraform** – Infrastructure as Code (IaC)
- **EKS** – Managed Kubernetes Cluster
- **Kubernetes** – Container orchestration
- **ArgoCD** – GitOps CD tool
- **NGINX** – Sample application

---

## 📁 Project Structure

devops-assignment/
├── terraform/ # Terraform code for VPC, EKS, and IAM
├── manifests/ # Kubernetes manifests (Deployment + Service)
├── argocd/ # ArgoCD Application resource
└── README.md # Setup instructions and documentation



---

## ✅ Setup Instructions

### 1. 🚀 Provision EKS Cluster (using Terraform)

> Ensure AWS CLI and Terraform are configured.

```bash
cd terraform/
terraform init
terraform apply



2.  Update kubeconfig
aws eks --region ap-south-1 update-kubeconfig --name demo-eks-cluster


3.  Install ArgoCD on EKS
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml



4.  Access ArgoCD UI
Option 1 (Port Forward):
kubectl port-forward svc/argocd-server -n argocd 8080:443


Then access: https://localhost:8080

Option 2 (LoadBalancer):

Edit the argocd-server service:
kubectl edit svc argocd-server -n argocd
# Change type: ClusterIP → LoadBalancer


Then run:
kubectl get svc -n argocd
Look for EXTERNAL-IP to access the ArgoCD UI.


5.  ArgoCD Login
kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d
Username: admin

Password: (value from above command)



Deploy NGINX with ArgoCD
1. Create ArgoCD Application Resource
kubectl apply -f argocd/nginx-app.yaml


2. Sync the Application in ArgoCD UI
Go to Applications

Click on nginx-app

Hit "Sync" to deploy


