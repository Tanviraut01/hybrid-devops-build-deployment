# Hybrid DevOps Architecture

## Project Flow

GitHub → Jenkins Controller → Jenkins Agent → Maven → SonarQube → Docker → Docker Hub → Amazon EKS → Kubernetes → AWS ALB → Route 53

## AWS Components

- EC2 - Jenkins Controller
- EC2 - Jenkins Agent
- EC2 - SonarQube
- EC2 - JFrog Artifactory
- Amazon EKS
- Kubernetes
- AWS Load Balancer Controller
- Application Load Balancer
- Route 53

## Application

The application is packaged as a Maven WAR application and containerized using Docker.

## Deployment

The application is deployed to Amazon EKS using Kubernetes Deployment, Service and Ingress resources.
