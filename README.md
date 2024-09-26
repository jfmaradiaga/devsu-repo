
# DevOps Technical Test - Django Application

This repository contains a Django-based application for a DevOps technical test. The application is containerized with Docker and deployed to an AWS EKS cluster using Kubernetes. The project includes a CI/CD pipeline using GitHub Actions for automating build, test, and deployment processes.

---

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Local Setup](#local-setup)
3. [Docker Setup](#docker-setup)
4. [AWS EKS Deployment](#aws-eks-deployment)
5. [Kubernetes Configuration](#kubernetes-configuration)
6. [CI/CD Pipeline](#ci-cd-pipeline)
7. [API Endpoints](#api-endpoints)
8. [Cleanup Resources](#cleanup-resources)

---

## Prerequisites

Before you begin, ensure you have the following installed:

- [Python 3.11.x](https://www.python.org/downloads/)
- [Docker](https://www.docker.com/)
- [AWS CLI](https://aws.amazon.com/cli/)
- [eksctl](https://eksctl.io/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- AWS account with access to create EKS clusters

---

## Local Setup

### 1. Clone the Repository:
```bash
git clone https://github.com/jfmaradiaga/devsu-repo.git
cd devsu-repo
```
### 2. Install Dependencies:
```bash
pip install -r requirements.txt
```
### 3. Run Migrations:
```bash
python manage.py makemigrations
python manage.py migrate
```
### 4. Start the Application:
```bash
python manage.py runserver
```
## Docker Setup

### 1. Build Docker Image:
```bash
docker build -t jfmaradiaga/django-devops-app .
```
### 2. Run the application in a Docker container:
```bash
docker run -p 8000:8000 jfmaradiaga/django-devops-app
```
### 3. Push the Docker image to Docker Hub:
```bash
docker push jfmaradiaga/django-devops-app
```

## AWS EKS Deployment

### 1. Create an EKS cluster:
```bash
eksctl create cluster \
  --name devops-cluster \
  --version 1.27 \
  --region us-east-1 \
  --nodegroup-name linux-nodes \
  --node-type t3.small \
  --nodes 1 \
  --nodes-min 1 \
  --nodes-max 2 \
  --managed
```
### 2. Update kubeconfig:
```bash
aws eks --region us-east-1 update-kubeconfig --name devops-cluster
```
## Kubernetes Configuration

### 1. Apply Kubernetes Deployment and Services:
```bash
cd k8s
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```
### 2. Check Deployment and service status:
```bash
kubectl get deployments
kubectl get services
```
### 3. Access the application:
Find the EXTERNAL-IP from the output of the kubectl get services command. Open the IP address in your browser.

## CI/CD Pipeline
This project includes a GitHub Actions pipeline to automate the build, test, and deployment of the application.

Pipeline Stages:
1. Checkout Code: Pulls the latest code from the repository.
2. Set Up Python: Installs the Python environment.
3. Install Dependencies: Installs the required dependencies from requirements.txt.
4. Run Django Tests: Executes Django tests using manage.py test.
5. Build Docker Image: Builds the Docker image.
6. Push Docker Image: Pushes the image to Docker Hub.
7. Deploy to Kubernetes: Deploys the application to the AWS EKS cluster.

### To view CI/CD pipeline.
Go to the Actions tab in your GitHub repository to view the pipeline status and logs.

## API Endpoints
The Django REST API provides the following endpoints:
### 1. Create User:
* Endpoint: /api/users/
* Method: POST
* Body
```json
{
  "dni": "123456",
  "name": "John Doe"
}
```
### 2. Get users:
* Endpoint: /api/users/
* Method: GET

### 3. Get user by id:
* Endpoint: /api/users/<id>/
* Method: GET

## Cleanup Resources
Last but not least, to avoid any non-desirable charges, make sure to delete your EKS cluster once you are done:
```bash
eksctl delete cluster --name devops-cluster --region us-east-1
```

## Repo Map
![2024-09-25 20_09_24-DevOps Technical Test Assistance and 11 more pages - Personal - Microsoft​ Edge](https://github.com/user-attachments/assets/ac8c5b1e-100c-4655-bd5c-a02ee81421b1)

## Diagram
![Untitled](https://github.com/user-attachments/assets/ee8359c6-62b2-43f7-a04e-0f7adbd91f04)

## Screenshots
![2024-09-25 20_02_22-Api Root – Django REST framework and 9 more pages - Personal - Microsoft​ Edge](https://github.com/user-attachments/assets/583b371d-1e01-49d3-ae22-f85c6390ddc7)
