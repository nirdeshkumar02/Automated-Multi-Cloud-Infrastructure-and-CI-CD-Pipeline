# Automated Multi-Cloud Infrastructure & CI/CD Pipeline Project

A demonstrative DevSecOps solution showcasing end-to-end automation, security integration, and SRE governance across the software deployment lifecycle.

This comprehensive DevSecOps pipeline addresses the need for secure, repeatable, and fiscally responsible deployments. The solution integrates IaC (Terraform), Continuous Delivery (Jenkins/Argo CD), and SRE Governance (Python/Boto3). This project highlights expertise in Infrastructure as Code (IaC), Continuous Delivery, and Cloud Automation (Boto3).

## 1. CI/CD Orchestration (jenkinsfile.txt)

The jenkinsfile.txt is a declarative Jenkins Pipeline script that orchestrates the entire deployment lifecycle, ensuring automated quality gates are met before code reaches production.

- SCM & Build: Pulls source code from the repository and uses Maven/Gradle to compile the Java application artifacts.

- Containerization: Builds the application's Docker image and pushes the validated artifact to AWS ECR.

- Security Scanning: Integrates SonarQube for static code analysis and Trivy for deep vulnerability scanning of the container image. Failures halt pipeline execution.

- Deployment: Prepares the application manifest for deployment to the EKS cluster, synchronizing with the continuous delivery tool, Argo CD.

- Post-Deployment Audit: Executes the crucial Python/Boto3 cleanup script to check and remediate cloud resource sprawl.

## 2. Infrastructure as Code (IaC) (main.tf)

The main.tf file contains the Terraform configuration used to provision the underlying AWS infrastructure for the application, ensuring repeatability and version control.

- EKS Cluster: Provisions a fully managed AWS EKS cluster, including node groups, security groups, and required networking (VPC).

- IAM Roles: Configures the necessary IAM roles and policies for the EKS nodes and the Jenkins pipeline to interact securely with AWS services (ECR, EKS).

- Efficiency: Reduces infrastructure setup time from hours to minutes, a key feature of IaC.

## 3. SRE Governance and Cloud Automation (cleanup_script.py)

The cleanup_script.py is an advanced automation layer that runs after deployment. It leverages Python and the Boto3 AWS SDK to perform essential SRE governance tasks, preventing cost overruns and maintaining resource hygiene.

Goal: To prevent cost overruns and maintain resource hygiene.

Functionality: The script audits the state of the EKS and EC2 fleet. It identifies and gracefully terminates or tags orphaned resources (e.g., EC2 instances or old EKS volumes) that were not correctly cleaned up by the deployment tool.
