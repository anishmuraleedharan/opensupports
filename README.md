# OpenSupports Deployment with AWS CloudFormation and GitHub Actions

This project sets up a multi-environment deployment for the OpenSupports application using AWS CloudFormation and GitHub Actions.

## Prerequisites
1. AWS account with necessary permissions to create the resources

## CloudFormation Templates

- **infra/infrastructure.yml**: Use this template via CLI or Console to deploy multiple environments. Change the necessary parameters. After the stack is deployed the Key Pair for EC2 instance will be stored in the parameter store.

- Spot instances will be used by default. For prod environment update the necessary parameter value.

- Instance will be launched with public IP address and HTTP access from everywhere.

## CI/CD Pipeline

The GitHub Actions workflow (`.github/workflows/deployment.yml`) automates deployment to AWS.

- **Update the Secrets for each environment in the repo settings**
- **Deployment strategy based  on Branches**
  - `develop`: Deploys to development.
  - `staging`: Deploys to staging
  - `main`: Deploys to production.


### Pipeline Steps

1. Based on the branch connects to each environment's EC2 via SSH
2. Commands are passed via SSH to download the opensupports package, necessary dependencies, and install it. 
3. Uses init commandsto configure OpenSupports.

## Recommended Next Steps

  - Move the instance from public subnet to private subnet.
  - Add ALB and allow traffic to instance from ALB only.
  - Remove SSH from EC2 & Use SSM only for connecting.
  - Once SSH is removed, update the `.github/workflows/deployment.yml`. Use AWS CodeDeploy to deploy the app.
  - Configure Cloudwatch agent to push the addintonal metrics & app logs to cloudwatch.
  - Create autoscaling based on metrics or schedule to meet the traffic requirements.
  - Add WAF infront of ALB for additonal security.

