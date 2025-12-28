# Bare Metal Kubernetes (Home Lab Setup)

This repository contains **all Kubernetes manifests and configurations** that I used to set up a **production-like Kubernetes cluster on bare metal servers / virtual machines (Home Lab)**.

The goal of this project is to **demonstrate real-world Kubernetes concepts** such as cluster setup, deployments, services, ingress, storage, and autoscaling — without using managed cloud services.

This project is also documented in detail in my **Medium blog**, where I explain each step practically.

---

## 🚀 Project Overview

- Kubernetes cluster installed on **bare metal / VMs**
- 3-tier application architecture
  - **Frontend**: React
  - **Backend**: Node.js
  - **Database**: MySQL (StatefulSet)
- **Horizontal Pod Autoscaler (HPA)** for frontend and backend
- **Ingress Controller** for external access
- **MetalLB** for LoadBalancer support on bare metal
- Designed for **learning, interviews, and DevOps portfolio**

---

## 🏗 Architecture

```
User
  |
  v
Ingress Controller
  |
Frontend (React)
  |
Backend (Node.js)
  |
MySQL (StatefulSet + PVC)
```

---

## 📁 Repository Structure

```
bare-metal-kubernetes/
│
├── hpa-deployment/
│   ├── frontend-app.yaml        # Frontend Deployment + Service
│   ├── backend-app.yaml         # Backend Deployment + Service
│   ├── frontend-hpa.yaml        # HPA for Frontend
│   ├── backend-hpa.yaml         # HPA for Backend
│   ├── mysql-statefulset.yaml   # MySQL StatefulSet
│   ├── mysql-service.yaml       # MySQL Service
│
├── frontend.yaml                # Standalone frontend manifest
├── backend.yaml                 # Standalone backend manifest
├── mysql.yaml                   # MySQL resources (combined)
├── ingress.yaml                 # Ingress configuration
├── metallb-12.yaml              # MetalLB configuration
│
└── README.md
```

---

## ⚙️ Prerequisites

- Linux-based VMs or bare metal servers
- Kubernetes cluster (kubeadm based)
- kubectl configured
- Metrics Server installed (required for HPA)
- MetalLB installed for LoadBalancer support

---

## 📦 Deployment Steps

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/AAKASHDEEP786/bare-metal-kubernetes.git
cd bare-metal-kubernetes
```

### 2️⃣ Deploy MySQL (Stateful Application)

```bash
kubectl apply -f hpa-deployment/mysql-statefulset.yaml
kubectl apply -f hpa-deployment/mysql-service.yaml
```

### 3️⃣ Deploy Backend and Frontend

```bash
kubectl apply -f hpa-deployment/backend-app.yaml
kubectl apply -f hpa-deployment/frontend-app.yaml
```

### 4️⃣ Deploy Ingress

```bash
kubectl apply -f ingress.yaml
```

### 5️⃣ Configure Autoscaling (HPA)

```bash
kubectl apply -f hpa-deployment/backend-hpa.yaml
kubectl apply -f hpa-deployment/frontend-hpa.yaml
```

---

## 📊 Load Testing (HPA Validation)

Example load test using BusyBox:

```bash
kubectl run fe-load --image=busybox --rm -it --restart=Never -- /bin/sh
```

Inside the pod:

```sh
while true; do wget -q -O- http://frontend-service; done
```

Watch scaling in real-time:

```bash
kubectl get pods -l app=frontend -w
kubectl get pods -l app=backend -w
```

---

## 📈 What This Project Demonstrates

- Bare metal Kubernetes setup
- Real-world Kubernetes manifests
- Difference between Deployment and StatefulSet
- CPU-based Horizontal Pod Autoscaling
- Storage handling using PVCs
- Ingress & LoadBalancer on bare metal

---

## 🧠 Learning Outcomes

- How Kubernetes works without cloud providers
- How autoscaling behaves under load
- How production-like architecture is designed
- How to structure Kubernetes manifests properly

---

## ✍️ Author

**Aakash Deep**  
DevOps Engineer | Kubernetes | Cloud | CI/CD  

- GitHub: https://github.com/AAKASHDEEP786
- Medium: (Add your Medium blog link here)

---

## ⭐ Support

If this repository helped you:
- Star ⭐ the repo
- Fork 🍴 it
- Share it with others

Happy Learning 🚀

