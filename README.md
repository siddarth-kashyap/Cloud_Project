# AWS Cloud Resume Challenge - Serverless Architecture

Welcome to my Cloud Resume Challenge project! This repository showcases the conceptualization, engineering, and deployment of my personal resume website as a highly available, scalable, and fully automated serverless application on AWS.
The core objective of this project was to leverage modern cloud-native technologies to build a durable, performant, and secure platform, fully managing infrastructure-as-code using Terraform and demonstrating strong competency in AWS, IaC, CI/CD, and serverless architectures. A full-stack, serverless resume website built completely on AWS using Infrastructure as Code (IaC) and deployed via Continuous Integration/Continuous Deployment (CI/CD). This is my attempt at cloud resume challenge in AWS. 
What is Cloud Resume Challenge? - <a href="https://cloudresumechallenge.dev/">The Cloud Resume Challenge</a> is a multiple-step resume project which helps build and demonstrate skills fundamental to pursuing a career in Cloud. 

## Architecture Diagram
![Cloud Architecture](link-to-your-diagram.png)

The architecture follows a standard serverless pattern:

1.  **Frontend (Static S3 & CloudFront CDN):** Your personal resume page, decoupled from local assets, is securely hosted on an S3 bucket and globally delivered via CloudFront CDN. SSL/TLS certificates (ACM) are integrated for consistent security.
2.  **API Entry (API Gateway):** A secure and scalable endpoint that async-triggers the backend logic.
3.  **Compute (Lambda):** Serverless Go/Python/Node.js **customize with your backend language** functions process visitor interactions and manage database communication.
4.  **Database (DynamoDB):** A scalable NoSQL database securely stores visitor metrics (e.g., page view counts).
5.  **Automation & IaC (Terraform & CI/CD Pipeline):**

**Key features include:**

* **Bespoke Resume Website:** A dynamic personal resume with features like visitor tracking, demonstrating direct serverless backend interaction. **customize with specific resume features/metrics**
* **100% Serverless Architecture (AWS):** No servers to manage, ensuring maximum scalability and cost-efficiency.
* **Infrastructure-as-Code (IaC) with Terraform:** Complete infrastructure, from networking to database, defined programmatically for repeatability and consistency. **customize with mention of Terraform modules, complex dependencies, etc.**
* **Automated CI/CD Pipeline:** Fully automated deployment bridge, ensuring seamless integration and delivery for both infrastructure changes and application code. **customize with your actual CI/CD tool**

## ⚙️ Technical Stack & Engineering Details
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

Working URL - <a href="https://dti4lnjhf12l.cloudfront.net/">Siddarth Kashyap - Multicloud DevOps Engineer</a>


### CI/CD Pipeline (Automation)
**[INSERT SCREENSHOT OR LINK TO GREEN PIPELINE RUN IF POSSIBLE]**


## Setup & Deployment Guide

This project is fully managed via Terraform. **Ensure you have the prerequisites installed before proceeding.**

### Prerequisites
1.  Terraform installed.
2.  AWS CLI configured with suitable permissions.
3.  Access to a Git repository for this project.

### Trigger Automated Updates
For seamless, automated integration and delivery:
* Simply push code or Terraform changes to your Git repository, and watch the CI/CD pipeline and AWS environment update themselves automatically.

---

## Unique Challenges & Customizations

* **customize EXAMPLE 1:** Engineered dynamic visitor counting application logic entirely within Lambda using complex asynchronous database interactions and robust error handling to handle high traffic bursts.
* **customize EXAMPLE 2:** Optimized CloudFront caching strategy with precise path-based cache expiration and preloading for sub-second page load times globally.
* **customize EXAMPLE 3:** Overcame complex Terraform state management dependencies when integratingRoute53 DNS validation for ACM certificates across different AWS accounts.

---

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


