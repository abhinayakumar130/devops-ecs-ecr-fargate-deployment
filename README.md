# 🚀 DevOps Project: Fully Automated ECS Deployment using Terraform, ECR, ALB, and GitHub Actions

This project automates the full deployment lifecycle of a Docker-based web app using:
- **Amazon ECS (Fargate)** to run containers
- **Amazon ECR** to store Docker images
- **Application Load Balancer (ALB)** to expose the service publicly
- **Terraform** to automate infrastructure creation
- **GitHub Actions** to build, push, and deploy

Everything is done **automatically**, no manual creation in AWS Console.

---

## 📌 Use Case

Deploy a Dockerized web application using infrastructure-as-code (Terraform) and CI/CD (GitHub Actions). Ideal for scalable, secure, and automated containerized app hosting on AWS.

---

## 📂 Project Structure
```
devops-ecs-ecr-fargate-deployment/
│
├── terraform/
│ ├── main.tf # Contains complete Terraform infrastructure
│ ├── variables.tf # All input variables
│ ├── outputs.tf # Final output values like ALB URL
│ └── backend.tf # Terraform remote backend config
│
├── app/
│ ├── Dockerfile # Dockerfile to containerize it
| └── index.js   # Node.js app entry point
│
└── .github/
  └── workflows/
    ├── ci-cd.yml # GitHub Actions CI/CD workflow
    └── destroy.yml # GitHub Actions destroy workflow
```
---

## 🔧 Components & Why They're Used

| Component        | Purpose                                                                 |
|------------------|-------------------------------------------------------------------------|
| VPC              | Isolated network for your ECS resources                                 |
| Subnets          | Public subnets to run Fargate tasks and connect with ALB                |
| Internet Gateway | Allows traffic from the internet to reach the ALB and containers      |
| Route Table      | Enables public subnet routing to the internet gateway                   |
| ECR              | Stores your Docker image built by GitHub Actions                        |
| ECS Cluster      | Manages container orchestration using Fargate                           |
| Task Definition  | Defines container settings (image, CPU, memory, port)                   |
| ALB              | Routes incoming traffic to running ECS containers                       |
| GitHub Actions   | Automates Docker build, push to ECR, and Terraform apply/destroy        |

---

## 🚀 How to Deploy

### 1️⃣ Configure GitHub Secrets

In your repo, add these under **Settings > Secrets > Actions**:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`

---

### 2️⃣ Trigger Deployment

On every push to `main` branch or by manual trigger:

- Builds Docker image from `app/Dockerfile`
- Pushes image to **ECR**
- Runs Terraform to:
  - Provision infra (VPC, ALB, ECS)
  - Deploy your container app

---

### 3️⃣ Access the App

 After deployment, Terraform will output the **ALB DNS name**:
 
  `alb_dns_name = "ecs-alb-xxxxx.us-east-1.elb.amazonaws.com`
  
  Open this URL in a browser to see your app running 🎉

---

## 🧹 To Destroy Everything

Use the **"Destroy ECS Infrastructure"** GitHub Action or run locally:

```bash
cd terraform
terraform destroy -auto-approve
```

## 🧪 Testing
You can check the following:

 - GitHub Actions logs: Confirm Docker image build + push
 - ECS Console: See running task
 - ALB: Open the DNS URL to verify deployment

## 🛠 Tools Used
 - Terraform
 - AWS ECS Fargate
 - AWS ECR
 - AWS ALB
 - GitHub Actions
 - Docker

## 📚 Learnings from the Project
 - Full AWS ECS deployment automation
 - Secure handling of IAM credentials via GitHub
 - CI/CD pipeline for containers
 - Real-world VPC + subnet setup for production-like scenario

##🙋‍♀️ Author
Abhinaya Muthukumar
DevOps Engineer | Terraform & AWS Automation Enthusiast
