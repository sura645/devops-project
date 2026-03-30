# 🚀 Node.js App CI/CD Pipeline using Docker & GitHub Actions

## 📌 Project Overview

This project demonstrates a complete **CI/CD pipeline** for a simple Node.js application using:

* 🟢 Node.js (HTTP Server)
* 🐳 Docker (Containerization)
* 🔁 GitHub Actions (CI/CD Automation)
* 📦 Docker Hub (Image Registry)

Whenever code is pushed to the `main` branch, the pipeline automatically:

1. Builds a Docker image
2. Pushes the image to Docker Hub

---

## 🏗️ CI/CD Workflow Architecture

```text
Developer → GitHub → GitHub Actions → Docker Build → Docker Hub
```

---

## ⚙️ Tech Stack

* Node.js
* Docker
* GitHub Actions
* Docker Hub

---

## 📁 Project Structure

```text
.
├── server.js
├── Dockerfile
├── .github/
│   └── workflows/
│       └── ci-cd.yml
└── README.md
```

---

## 🧑‍💻 Application Code

### server.js

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    res.write("Hello to DevOps World 🚀");
    res.end();
});

server.listen(3000, () => {
    console.log("Server running on port 3000");
});
```

---

## 🐳 Docker Configuration

### Dockerfile

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY . .

EXPOSE 3000

CMD ["node", "server.js"]
```

---

## 🔁 GitHub Actions CI/CD Pipeline

### Workflow: `.github/workflows/ci-cd.yml`

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  docker:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Code
      uses: actions/checkout@v3

    - name: Login to Docker Hub
      uses: docker/login-action@v2
      with:
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}

    - name: Build Docker Image
      run: docker build -t ${{ secrets.DOCKER_USERNAME }}/devops-app:latest .

    - name: Push Docker Image
      run: docker push ${{ secrets.DOCKER_USERNAME }}/devops-app:latest
```

---

## 🔐 GitHub Secrets Setup

Add the following secrets in your GitHub repository:

* `DOCKER_USERNAME`
* `DOCKER_PASSWORD`

📍 Path:
**Repository → Settings → Secrets → Actions**

---

## ▶️ How to Run Locally

### 1. Clone the repository

```bash
git clone https://github.com/your-username/devops-project.git
cd devops-project
```

---

### 2. Build Docker Image

```bash
docker build -t devops-app .
```

---

### 3. Run Container

```bash
docker run -d -p 3000:3000 devops-app
```

---

### 4. Access Application

Open browser:

```text
http://localhost:3000
```

---

## 🚀 CI/CD Flow Explanation

1. Developer pushes code to GitHub
2. GitHub Actions workflow is triggered
3. Docker image is built
4. Image is pushed to Docker Hub

---

## 💡 Key Learnings

* CI/CD pipeline automation using GitHub Actions
* Dockerizing a Node.js application
* Secure authentication using GitHub Secrets
* Integration between GitHub and Docker Hub

---

