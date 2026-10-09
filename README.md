# Hybrid-Based Build and Deployment via Docker & Kubernetes

## Project Overview

This project automates the build and deployment of a Java web application using Jenkins, Maven, SonarQube, Docker, and Amazon EKS.

## Technologies Used

- AWS EC2 and Amazon EKS
- Jenkins for CI/CD automation
- Git and GitHub for source control
- Maven for application packaging
- SonarQube for code quality analysis
- Docker and Docker Hub for containerization
- Kubernetes for container orchestration
- AWS Load Balancer Controller and Application Load Balancer for public access

## CI/CD Pipeline

1. Checkout source code from GitHub.
2. Build and package the application using Maven.
3. Analyze code with SonarQube.
4. Build a Docker image.
5. Push the image to Docker Hub.
6. Deploy the application to Amazon EKS.
7. Verify the Kubernetes deployment.

## Architecture

Developer → GitHub → Jenkins → Maven Build → SonarQube → Docker Build and Push → Amazon EKS → AWS Load Balancer → Web Application

## Live Demo

http://hybrid-devops.pntr.dev/webapp/

## Key Challenges and Learnings

- Updated the EKS kubeconfig after the cluster endpoint changed.
- Configured IAM and Kubernetes access for the Jenkins agent.
- Troubleshot Kubernetes pod scheduling limits on worker nodes.
- Resolved deployment rollout issues by increasing worker-node capacity.
- Configured an AWS Application Load Balancer for public application access.

## Repository Structure

- `Jenkinsfile` — CI/CD pipeline definition
- `Dockerfile` — Docker image build instructions
- `k8s/` — Kubernetes deployment and ingress manifests
- `pom.xml` — Maven project configuration

## Future Improvements

- Configure HTTPS using AWS Certificate Manager.
- Add automated application tests.
- Improve monitoring and deployment rollback procedures.
