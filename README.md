# AWS Infrastructure Templates

Professional Infrastructure as Code repository for multi-tier application deployment using AWS CloudFormation.

## 🏗️ Architecture Overview

This repository implements a **modular, multi-tier AWS infrastructure** with the following components:

### Infrastructure Layers
1. **Networking** (`vpc-stack.yml`)
   - VPC with public/private subnets
   - Internet Gateway and routing tables
   - Multi-AZ architecture for high availability

2. **Security** (`security-groups.yml`)
   - Layered security groups for different tiers
   - Web, application, database, bastion, and load balancer security
   - Defense-in-depth security principles

3. **Compute** (`ec2-compute.yml`)
   - Web servers in public subnet with Flask application
   - Application servers in private subnet for internal APIs
   - Auto-deployment via UserData scripts

4. **Storage** (`s3-storage.yml`)
   - Static website hosting bucket
   - Application data storage with lifecycle policies
   - Backup and logging buckets
   - Cost-optimized storage transitions

## 📁 Repository Structure

```
aws-infrastructure-templates/
├── README.md                          # Project documentation
├── infrastructure/                    # CloudFormation templates
│   ├── networking/
│   │   └── vpc-stack.yml             # VPC, subnets, routing
│   ├── security/
│   │   └── security-groups.yml       # Security groups
│   ├── compute/
│   │   └── ec2-compute.yml           # EC2 instances
│   └── storage/
│       └── s3-storage.yml            # S3 buckets
├── env/                              # Environment configurations
│   ├── dev-params.json               # Development parameters
│   └── prod-params.json              # Production parameters
├── scripts/                          # Deployment automation
│   └── deploy.sh                     # Deployment script
├── docs/                             # Documentation
└── examples/                         # Usage examples
```

## ✨ Key Features

- ✅ **Modular Design** - Independent, reusable CloudFormation templates
- ✅ **Cross-Stack References** - Templates import resources from other stacks
- ✅ **Environment Parameterization** - Same templates work for dev/test/prod
- ✅ **Enterprise Security** - Multi-tier security with proper isolation
- ✅ **Cost Optimization** - S3 lifecycle policies and right-sized instances
- ✅ **Production Ready** - Professional patterns and best practices

## 🚀 Quick Start

### Prerequisites
- AWS CLI installed and configured
- Valid AWS credentials with CloudFormation permissions
- EC2 Key Pair created in your target region

### Deploy Complete Infrastructure
```bash
# Clone repository
git clone https://github.com/your-username/aws-infrastructure-templates.git
cd aws-infrastructure-templates

# Deploy infrastructure (manual method)
# 1. Deploy networking layer
aws cloudformation create-stack \
  --stack-name dev-networking \
  --template-body file://infrastructure/networking/vpc-stack.yml \
  --parameters file://env/dev-params.json

# 2. Deploy security layer
aws cloudformation create-stack \
  --stack-name dev-security \
  --template-body file://infrastructure/security/security-groups.yml \
  --parameters file://env/dev-params.json

# 3. Deploy compute layer
aws cloudformation create-stack \
  --stack-name dev-compute \
  --template-body file://infrastructure/compute/ec2-compute.yml \
  --parameters file://env/dev-params.json

# 4. Deploy storage layer
aws cloudformation create-stack \
  --stack-name dev-storage \
  --template-body file://infrastructure/storage/s3-storage.yml \
  --parameters file://env/dev-params.json
```

## 📊 Infrastructure Components

| Component | Resources | Purpose |
|-----------|-----------|---------|
| **Networking** | VPC, Subnets, IGW, Route Tables | Network foundation |
| **Security** | 5 Security Groups | Multi-tier access control |
| **Compute** | 2 EC2 Instances | Web and application servers |
| **Storage** | 5 S3 Buckets | Website, data, logs, backup, templates |

## 💰 Estimated Costs

| Component | Monthly Cost (USD) |
|-----------|-------------------|
| VPC & Networking | $0.00 |
| Security Groups | $0.00 |
| EC2 Instances (2x t3.micro) | ~$15.00 |
| S3 Storage (minimal usage) | ~$1.00 |
| **Total** | **~$16.00** |

*Costs based on us-east-2 region with minimal usage patterns*

## 🛠️ Management Commands

```bash
# Check stack status
aws cloudformation describe-stacks --stack-name dev-networking

# Update existing stack
aws cloudformation update-stack \
  --stack-name dev-networking \
  --template-body file://infrastructure/networking/vpc-stack.yml \
  --parameters file://env/dev-params.json

# Delete stack (reverse order)
aws cloudformation delete-stack --stack-name dev-storage
aws cloudformation delete-stack --stack-name dev-compute
aws cloudformation delete-stack --stack-name dev-security
aws cloudformation delete-stack --stack-name dev-networking
```

## 🔧 Environment Configuration

### Development Environment (`dev-params.json`)
- **Network:** 10.0.0.0/16 CIDR
- **Instance Type:** t3.micro
- **SSH Access:** Open (for learning)
- **Logging:** Enabled

### Production Environment (`prod-params.json`)
- **Network:** 10.1.0.0/16 CIDR
- **Instance Type:** t3.small
- **SSH Access:** Restricted CIDR
- **Enhanced Security:** Stricter configurations

## 📈 Learning Outcomes

This project demonstrates:
- **Infrastructure as Code** fundamentals and best practices
- **AWS CloudFormation** template design and modularization
- **Multi-tier application architecture** patterns
- **AWS networking and security** concepts
- **Production deployment** strategies
- **Version control** for infrastructure
- **Professional documentation** and project organization

## 🚦 Deployment Order

**Important:** Deploy stacks in this order due to dependencies:
1. **Networking** (provides VPC and subnets)
2. **Security** (uses VPC, provides security groups)
3. **Compute** (uses VPC and security groups)
4. **Storage** (independent, can be deployed anytime)

## ⚠️ Important Notes

- **Cost Management:** Remember to stop/terminate EC2 instances when not in use
- **SSH Access:** Update `AllowedSSHCidr` parameter for production environments
- **Key Pairs:** Ensure your EC2 key pair exists in the target region
- **Region Specific:** AMI IDs in templates are region-specific

## 🔍 Troubleshooting

### Common Issues
- **Stack creation fails:** Check CloudFormation Events tab for detailed errors
- **Cross-stack reference errors:** Ensure dependent stacks are deployed first
- **SSH connection issues:** Verify security group rules and key pair
- **Application not accessible:** Check EC2 instance status and security groups

### Useful Commands
```bash
# View stack events
aws cloudformation describe-stack-events --stack-name dev-networking

# Check stack outputs
aws cloudformation describe-stacks --stack-name dev-networking --query 'Stacks[0].Outputs'

# Validate template syntax
aws cloudformation validate-template --template-body file://infrastructure/networking/vpc-stack.yml
```

## 📝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built during AWS Cloud Services learning journey
- Implements enterprise Infrastructure as Code patterns
- Demonstrates modern DevOps practices

---

**⭐ If this repository helped you learn AWS Infrastructure as Code, please give it a star!**