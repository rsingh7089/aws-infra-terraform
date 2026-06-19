# ☁️ AWS Infrastructure — Terraform Modules

Production-ready Terraform modules for provisioning and managing AWS infrastructure. Built with best practices — modular, reusable, and environment-aware using Terraform Workspaces.

## 🏗️ Architecture Overview
```
aws-infra-terraform/
├── modules/
│   ├── vpc/              # VPC, Subnets, Route Tables, IGW, NAT
│   ├── ec2/              # EC2 instances, Security Groups, Key Pairs
│   ├── s3/               # S3 Buckets with versioning, encryption, lifecycle
│   ├── iam/              # IAM Roles, Policies, Users
│   ├── sqs/              # SQS Queues + Dead Letter Queues
│   ├── lambda/           # Lambda functions + triggers
│   ├── api-gateway/      # REST API Gateway + stages
│   └── transfer-family/  # AWS Transfer Family (SFTP) server
├── environments/
│   ├── dev/
│   ├── qa/
│   ├── stg/
│   └── prod/
├── main.tf
├── variables.tf
├── outputs.tf
└── backend.tf            # Remote state in S3 + DynamoDB locking
```

## 🚀 Usage

### Prerequisites
- Terraform >= 1.0
- AWS CLI configured
- S3 bucket for remote state

### Deploy to an environment
```bash
# Initialize
terraform init

# Select workspace
terraform workspace select dev   # dev / qa / stg / prod

# Plan
terraform plan -var-file="environments/dev/terraform.tfvars"

# Apply
terraform apply -var-file="environments/dev/terraform.tfvars"
```

### Example — Create VPC
```hcl
module "vpc" {
  source = "./modules/vpc"

  vpc_cidr           = "10.0.0.0/16"
  environment        = "dev"
  availability_zones = ["us-east-2a", "us-east-2b"]
  private_subnets    = ["10.0.1.0/24", "10.0.2.0/24"]
  public_subnets     = ["10.0.101.0/24", "10.0.102.0/24"]
}
```

## 🔐 Security Best Practices Applied
- ✅ S3 buckets — SSE-S3 encryption + versioning enabled
- ✅ IAM — least privilege policies, no wildcard `*` actions
- ✅ EC2 — SSM Session Manager (no SSH port 22 open)
- ✅ VPC — Private subnets for application tier
- ✅ Remote state — encrypted S3 backend + DynamoDB state locking

## ☁️ AWS Services Covered
```
VPC | EC2 | S3 | IAM | SQS | Lambda | API Gateway
RDS | CloudWatch | SSM | Transfer Family | Route53
```

## 🛠️ Tech Stack
![Terraform](https://img.shields.io/badge/Terraform-%235835CC.svg?style=flat&logo=terraform&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=flat&logo=amazon-aws&logoColor=white)

## 👤 Author
**Ranjeet Singh** — DevOps & Cloud Engineer | AWS SAA-C03 | Terraform Associate  
[LinkedIn](https://linkedin.com/in/ranjeet-singh-indore) | [GitHub](https://github.com/rsingh7089)
