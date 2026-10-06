# Deployment Process

## 1. Source Code

Application source code is maintained in GitHub.

## 2. Continuous Integration

Jenkins checks out the source code and builds the application using Maven.

## 3. Code Quality

SonarQube performs static code analysis.

## 4. Containerization

Docker builds an image containing the application and Tomcat.

## 5. Image Repository

The Docker image is pushed to Docker Hub.

## 6. Kubernetes Deployment

Jenkins deploys the application to Amazon EKS using Kubernetes manifests.

## 7. External Access

AWS Load Balancer Controller provisions an Application Load Balancer for the Kubernetes Ingress.

## 8. DNS

Route 53 provides DNS routing to the application.
