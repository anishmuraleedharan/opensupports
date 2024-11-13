# OpenSupports Deployment with AWS CloudFormation and GitHub Actions

This project sets up a multi-environment deployment for the OpenSupports application using AWS CloudFormation and GitHub Actions.

## Prerequisites
1. AWS account with IAM roles set up for CI/CD.
2. EC2 Key Pair (`your-key-pair.pem`) configured for SSH access.
3. GitHub repository forked from [OpenSupports](https://github.com/opensupports/opensupports).

## CloudFormation Templates

- **main_infrastructure.yml**: Sets up VPC, EC2, RDS, S3, Security Groups.
- **cloudwatch_logs.yml**: Configures CloudWatch logging.

## CI/CD Pipeline

The GitHub Actions workflow (`.github/workflows/deployment.yml`) automates deployment to AWS.

- **Branches**:
  - `develop`: Deploys to development.
  - `main`: Deploys to production.

### Pipeline Steps

1. **Build**: Validates application setup.
2. **Deploy to AWS**: Deploys EC2, RDS, S3, and other resources via CloudFormation.
3. **Run Application**: Sets up OpenSupports on EC2 instance.

## Best Practices

- **Security**: IAM roles, Security Groups with least privileges.
- **Cost Optimization**: Use Auto Scaling for production, Spot Instances for non-production.

## Usage

- Push to `develop` branch to deploy to the development environment.
- Push to `main` branch to deploy to production.
