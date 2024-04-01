# CI/CD Project-DevOps-devops-prod.online

## Overview
This repository contains the source code and configurations for a DevOps project. The CI/CD pipeline automates various stages, including building, testing, security checks, and deployment using GitHub Actions.

## Continuous Integration (CI) - Build, Test, Push
The CI pipeline is triggered on a schedule (daily at midnight) and on each push to the repository. It includes the following steps:

1. **Build the Stack:** 
   - Change to the 'react-app' directory and build the Docker containers using Docker Compose.

2. **Run Curl Test:**
   - Install curl, test the application endpoint, display running containers, and print the current working directory.

3. **Change Image Name:**
   - Tag Docker images for MySQL and the React app with the appropriate names.

4. **Docker Push:**
   - Log in to Docker Hub using credentials from GitHub Secrets.
   - Push Docker images to the Docker Hub registry.

5. **Slack Notification:**
   - Notify Slack channel of successful CI pipeline completion.

## Security Check - Snyk
The security check job runs after the CI pipeline. It includes scanning infrastructure as code for security vulnerabilities using Snyk.

## Continuous Deployment (CD) - Terraform
The CD pipeline is triggered after the successful completion of the security check. It runs on a self-hosted runner and includes the following steps:

1. **Pull the Repository:**
   - Pull the latest changes from the GitHub repository.

2. **Terraform Initialization:**
   - Change to the 'Terraform' directory and initialize Terraform.

3. **Terraform Validation:**
   - Validate Terraform configurations.

4. **Terraform Plan:**
   - Display Terraform plan.

5. **Terraform Apply:**
   - Apply Terraform changes.

6. **AWS EKS Configuration:**
   - Update the kubeconfig file for AWS EKS.

7. **Namespace Setup:**
   - Create or delete namespaces for cert-manager, ingress-nginx, react-app, argocd, monitoring, and app-demo.

8. **Ingress and Certificate Installation:**
   - Install ingress controllers, certificates, and configure routing for applications.

9. **Monitoring Tools Deployment:**
   - Deploy Grafana, Prometheus, Loki, Mimir, Tempo, and Promtail for monitoring.

10. **React App Deployment:**
    - Deploy the React app.

11. **Slack Notification:**
    - Notify Slack channel of successful CD pipeline completion.

## Usage
1. Clone the repository.
2. Follow the steps in the CI/CD pipeline for building, testing, and deploying the project.
3. Monitor the Slack channel for notifications on pipeline success.

## Dependencies
Ensure the following dependencies are met:
  - secrets 
  - Docker 
  - Snyk
  - AWS CLI
  - Terraform
  - Slack Notification

## Slack Notifications
To receive Slack notifications, set up the SLACK_INCOMING_WEBHOOK secret in your GitHub repository.

## Snyk Security
To perform security checks with Snyk, provide the SNYKTOKEN secret in your GitHub repository.

## GitHub Actions Secrets
Make sure to add the necessary secrets in your GitHub repository for Docker Hub, Slack, and Snyk integration.

For questions or contributions, please open an Issue or submit a Pull Request.
