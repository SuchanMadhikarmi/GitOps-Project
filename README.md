# GitOps Project with AWS EKS & ECR (App + Infrastructure Repositories)

## Project Description

This GitOps-based DevOps project showcases a **CI/CD pipeline** for deploying a Java-based web application on **AWS EKS** using **Terraform**, **Maven**, **Docker**, and **Helm**. It separates infrastructure and application concerns into two GitHub repositories, automating provisioning and deployment with **GitHub Actions** and ensuring code quality with **SonarCloud**. The pipeline supports staging-to-production promotion, secure credential management, and scalable Kubernetes deployments.

All screenshots of the deployment steps are available in the **`screenshots`** folder.

---

 # Project Repositories

## Infrastructure Repository
Manages AWS infrastructure provisioning using **Terraform**.

🔗 [Infrastructure Repository](https://github.com/SuchanMadhikarmi/iac-vprofile)

## Application Repository
Handles the development, containerization, and deployment of a Java-based web application using **Maven**, **Docker**, and **Helm**.

🔗 [Application Repository](https://github.com/SuchanMadhikarmi/iac-vprofile)


The project is adapted from the **Udemy course "GitOps with AWS EKS and Terraform"**, extended with features like custom Helm charts, SonarCloud integration for code quality, and a secure CI/CD pipeline. It showcases best practices such as automated testing, image scanning, and staged promotion from staging to production environments, providing a real-world example of a scalable and secure deployment pipeline.

---

##  Repository Structure

### 1. Infrastructure Repository (`infra-repo`)
Manages AWS infrastructure provisioning and updates using **Terraform**:
- AWS EKS cluster creation
- AWS ECR registry for Docker images
- S3 backend for Terraform state
- IAM roles and service accounts for EKS
- Helm provider configuration for Kubernetes resources

**Branching Strategy**:
- `staging` branch: Infrastructure changes are tested here
- `main` branch: Production-ready infrastructure code is merged after peer review

Changes are automatically applied using **GitHub Actions** workflows configured for each branch.

### 2. Application Repository (`app-repo`)
Handles application code, quality checks, containerization, and deployment to EKS:
- Java-based web application built using **Maven**
- Containerized using **Docker**
- Deployed to EKS using **Helm**
- Continuous integration and delivery using **GitHub Actions**

**Branching Strategy**:
- `staging`: Application changes are tested here
- `main`: Production-ready application code is deployed after validation

---

##  Tech Stack & Technologies

### Infrastructure Repository
- **Terraform**: Infrastructure as Code for provisioning AWS resources
- **AWS EKS**: Managed Kubernetes cluster for hosting applications
- **AWS ECR**: Container registry for storing Docker images
- **AWS S3**: Remote backend for Terraform state storage
- **GitHub Actions**: Automation of CI/CD pipelines
- **Helm**: Kubernetes package manager for deploying resources

### Application Repository
- **Maven**: Build tool for Java application
- **Docker**: Containerization of the application
- **Helm**: Deployment to EKS
- **SonarCloud**: Static code analysis and quality gates
- **GitHub Actions**: CI/CD pipeline for application lifecycle
- **AWS ALB Ingress Controller**: For routing traffic to the application

---

##  Infrastructure Workflow (Infra Repo)

### Tools & Services:
- **Terraform** for Infrastructure as Code
- **AWS EKS** for Kubernetes Cluster
- **AWS S3** for Terraform backend
- **GitHub Actions** for CI/CD
- **Helm** for Kubernetes deployments

### Setup Steps:
1. **GitHub Repository Initialization**:
   - Created the `infra-repo` with `staging` and `main` branches.
2. **Terraform Configuration**:
   - Wrote Terraform scripts to provision:
     - AWS EKS Cluster
     - ECR Repositories
     - IAM roles and OIDC for Kubernetes
     - S3 bucket for remote backend
     - Helm provider for Kubernetes
3. **GitHub Secrets Configured**:
   - `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `TF_STATE_BUCKET`, `TF_REGION`
4. **Terraform State Management**:
   - Used AWS S3 for secure remote state storage
5. **GitHub Actions Workflow**:
   - Configured to:
     - Format and lint Terraform code
     - Run `terraform plan` on `staging` branch
     - Run `terraform apply` on `main` branch (after PR approval)
6. **EKS Access & Helm Setup**:
   - Installed Helm in GitHub workflow runner
   - Set up `kubectl` context using `aws eks update-kubeconfig`

---

## Application Workflow (App Repo)

### Tools & Services:
- **Maven** for building Java application
- **Docker** for containerization
- **AWS ECR** for image storage
- **Helm** for deployment
- **SonarCloud** for static code analysis and quality gates
- **GitHub Actions** for CI/CD

### Setup Steps:
1. **GitHub Repository Initialization**:
   - Created the `app-repo` and initialized GitHub Actions workflows
2. **Docker Setup**:
   - Created a custom `Dockerfile` for the Maven-based Java app
   - Used multi-stage Docker builds to optimize image size
3. **SonarCloud Integration**:
   - Created a SonarCloud organization and generated a token
   - Added token to GitHub Secrets
   - Configured `.sonarcloud.properties` in the repository
   - Set up a custom quality gate
4. **Secrets Added**:
   - `SONAR_TOKEN`, `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `ECR_REPOSITORY`, `KUBECONFIG`
5. **Helm Setup**:
   - Created custom Helm charts (removed default templates)
   - Defined values in `values.yaml` and secrets in `secrets.yaml`
   - Used custom `deployment.yaml`, `service.yaml`, and `ingress.yaml`
6. **GitHub Actions Workflow**:
   - Workflow jobs:
     - Code Checkout
     - Maven Build
     - SonarCloud Analysis
     - Docker Image Build & Push to ECR
     - Helm Deployment to EKS
   - Validated application deployment on each push to `main`

---

##  Testing and Manual Workflow

1. **Initial Manual Test**:
   - Ran GitHub workflows manually to validate the end-to-end pipeline
   - Verified Terraform infrastructure provisioning
   - Confirmed successful image push to ECR
   - Validated deployment to EKS
2. **Ingress Setup & Custom Domain**:
   - Configured Kubernetes Ingress controller (ALB Ingress)
   - Set up a custom domain pointing to the ingress endpoint
   - Validated application access via HTTPS

---

##  Security Considerations

- Used GitHub Secrets for all credentials and tokens
- IAM roles scoped with least privilege access
- SonarCloud enforces quality gates before image deployment
- Terraform state encrypted and stored securely in S3

## Key Learnings

- **GitOps Workflow**: Learned to separate infrastructure and application concerns using distinct repositories and automated CI/CD pipelines
- **Terraform Management**: Gained expertise in provisioning AWS resources and managing state securely with S3
- **CI/CD Automation**: Mastered GitHub Actions for automating infrastructure and application deployments
- **Kubernetes with Helm**: Understood Helm chart creation and Kubernetes resource management for scalable deployments
- **Code Quality**: Integrated SonarCloud for static code analysis and enforced quality gates
- **Security Best Practices**: Implemented secure credential management and least privilege IAM roles
- **Ingress and Networking**: Configured AWS ALB Ingress Controller for secure and scalable application access

---

---

