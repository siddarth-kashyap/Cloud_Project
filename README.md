# AWS Cloud Resume Challenge - Serverless Architecture

A full-stack, serverless resume website built completely on AWS using Infrastructure as Code (IaC) and deployed via Continuous Integration/Continuous Deployment (CI/CD). This is my attempt at cloud resume challenge in AWS. What is Cloud Resume Challenge? - <a href="https://cloudresumechallenge.dev/">The Cloud Resume Challenge</a> is a multiple-step resume project which helps build and demonstrate skills fundamental to pursuing a career in Cloud. 

## Architecture Diagram
![Cloud Architecture](link-to-your-diagram.png)

## ⚙️ Technology Stack
- **Frontend:** HTML, CSS, JavaScript
- **Backend:** Python
- **Cloud Provider:** Amazon Web Services (AWS)
- **Infrastructure as Code (IaC):** Terraform
- **CI/CD:** GitHub Actions
- **State Management:** AWS S3 (State File) & DynamoDB (State Lock)

## 🌐 Cloud Services Utilized
* **Amazon S3:** Hosts the static frontend assets. Public access is strictly blocked.
* **Amazon CloudFront:** Global Content Delivery Network (CDN) enforcing HTTPS and utilizing Origin Access Control (OAC) to securely fetch assets from S3.
* **Amazon API Gateway:** HTTP API acting as the secure entry point for the backend, configured with strict CORS rules.
* **AWS Lambda:** Serverless compute running Python (boto3) to execute the visitor counter logic.
* **Amazon DynamoDB:** NoSQL database storing the atomic visitor count.
* **AWS IAM:** Enforces least-privilege access, ensuring Lambda can only update specific database tables and API Gateway can only trigger specific functions.

## 🚀 Deployment Pipeline (CI/CD)
This project utilizes **GitHub Actions** for fully automated deployment. The pipeline triggers on every push to the `main` branch and executes two jobs:

1. **Infrastructure Provisioning:** Authenticates securely with AWS, runs `terraform fmt`, `terraform plan`, and `terraform apply` to dynamically provision or update cloud resources.
2. **Frontend Synchronization:** Syncs the local `frontend/` directory to the S3 bucket and automatically creates a CloudFront invalidation to clear the global edge cache.

## 📂 Repository Structure
```text
.
├── .github/workflows/deploy.yml   # CI/CD Pipeline configuration
├── backend/
│   └── lambda_function.py         # Python logic for DynamoDB update
├── frontend/
│   └── index.html                 # Static website assets
└── infrastructure/
    ├── main.tf                    # Core Terraform resources
    ├── outputs.tf                 # Generated API URLs and Bucket Names
    └── variables.tf               # Environment variables
