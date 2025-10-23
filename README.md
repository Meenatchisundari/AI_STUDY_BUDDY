# AI STUDY BUDDY — Intelligent Learning Assistant (GitOps)

An advanced AI-powered study companion that helps students learn effectively through intelligent question generation, personalized study plans, and interactive learning sessions. Built with LLMOps best practices, featuring automated GitOps deployment through Jenkins, ArgoCD, and Kubernetes — combining AI-driven education, automation, and cloud-native architecture into one complete pipeline.

---

## Table of Contents

- [Features](#features)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [GitOps CI/CD Pipeline](#gitops-cicd-pipeline)
- [Technologies Used](#technologies-used)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)
- [Future Enhancements](#future-enhancements)
- [Acknowledgments](#acknowledgments)

---

## Features

- **AI-Powered Question Generation**: Automatically generates practice questions from study materials  
- **Personalized Learning Paths**: Adapts to individual learning styles and pace  
- **Interactive Study Sessions**: Real-time Q&A with intelligent feedback  
- **Progress Tracking**: Visual dashboards to monitor learning progress  
- **Multi-Subject Support**: Covers various academic subjects and topics  
- **GitOps Automation**: Fully automated CI/CD pipeline with Jenkins and ArgoCD  
- **Kubernetes Orchestration**: Cloud-native deployment with auto-scaling  
- **Security Scanning**: Integrated Trivy vulnerability scanning  
- **Webhook Integration**: Auto-deployment on every GitHub push  
- **High Availability**: Deployed on GCP with Minikube cluster management

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                    DEVELOPMENT AND SETUP                            │
│  ┌──────────┐  ┌──────────────┐  ┌─────────────────┐                │
│  │ Project  │  │ Configuration│  │   Question      │                │
│  │ and API  │→ │    Code      │→ │   Schemas       │                │
│  │  Setup   │  │              │  │  Models Code    │                │
│  └──────────┘  └──────────────┘  └─────────────────┘                │
│       ↓               ↓                    ↓                        │
│  ┌──────────┐  ┌──────────────┐  ┌─────────────────┐                │
│  │ Prompt   │  │  Groq Client │  │   Question      │                │
│  │Templates │→ │ Setup Code   │→ │  Generator      │                │
│  │  Code    │  │              │  │     Code        │                │
│  └──────────┘  └──────────────┘  └─────────────────┘                │
│       ↓               ↓                    ↓                        │
│  ┌──────────────────────────────────────────────┐                   │
│  │         Helper Class Codes                   │                   │
│  └──────────────────────────────────────────────┘                   │
└─────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────┐
│                         APPLICATION                                 │
│  ┌────────────────────────────────────────────────┐                 │
│  │          Main Application                      │                 │
│  │  (Streamlit UI + LLM Integration)              │                 │
│  └────────────────────────────────────────────────┘                 │
└─────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────┐
│              VERSIONING AND CONTAINERIZATION                        │
│  ┌──────────────────┐         ┌──────────────────┐                  │
│  │ Code Versioning  │    →    │   Dockerfile     │                  │
│  │   (GitHub)       │         │                  │                  │
│  └──────────────────┘         └──────────────────┘                  │
└─────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────┐
│            INFRASTRUCTURE AND DEPLOYMENT                            │
│  ┌──────────────────┐         ┌──────────────────┐                  │
│  │   Kubernetes     │    →    │   GCP VM         │                  │
│  │ Manifests Files  │         │ Instance Setup   │                  │
│  └──────────────────┘         └──────────────────┘                  │
└─────────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────────┐
│                      CI/CD PIPELINE                                 │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐             │
│  │ Jenkins  │→ │  GitHub  │→ │  Build   │→ │  ArgoCD  │             │
│  │  Setup   │  │Integration│ │  & Push  │  │  Setup   │             │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘             │
│       ↓              ↓             ↓              ↓                 │
│  Automated    Version      Docker        Continuous                 │
│   Testing     Control      Image         Deployment                 │
│                           to DockerHub                              │
│       ↓              ↓             ↓              ↓                 │
│  ┌────────────────────────────────────────────────────┐             │
│  │          WebHooks (GitHub Auto-trigger)            │             │
│  └────────────────────────────────────────────────────┘             │
└─────────────────────────────────────────────────────────────────────┘
                              ↓
                    ┌──────────────────┐
                    │   Production     │
                    │   Kubernetes     │
                    │    Cluster       │
                    └──────────────────┘
```

---

## Prerequisites

### Required Software

- **Python 3.8+**
- **Git**
- **Docker Desktop**
- **Google Cloud Platform Account**
- **kubectl**
- **Minikube**

### Required Accounts & Credentials

- **GitHub** (for version control + Jenkins integration)
- **DockerHub** (for container registry)
- **GCP Account** (for VM instance and deployment)
- **Groq API Key** (for LLM integration)

### Local Development

- Python virtual environment
- Code editor (VS Code recommended)
- Terminal/Command Line access

---

## Installation

### Step 1: Clone the Repository

```bash
git clone https://github.com/meenatchisundari/AI_STUDY_BUDDY.git
cd AI-STUDY-BUDDY
```

### Step 2: Create Virtual Environment

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Set Up Environment Variables

Create a `.env` file in the root directory:

```env
GROQ_API_KEY=your_groq_api_key_here
```

### Step 5: Run Locally

```bash
streamlit run app.py
```

Access the application at: `http://localhost:8501`

---

## Project Structure

```
AI-STUDY-BUDDY/
│
├── app/                      # Main application code
│   ├── main.py              # Streamlit UI
│   ├── question_generator.py
│   ├── groq_client.py
│   └── helpers.py
│
├── manifests/               # Kubernetes deployment files
│   ├── deployment.yaml
│   ├── service.yaml
│   └── configmap.yaml
│
├── Dockerfile               # Container configuration
├── Jenkinsfile             # CI/CD pipeline definition
├── requirements.txt        # Python dependencies
├── setup.py               # Setup configuration
├── .gitignore             # Ignored files
└── README.md              # This file
```

---

## GitOps CI/CD Pipeline

The complete GitOps pipeline automates the entire deployment workflow from code commit to production.

### Pipeline Stages

1. **Code Checkout** → Jenkins pulls latest code from GitHub
2. **Build Docker Image** → Creates containerized application
3. **Push to DockerHub** → Uploads image to container registry
4. **Install kubectl & ArgoCD CLI** → Prepares deployment tools
5. **Apply Kubernetes Manifests** → Deploys to cluster
6. **Sync with ArgoCD** → Ensures desired state matches actual state

### Setup Instructions

#### 1. GCP VM Instance Setup

```bash
# Create VM on Google Cloud Platform
Name: gitops
Machine Type: E2 Standard (16 GB RAM)
Boot Disk: Ubuntu 24.04 LTS (256 GB)
Networking: Enable HTTP and HTTPS traffic
```

#### 2. Install Docker on VM

```bash
# Follow official Docker installation guide
# Enable Docker without sudo
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

#### 3. Install Minikube

```bash
# Install Minikube binary
minikube start
kubectl cluster-info
```

#### 4. Jenkins Setup (Docker-in-Docker)

```bash
docker run -d --name jenkins \
  -p 8080:8080 \
  -p 50000:50000 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v $(which docker):/usr/bin/docker \
  -u root \
  -e DOCKER_GID=$(getent group docker | cut -d: -f3) \
  --network minikube \
  jenkins/jenkins:lts
```

Access Jenkins at: `http://<VM_EXTERNAL_IP>:8080`

#### 5. Configure Jenkins Credentials

Add the following credentials in Jenkins:

- **GitHub Token** (`github-token`)
- **DockerHub Token** (`gitops-dockerhub`)
- **Kubeconfig** (`kubeconfig` - secret file)

#### 6. Install ArgoCD

```bash
# Create namespace
kubectl create ns argocd

# Install ArgoCD
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Change service to NodePort
kubectl edit svc argocd-server -n argocd
# Change type: ClusterIP to type: NodePort

# Get admin password
kubectl get secret -n argocd argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

Access ArgoCD at: `http://<VM_EXTERNAL_IP>:31704`

#### 7. Connect GitHub to ArgoCD

- Go to ArgoCD UI → Settings → Repositories → Connect Repo
- Add your GitHub repository with credentials
- Create new application pointing to `manifests/` directory

#### 8. Create Kubernetes Secret for Groq API

```bash
kubectl create secret generic groq-api-secret \
  --from-literal=GROQ_API_KEY="your_api_key_here" \
  -n argocd
```

#### 9. Configure GitHub Webhook

- Go to GitHub Repository → Settings → Webhooks → Add webhook
- **Payload URL**: `http://<JENKINS_IP>:8080/github-webhook/`
- **Content type**: `application/json`
- **Events**: Just the push event

#### 10. Enable Jenkins Auto-trigger

- Go to Jenkins → Pipeline → Configure
- Enable: **GitHub hook trigger for GITScm polling**

---

## Technologies Used

| Category | Tools |
|----------|-------|
| **AI & NLP** | Groq API • LangChain • Streamlit |
| **DevOps** | Jenkins • Docker • Kubernetes • ArgoCD |
| **Cloud** | Google Cloud Platform (GCP) |
| **Orchestration** | Minikube • kubectl |
| **Version Control** | Git • GitHub |
| **Container Registry** | DockerHub |
| **CI/CD** | Jenkins Pipeline • GitHub Webhooks |
| **GitOps** | ArgoCD (Continuous Deployment) |
| **Language** | Python 3.8+ |

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Jenkins not loading | Ensure Docker is running and port 8080 is free |
| Minikube not starting | Check Docker is installed and running |
| ArgoCD login fails | Verify admin password and ensure port-forward is active |
| Docker build fails | Check Dockerfile syntax and dependencies |
| Kubernetes pods not running | Check logs with `kubectl logs <pod-name> -n argocd` |
| Webhook not triggering | Verify Jenkins firewall rules and webhook URL |
| Port-forward disconnects | Run in separate terminal with `nohup` or `screen` |

---

## Contributing

Contributions are welcome! To add features:

```bash
git checkout -b feature/new-feature
git commit -m "Add new feature"
git push origin feature/new-feature
```

Then open a Pull Request.

### Guidelines:

- Follow PEP 8 style guide
- Add unit tests for new modules
- Ensure CI/CD pipeline passes before merging
- Update documentation for new features

---

## License

This project is licensed under the **MIT License** — see [LICENSE](LICENSE) for details.

---

## Contact

**Meenatchi Sundari**  
[Linkedin](https://linkedin.com/in/meenatchisundari)

---

## Future Enhancements

- **Multi-language Support**: Support for multiple languages
- **Gamification**: Add points, badges, and leaderboards
- **Advanced Analytics**: Detailed learning insights and recommendations
- **Voice Integration**: Voice-based question answering
- **Mobile App**: Native iOS and Android applications
- **Collaborative Learning**: Study groups and peer learning features
- **Custom Themes**: Personalized UI themes
- **OAuth Integration**: Social login support
- **A/B Testing**: Experiment with different learning strategies
- **CDN Integration**: Faster global content delivery

---

## Acknowledgments

- **Groq** for high-performance LLM API
- **Jenkins** for CI/CD automation
- **ArgoCD** for GitOps continuous delivery
- **Kubernetes** for container orchestration
- **Google Cloud Platform** for cloud infrastructure
- **Streamlit** for rapid UI development
- **Open-Source Community** for amazing tools and libraries

---

## Architecture Highlights

### GitOps Workflow

```
Developer Push → GitHub → Jenkins Webhook → Build & Test → 
Docker Build → Push to DockerHub → Update Manifests → 
ArgoCD Sync → Kubernetes Deployment → Production
```

### Security Features

- Secret management with Kubernetes secrets
- API key encryption
- Container vulnerability scanning (optional: Trivy integration)
- Private container registry support
- RBAC (Role-Based Access Control) with ArgoCD

### High Availability

- Auto-scaling with Kubernetes
- Self-healing deployments
- Rolling updates with zero downtime
- Health checks and liveness probes

---

## Quick Start Commands

```bash
# Clone and setup
git clone https://github.com/yourusername/AI-STUDY-BUDDY.git
cd AI-STUDY-BUDDY
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt

# Run locally
streamlit run app.py

# Build Docker image
docker build -t ai-study-buddy:latest .

# Deploy to Kubernetes
kubectl apply -f manifests/

# Check deployment status
kubectl get pods -n argocd
kubectl get svc -n argocd
```

---

**If you found this project useful, give it a star!**

---

