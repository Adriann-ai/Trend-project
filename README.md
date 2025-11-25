Trend Project - CI/CD Pipeline

GitHub Repositories:

        Trend Project :  https://github.com/Adriann-ai/Trend-project.git
        
        Terraform Project : https://github.com/Adriann-ai/Terraform-IAC-Trend_Project.git

Overview

This project demonstrates a full CI/CD pipeline leveraging AWS, Jenkins, Docker, Kubernetes (EKS), and monitoring tools (Prometheus + Grafana).

The pipeline automates:

        EC2 provisioning as a bastion host
        
        Docker image building and deployment
        
        Kubernetes manifests deployment to AWS EKS
        
        Monitoring via Prometheus and Grafana

Components
1. EC2 Bastion Server

        Launch an EC2 instance
        
        Install all required software:
        
        Java (for Jenkins)
        
        Jenkins
        
        AWS CLI
        
        eksctl
        
        kubectl
        
        Docker

2. Docker Hub

        Create a public repository to store Docker images
        
        Jenkins pipeline pushes built images to Docker Hub

3. Jenkins

        Install and configure the following plugins:
        
        Docker Pipeline
        
        Kubernetes
        
        Git

        Pipeline Stage View
        
        Configure AWS credentials, Docker Hub credentials, and Kubernetes service account tokens

4. AWS EKS

        Create an EKS cluster using the AWS console or eksctl
        
        Configure IAM roles for EKS and node groups
        
        Ensure Jenkins can deploy manifests via a Kubernetes service account and RBAC binding

5. RBAC for Jenkins

        Create a service account in EKS for Jenkins
        
        Bind the necessary roles and cluster role bindings
        
        Generate a token using Kubernetes secret
        
        Configure Jenkins with this token to deploy manifests

6. GitHub Integration

        Push all source code, Dockerfile, and Jenkinsfile to GitHub
        
        Webhook triggers the Jenkins pipeline automatically
        
        Jenkins pipeline executes:
        
        Builds Docker images
        
        Pushes images to Docker Hub
        
        Deploys manifests to EKS cluster

7. Monitoring

        Prometheus installed as a data source
        
        Grafana dashboard configured to visualize metrics
        
        Metrics collected from deployed services in EKS

Pipeline Flow
        Source code pushed to GitHub
               ↓ (Webhook)
        Jenkins pipeline triggered
               ↓
        Docker builds image → Push to Docker Hub
               ↓
        Jenkins deploys manifests to Kubernetes (EKS)
               ↓
        Prometheus collects metrics → Grafana dashboard visualizes

Prerequisites

        AWS account with permissions for EC2, EKS, IAM, and networking
        
        Docker Hub account for storing images
        
        Jenkins server installed on EC2 bastion host
        
        GitHub repository for source code, Dockerfile, and Jenkinsfile

Tools Used and Purpose
      AWS EC2	Bastion server and compute
      Docker Hub to	Store images
      Jenkins	CI/CD pipeline
      AWS EKS	Kubernetes cluster
      kubectl	Deploy manifests
      eksctl	Create/manage EKS clusters
      Prometheus	Metrics collection
      Grafana	Visualization/dashboard


 Workflow Summary

          Developer pushes code to GitHub
          
          Webhook triggers Jenkins pipeline
          
          Docker image built and pushed to Docker Hub
          
          Jenkins deploys manifests to EKS cluster
          
          Prometheus collects metrics → Grafana visualizes them
