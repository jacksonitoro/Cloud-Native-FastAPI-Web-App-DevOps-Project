# CLOUD NATIVE: FastAPI Web App DevOps Project

## Project Overview
This project demonstrates how to containerize a Python FastAPI web application, deploy it using Docker, and implement CI/CD pipelines to automate deployment to AWS EC2 instances.

---

## Objectives
1. Containerize a Python FastAPI web application using Docker.
2. Deploy the Dockerized app on AWS EC2 instances.
3. Set up GitHub Actions CI/CD to automatically build, push, and deploy the application.
4. Ensure the application is consistently deployed to two EC2 instances.
5. Integrate Vault for managing sensitive environment variables.

---

## Dockerizing Python Web App

### Step 1: Create Dockerfile
### dockerfile
- FROM python:3.11-slim

- Set working directory
WORKDIR /app

- Copy project files
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .

- Expose port
EXPOSE 8000

- Start the app
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]

# Build and Run Docker Image Locally
### bash
- docker build -t fastapi-app .
- docker run -p 8000:8000 -e VAULT_ADDR="http://<VAULT_ADDR>" -e VAULT_ROLE_ID="<ROLE_ID>" -e VAULT_SECRET_ID="<SECRET_ID>" fastapi-app


# Setting Up EC2 in AWS
## Launch two Ubuntu EC2 instances.
## SSH into each EC2 instance:
- ssh -i "key-pair.pem" ubuntu@<EC2_PUBLIC_IP>
## Install Docker:
- sudo apt update
- sudo apt install -y docker.io
- sudo systemctl enable docker
- sudo systemctl start docker
- sudo usermod -aG docker ubuntu
## Test Docker installation:
- docker --version


