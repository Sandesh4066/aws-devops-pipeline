# AWS DevOps Pipeline - Infrastructure as Code Project

![AWS](https://img.shields.io/badge/AWS-ECS%20%7C%20ECR%20%7C%20VPC-orange)
![Terraform](https://img.shields.io/badge/Terraform-IaC-purple)
![Docker](https://img.shields.io/badge/Docker-Containerized-blue)
![CI/CD](https://img.shields.io/badge/CI%2FCD-GitHub%20Actions-green)

A production-ready DevOps project demonstrating automated infrastructure provisioning and continuous deployment on AWS using modern cloud-native tools.

## 🚀 Live Demo

**Application URL:** `http://3.110.175.222`

## 📋 Project Overview

This project showcases a complete DevOps workflow with:

- **Infrastructure as Code (IaC)** using Terraform
- **Containerization** with Docker
- **AWS ECS Fargate** for serverless container orchestration
- **Automated CI/CD** pipeline with GitHub Actions
- **AWS ECR** for private container registry
- **Custom VPC** with multi-AZ deployment
- **CloudWatch** for logging and monitoring

## 🏗️ Architecture
```
┌─────────────────┐
│  GitHub Repo    │
│  (Source Code)  │
└────────┬────────┘
         │
         │ Push triggers
         │
         ▼
┌─────────────────────────┐
│   GitHub Actions        │
│   (CI/CD Pipeline)      │
│   • Build Docker Image  │
│   • Push to ECR         │
│   • Deploy to ECS       │
└────────┬────────────────┘
         │
         │
         ▼
┌─────────────────────────┐
│   AWS Infrastructure    │
│   ┌─────────────────┐   │
│   │  Amazon ECR     │   │
│   │  (Container     │   │
│   │   Registry)     │   │
│   └─────────────────┘   │
│          │              │
│          ▼              │
│   ┌─────────────────┐   │
│   │  ECS Fargate    │   │
│   │  (2 containers) │   │
│   │                 │   │
│   │  VPC + Subnets  │   │
│   │  Security Groups│   │
│   └─────────────────┘   │
│          │              │
│          ▼              │
│   ┌─────────────────┐   │
│   │   CloudWatch    │   │
│   │   (Logs)        │   │
│   └─────────────────┘   │
└─────────────────────────┘
```

## 🛠️ Technologies Used

### Infrastructure & Cloud
- **AWS ECS Fargate** - Serverless container compute
- **AWS ECR** - Container image registry
- **AWS VPC** - Virtual Private Cloud with custom networking
- **AWS CloudWatch** - Centralized logging
- **AWS IAM** - Role-based access control
- **Terraform** - Infrastructure as Code (IaC)

### Application & DevOps
- **Docker** - Containerization
- **Nginx** - Web server
- **GitHub Actions** - CI/CD automation
- **Git** - Version control

## 📁 Project Structure
```
aws-devops-pipeline/
├── .github/
│   └── workflows/
│       └── deploy.yml          # CI/CD pipeline configuration
├── app/
│   ├── Dockerfile              # Container image definition
│   ├── index.html              # Application code
│   └── nginx.conf              # Web server configuration
├── terraform/
│   ├── main.tf                 # Main infrastructure definitions
│   ├── variables.tf            # Input variables
│   ├── outputs.tf              # Output values
│   └── terraform.tfvars        # Variable values
└── README.md                   # This file
```

## 🚀 Deployment Process

### Prerequisites
- AWS Account with appropriate permissions
- Terraform installed
- Docker installed
- AWS CLI configured
- GitHub account

### Infrastructure Deployment

1. **Clone the repository:**
```bash
   git clone https://github.com/Sandesh4066/aws-devops-pipeline.git
   cd aws-devops-pipeline
```

2. **Initialize Terraform:**
```bash
   cd terraform
   terraform init
```

3. **Deploy infrastructure:**
```bash
   terraform apply
```

4. **Build and push Docker image:**
```bash
   # Login to ECR
   aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin <ECR_URL>
   
   # Build and push
   cd ../app
   docker build -t devops-pipeline-app .
   docker tag devops-pipeline-app:latest <ECR_URL>:latest
   docker push <ECR_URL>:latest
```

5. **Deploy to ECS:**
```bash
   aws ecs update-service --cluster devops-pipeline-cluster --service devops-pipeline-service --force-new-deployment --region ap-south-1
```

### Automated Deployment (CI/CD)

Every push to the `main` branch automatically:
1. Builds a new Docker image
2. Pushes it to Amazon ECR
3. Deploys to ECS Fargate
4. Updates running containers with zero downtime

## 🔒 Security Features

- IAM roles with least-privilege access
- Security groups restricting network access
- Container image scanning in ECR
- Secrets management via GitHub Actions secrets
- VPC isolation for resources

## 📊 AWS Resources Created

- 1 VPC with custom CIDR
- 2 Public subnets across availability zones
- 1 Internet Gateway
- Route tables and associations
- Security groups with ingress/egress rules
- ECS Cluster
- ECS Service with 2 tasks
- ECR Repository
- IAM Roles and Policies
- CloudWatch Log Groups

## 💡 Key Learning Outcomes

- Infrastructure as Code principles
- Container orchestration with ECS
- CI/CD pipeline design and implementation
- AWS networking fundamentals
- Security best practices in cloud
- GitOps workflow

## 🔄 Future Enhancements

- [ ] Add Application Load Balancer for production-grade traffic distribution
- [ ] Implement auto-scaling based on CloudWatch metrics
- [ ] Add SSL/TLS certificates for HTTPS
- [ ] Integrate monitoring dashboards
- [ ] Add automated testing in CI/CD pipeline
- [ ] Implement blue-green deployments
- [ ] Add cost optimization tags and budget alerts

## 📝 License

This project is open source and available for educational purposes.

## 👤 Author

**Sandesh**
- GitHub: [@Sandesh4066](https://github.com/Sandesh4066)

---

⭐ If you found this project helpful, please give it a star!