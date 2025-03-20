# Kubernetes
# React E-Commerce App - Kubernetes Deployment

This repository contains the Kubernetes deployment setup for a **React-based e-commerce application**. The deployment uses **Minikube, Docker, and Kubernetes** to containerize and manage the application.

---

## 🚀 Prerequisites
Before proceeding, ensure you have the following installed:

- [Docker](https://docs.docker.com/get-docker/)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- [Git](https://git-scm.com/)

---

## 📌 Setup Guide

### **Step 1: Clone the Repository**
```bash
git clone <your-repo-url>
cd <your-repo-folder>
```

### **Step 2: Build the Docker Image**
```bash
docker build -t e-commerce-app .
```

### **Step 3: Start Minikube**
```bash
minikube start --force
minikube status
```

### **Step 4: Load the Docker Image into Minikube**
```bash
minikube image load e-commerce-app
```
Verify the image is loaded:
```bash
minikube image list  # Ensure "e-commerce-app" is listed
```

### **Step 5: Deploy the Application**
```bash
kubectl apply -f deployment.yml
kubectl get deployments
kubectl get pods
```

If you need a **NodePort service**, apply it:
```bash
kubectl apply -f Nodeport.yaml
```

### **Step 6: Fix Image Pull Issues (if necessary)**
If Kubernetes tries to pull the image from a registry instead of using the local image, patch the deployment:
```bash
kubectl patch deployment react-ecommerce-deployment --type='json' -p='[{"op": "replace", "path": "/spec/template/spec/containers/0/imagePullPolicy", "value": "Never"}]'
```
Alternatively, manually run a pod:
```bash
kubectl run react-ecommerce --image=e-commerce-app --image-pull-policy=Never --port=80
kubectl expose pod react-ecommerce --type=NodePort --port=80
```
Check services:
```bash
kubectl get svc
```

### **Step 7: Expose the Service & Access the App**
```bash
minikube ip
minikube service react-ecommerce-service
```

---

## 📤 Push to GitHub
```bash
git init  # If not already initialized
git add Dockerfile deployment.yml Nodeport.yaml
git commit -m "Kubernetes deployment for React e-commerce app"
git remote add origin <your-repo-url>
git branch -M main
git push -u origin main
```
