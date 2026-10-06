# Troubleshooting

## Jenkins Agent Connection

The Jenkins Controller connects to the Jenkins Agent using SSH.

## Java Version

Jenkins Agent requires a compatible Java version.

Java 21 is used on the Jenkins Agent.

## Docker

The Jenkins Agent is configured to execute Docker commands.

## Kubernetes Connectivity

kubectl is configured on the Jenkins Agent to communicate with Amazon EKS.

## EKS Security Group

The Jenkins Agent security group must be allowed to communicate with the EKS cluster security group on TCP port 443.

## ALB Health Check

The application uses `/webapp/` as the ALB health-check path because `/webapp/` returns HTTP 200.
