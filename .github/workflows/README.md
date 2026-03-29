# 🚀 Flask App Deployment using Docker & GitHub Actions CI/CD

## 📌 Project Overview

This project demonstrates a complete **CI/CD pipeline** for deploying a simple Flask application using:

* 🐍 Flask (Python Web Framework)
* 🐳 Docker (Containerization)
* 🔁 GitHub Actions (CI/CD Automation)
* 📦 Docker Hub (Image Registry)

The pipeline automatically builds and pushes a Docker image to Docker Hub whenever code is pushed to the repository.

---

## 🏗️ Architecture

```
Developer → GitHub Repo → GitHub Actions → Docker Build → Docker Hub
```

---

## ⚙️ Tech Stack

* Python (Flask)
* Docker
* GitHub Actions
* Docker Hub

```

---

## 🧑‍💻 Application Code

### app.py

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, DevOps World!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

---

## 📦 Requirements

```txt
flask
```

---

## 🐳 Docker Setup

### Dockerfile

```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

---

## 🔁 CI/CD Pipeline (GitHub Actions)

### Workflow File: `.github/workflows/ci-cd.yml`

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build-and-push:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Login to Docker Hub
        run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin

      - name: Build Docker Image
        run: docker build -t ${{ secrets.DOCKER_USERNAME }}/flask-app:latest .

      - name: Push Docker Image
        run: docker push ${{ secrets.DOCKER_USERNAME }}/flask-app:latest
```

---

## 🔐 GitHub Secrets Setup

Add the following secrets in your GitHub repository:

* `DOCKER_USERNAME`
* `DOCKER_PASSWORD`

📍 Path:
`Repo → Settings → Secrets → Actions`

---

## ▶️ How It Works

1. Developer pushes code to GitHub
2. GitHub Actions workflow triggers automatically
3. Docker image is built
4. Image is pushed to Docker Hub

---

## 🚀 How to Run Locally

### 1. Clone Repository

```bash
git clone <your-repo-url>
cd <repo-folder>
```

### 2. Build Docker Image

```bash
docker build -t flask-app .
```

### 3. Run Container

```bash
docker run -d -p 5000:5000 flask-app
```

### 4. Access Application

```
http://localhost:5000
```

---


