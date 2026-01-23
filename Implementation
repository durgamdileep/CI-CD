# 🚀 CI/CD Implementation Using Jenkins, Docker, SonarQube & ArgoCD

## 📌 1. Overview

This setup follows modern DevOps best practices by separating:

- ⚙️ CI (Continuous Integration) → Jenkins
- 🔄 CD (Continuous Deployment) → ArgoCD (GitOps)

Flow summary:

- 🧑‍💻 Developer pushes code → Git
- 🪝 Webhook triggers Jenkins → CI pipeline runs
- 🏗️ Jenkins builds, tests, scans, and creates artifacts
- 🐳 Docker image is built and pushed to a registry
- ☸️ Kubernetes deployment manifests are updated in Git
- 🚀 ArgoCD detects changes and deploys to Kubernetes

## 🏗️ 2. Infrastructure Setup (AWS EC2)

### 🚀 2.1 Launch EC2 Instance

- 🐧 OS: Amazon Linux / Ubuntu

Open ports:

- 🔐 22 → SSH
- ⚙️ 8080 → Jenkins
- 🔍 9000 → SonarQube
- 🌐 80/443 → Application (optional)

### ☕ 2.2 Install Java
```
 sudo apt update
 sudo apt install openjdk-11-jdk -y

```

### 2.3 Install Jenkins
 ```
  curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
  
  echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
  
  sudo apt update
  sudo apt install jenkins -y
  sudo systemctl start jenkins
  sudo systemctl enable jenkins

```
- Access Jenkins:
  ``` http://<EC2-IP>:8080 ```

### 2.4 Install Docker
```  
  sudo apt install docker.io -y
  sudo systemctl start docker
  sudo systemctl enable docker
```
- Give Docker access to Jenkins
``` 
  sudo usermod -aG docker jenkins
  sudo systemctl restart jenkins
```


## ⚙️ 3. Jenkins Configuration

### 🔓 3.1 Initial Setup

- 🔑 Unlock Jenkins
- 👤 Create Admin User
- 🧩 Install suggested plugins

### 🧩 3.2 Required Plugins

- 🐳 Docker Pipeline
- 🌿 Git
- 🧱 Pipeline
- 🔍 SonarQube Scanner
- 📢 Slack / Email Notification (optional)

## 🧪 4. CI Pipeline Using Jenkinsfile

### 📄 4.1 Jenkinsfile Location

- 📂 Stored in SCM (Git repository) or
- ✍️ Written in Groovy

### 🐳 4.2 Docker as Jenkins Agent

- 🤖 Jenkins uses Docker agent
- 📦 Maven Docker image (specific version) is used
- ♻️ If image exists → reuse
- ⬇️ If not → pull image and create container
- 📦 Pipeline runs inside container

## 🏗️ 5. CI Pipeline Stages

### 📥 5.1 Checkout Stage

- 🌿 Jenkins pulls latest code from Git

### 🛠️ 5.2 Build & Unit Test

- 🏗️ Compile code
- 🧪 Run unit tests
- ❌ Fail pipeline if tests fail

### 🔍 5.3 Static Code Analysis

- 🔎 Analyze source code
- 🐞 Detect bugs, code smells, security issues

### 🛡️ 5.4 Code Quality & Vulnerability Check

- 🔍 SonarQube used for:
  - 📊 Code quality
  - 🔐 Security hotspots
  - 📈 Coverage
- 🧰 (Optional) Use tools like:
  - 🛡️ Trivy
  - 🔎 OWASP Dependency Check
  - 🧪 Snyk (for vulnerabilities)

### 📊 5.5 Reports & Artifacts

- 📄 Generate reports
- 📦 Create artifacts:
  - 📁 JAR / WAR
- 🗄️ Store artifacts in Jenkins or Nexus/Artifactory

### 🐳 5.6 Docker Image Creation

- 🏗️ Build Docker image using Dockerfile
- 🏷️ Tag image with version or commit ID
- 📤 Push image to:
  - 🐳 Docker Hub
  - ☁️ AWS ECR
  - 📦 Other container registry

### 📢 5.7 Notifications

- ❌ On failure:
  - 💬 Slack
  - 📧 Email
- ✅ On success:
  - 🎉 Optional success notification

## 🔎 6. SonarQube Integration

### 🖥️ 6.1 Install SonarQube (on EC2)

- 🌐 Runs on port 9000

### 👤 6.2 SonarQube Setup

- 👤 Create SonarQube account
- 🔑 Generate authentication token

### 🔐 6.3 Jenkins Integration

- 🔐 Store token in Jenkins:
  - ⚙️ Manage Jenkins → Credentials
- 🧩 Configure SonarQube server in Jenkins
- 🔒 Jenkins connects securely using token

## 🔁 7. CI Trigger Mechanism

### 🪝 7.1 Webhooks

- 🌿 Git repository → Jenkins
- 🚫 Jenkins does NOT poll Git
- 🔔 Webhook triggers Jenkins on:
  - 🆕 New commit
  - 📤 New push
  - 🔀 PR (optional)

## 📦 8. CI Output

- 📌 At the end of CI:
  - ✔️ Code tested and analyzed
  - ✔️ Artifact created (JAR/WAR)
  - ✔️ Docker image pushed to registry
  - ❌ No deployment yet
- 👉 CI ends here.

## 🚀 9. CD Using ArgoCD (GitOps)

### 🤔 9.1 Why ArgoCD?

- ☸️ Best for Kubernetes
- 📜 Declarative
- 🔄 Automatic sync
- ⏪ Rollback support

### 📂 9.2 GitOps Flow

- 📁 Kubernetes manifests stored in Git:
  - 📄 deployment.yaml
  - 📄 service.yaml
- 🏷️ Image tag updated in manifest
- 📤 Commit pushed to Git

### 🔄 9.3 ArgoCD Behavior

- 👀 Continuously monitors Git repository
- 🔍 Detects changes in manifests
- ⬇️ Pulls latest Docker image from registry
- 🚀 Deploys application to Kubernetes Pods

⚠️ Note:

- 📂 ArgoCD pulls manifests from Git
- 🐳 Images are pulled from container registry

## 🔗 10. CI vs CD Relationship

| 🧰 Tool       | 📌 Responsibility                              |
|--------------|-----------------------------------------------|
| 🌿 Git        | Source of truth                                |
| ⚙️ Jenkins    | CI (build, test, scan, image build)            |
| 🐳 Docker     | Containerization                               |
| 🔍 SonarQube  | Code quality                                   |
| 📦 Registry   | Store images                                   |
| 🚀 ArgoCD     | CD (deploy to Kubernetes)                      |


## 🧾 11. Final Summary

- 🪝 Jenkins and Git communicate using webhooks
- 🤖 Jenkins runs CI using Docker agent
- 🔍 SonarQube handles code quality
- 📦 Artifacts and Docker images are created
- 🚀 ArgoCD handles deployment using GitOps
- 🚫 Jenkins does not deploy to Kubernetes directly
- 🌿 Git is the single source of truth


