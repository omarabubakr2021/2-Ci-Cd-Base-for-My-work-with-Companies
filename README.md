
## ⚙️ CI/CD Pipeline – Backend Deployment System

Welcome to the CI/CD pipeline powering a large-scale backend system, built with reliability, security, and automation in mind.

This GitHub Actions pipeline was designed to streamline the journey from source code → Docker image → production Kubernetes cluster with full traceability and zero manual steps.

---

## 🚀 Overview

This pipeline listens for pushes to the `main` branch and then:

1. Builds a Docker image of the backend service
2. Tags it using the commit hash for traceability
3. Pushes it to Docker Hub
4. Updates the Kubernetes deployment with the new image
5. Verifies successful rollout

---

## 🤖 Pipeline Diagram

```mermaid
graph TD
    A[Push to main] --> B[Checkout Code]
    B --> C[Extract Commit Hash]
    C --> D[Login to Docker Hub]
    D --> E[Set up Buildx]
    E --> F[Build & Push Docker Image]
    F --> G[Checkout Repo Again]
    G --> H[Decode Kubeconfig Secret]
    H --> I[Set K8s Context]
    I --> J[Set New Image on Deployment]
    J --> K[Verify Deployment Rollout]
    K --> L[Done ✅]
````

---

## ⚙️ Pipeline Stages

### 🔧 Build Job

| Step                  | Description                                |
| --------------------- | ------------------------------------------ |
| `Checkout`            | Pulls latest code from `main`              |
| `Extract Commit Hash` | Shortens commit SHA for clean tagging      |
| `Login to Docker Hub` | Auth via GitHub Secrets                    |
| `Docker Buildx`       | Enables fast, cache-aware builds           |
| `Build & Push`        | Image pushed to Docker Hub with commit tag |

---

### 🚀 Deploy Job

| Step             | Description                            |
| ---------------- | -------------------------------------- |
| `Checkout`       | Ensures repo is available              |
| `Kubeconfig`     | Decoded securely from base64 secret    |
| `Context Switch` | Targets the right cluster/context      |
| `Set Image`      | Updates deployment with new image      |
| `Rollout Check`  | Waits for Kubernetes to finish rollout |

---

## 🌟 Key Features

* 🔐 Secrets-driven, zero exposure pipeline
* 🔁 Reusable & modular design (Build + Deploy separated)
* 🧬 Commit-based versioning for traceability
* ⚡ Optimized Docker caching
* ☁️ Kubernetes-native integration
* ✅ Tested in high-scale production systems
