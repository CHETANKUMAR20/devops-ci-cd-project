# devops-ci-cd-project
🚀 DevOps CI/CD Project Documentation
📌 Project Overview

This project demonstrates an end-to-end CI/CD pipeline using:

GitHub Actions (CI/CD)

Docker (Containerization)

Amazon ECR (Container Registry)

Amazon EC2 (Deployment Target)

IAM Roles (Secure authentication)

The pipeline automatically builds a Docker image, pushes it to ECR, and deploys the latest version to EC2 whenever code is pushed to the main branch.

🏗 Architecture Flow
Developer Push → GitHub Actions → Docker Build → ECR Push → 
SSH to EC2 → Stop Old Container → Pull New Image → Run Container

🛠 Technologies Used

AWS EC2

AWS ECR

IAM Roles

GitHub Actions

Docker

Python (Flask)

Amazon Linux

⚙ Infrastructure Setup
1️⃣ EC2 Instance

Amazon Linux

Docker installed

Port 5000 allowed in Security Group

IAM Role attached for ECR access

2️⃣ ECR Repository

Repository name: devops-ci-cd-project

Stores Docker images

3️⃣ GitHub Secrets Used
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_REGION
AWS_ACCOUNT_ID
ECR_REPOSITORY
EC2_HOST
EC2_USER
EC2_SSH_KEY

🚀 CI/CD Workflow Steps

Checkout Code

Configure AWS credentials

Login to ECR

Build Docker image

Tag image

Push image to ECR

SSH to EC2

Stop old container

Pull latest image

Start new container

🐞 Issues Faced & Solutions
❌ Issue 1 – Invalid Workflow YAML

Error:

Invalid workflow file
A sequence was not expected


Cause:
Incorrect YAML indentation / incomplete structure.

Solution:
Rewrote full workflow file with proper name, on, and jobs structure.

❌ Issue 2 – ECR Repository Not Found

Error:

repository does not exist in the registry


Cause:
Region mismatch / incorrect ECR repository name in GitHub Secrets.

Solution:
Verified AWS region and corrected ECR_REPOSITORY and AWS_REGION values.

❌ Issue 3 – Invalid Security Token

Error:

The security token included in the request is invalid


Cause:
Incorrect AWS access keys in GitHub Secrets.

Solution:
Generated new IAM access key and updated GitHub secrets.

❌ Issue 4 – Docker Build Context Error

Error:

docker buildx build requires 1 argument


Cause:
Missing . (build context) in docker build command.

Solution:
Updated build command to:

docker build -t app-image .

❌ Issue 5 – Image Tag Failed

Error:

:latest: command not found


Cause:
ECR_REPOSITORY secret was missing.

Solution:
Added correct secret in GitHub repository settings.

❌ Issue 6 – Cannot Access App via Browser

Cause:
Container crashed due to Python indentation error.

Error in Logs:

IndentationError: expected an indented block


Solution:
Fixed indentation in app.py and pushed new version.

❌ Issue 7 – Unable to Pull Image from EC2

Error:

Unable to locate credentials


Cause:
EC2 had no AWS credentials.

Solution:
Created IAM Role with AmazonEC2ContainerRegistryReadOnly
and attached role to EC2 instance.

❌ Issue 8 – no basic auth credentials

Cause:
ECR login token expired.

Solution:
Re-executed:

aws ecr get-login-password | docker login

🔐 Security Best Practices Implemented

Used IAM Roles instead of hardcoded credentials on EC2

Used GitHub Secrets for secure credential storage

Avoided storing AWS keys in application code

Used least privilege role for ECR access

📈 What This Project Demonstrates

CI/CD Pipeline Implementation

Infrastructure Debugging

Docker Container Management

AWS IAM Best Practices

Real-world Production Troubleshooting

Automated Deployment Strategy

🎯 Final Outcome

Application successfully deployed and accessible at:

http://<EC2_PUBLIC_IP>:5000


Version updates automatically deployed via GitHub push.

🏆 Key Learning Outcomes

YAML troubleshooting

AWS credential debugging

IAM role vs access keys understanding

Container lifecycle management

Deployment automation design

Production error debugging
