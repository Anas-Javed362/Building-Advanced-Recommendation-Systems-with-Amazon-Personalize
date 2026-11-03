# Infrastructure as Code for Amazon Personalize Recommendation Systems

Infrastructure as Code (IaC) implementations for building advanced recommendation systems using Amazon Personalize.

## Overview

This project provides multiple infrastructure deployment options for a recommendation system, including model training, real-time recommendations, batch inference, automated retraining, and monitoring.

## Available Implementations

- AWS CloudFormation
- AWS CDK with TypeScript
- AWS CDK with Python
- Terraform
- Bash deployment scripts

## Architecture

The infrastructure includes:

- **Data Storage:** Amazon S3 for training data, metadata, and inference outputs.
- **ML Training:** Amazon Personalize dataset groups, schemas, and recommendation solutions.
- **Inference:** Real-time campaigns and batch inference.
- **API Layer:** AWS Lambda and API Gateway for recommendation delivery.
- **Automation:** EventBridge for scheduled model retraining.
- **Monitoring:** CloudWatch metrics, dashboards, and alerts.

### Recommendation Strategies

- User Personalization
- Similar Items
- Trending Now
- Popularity Count

## Prerequisites

- AWS CLI v2 configured with appropriate permissions
- AWS account with access to Amazon Personalize, S3, Lambda, IAM, EventBridge, and CloudWatch
- Historical interaction data
- Node.js for CDK TypeScript
- Python for CDK Python
- Terraform 1.0+ for Terraform deployment

**Estimated AWS cost:** $200–$500/month, depending on usage and deployment configuration.

## Deployment

### CloudFormation

```bash
aws cloudformation create-stack \
  --stack-name personalize-recommendation-system \
  --template-body file://cloudformation.yaml \
  --capabilities CAPABILITY_IAM
```

### CDK TypeScript

```bash
cd cdk-typescript
npm install
cdk bootstrap
cdk deploy PersonalizeRecommendationStack
```

### CDK Python

```bash
cd cdk-python
pip install -r requirements.txt
cdk bootstrap
cdk deploy PersonalizeRecommendationStack
```

### Terraform

```bash
cd terraform
terraform init
terraform plan
terraform apply
```

### Bash Scripts

```bash
chmod +x scripts/deploy.sh scripts/destroy.sh
./scripts/deploy.sh
```

## Data Requirements

### Interactions Dataset

```csv
USER_ID,ITEM_ID,TIMESTAMP,EVENT_TYPE,EVENT_VALUE
user_001,item_001,1609459200,view,1
user_001,item_002,1609459260,purchase,5
```

### Items Metadata

```csv
ITEM_ID,CATEGORY,PRICE,BRAND,CREATION_TIMESTAMP
item_001,electronics,299.99,BrandA,1609459200
```

### Users Metadata

```csv
USER_ID,AGE,GENDER,MEMBERSHIP_TYPE
user_001,25,M,premium
```

## API Endpoints

| Endpoint | Description |
|---|---|
| `GET /recommendations/{userId}` | Personalized recommendations |
| `GET /recommendations/{userId}?type=similar_items&itemId={itemId}` | Similar items |
| `GET /recommendations/{userId}?type=trending_now` | Trending recommendations |
| `GET /recommendations/{userId}?type=popularity` | Popular items |
| `GET /recommendations/{userId}?category={category}` | Category-based recommendations |
| `GET /recommendations/{userId}?minPrice={min}&maxPrice={max}` | Price-filtered recommendations |

## Monitoring

Amazon CloudWatch provides:

- Recommendation request metrics
- API response time monitoring
- A/B testing performance
- Model training status
- Campaign utilization
- Error and cost alerts

## Security

- IAM roles and policies
- S3 encryption at rest
- Optional VPC integration
- S3 access logging
- API Gateway throttling and API key support

## Cost Optimization

- Use minimum campaign TPS in development.
- Prefer batch inference for bulk recommendations.
- Configure S3 lifecycle policies.
- Monitor AWS usage and billing alerts.

## Cleanup

Destroy deployed resources when no longer required.

### CloudFormation

```bash
aws cloudformation delete-stack \
  --stack-name personalize-recommendation-system
```

### CDK

```bash
cdk destroy PersonalizeRecommendationStack
```

### Terraform

```bash
terraform destroy
```

### Bash

```bash
./scripts/destroy.sh
```

## Technologies

- AWS Amazon Personalize
- AWS Lambda
- Amazon S3
- Amazon API Gateway
- AWS CloudFormation
- AWS CDK
- Terraform
- Amazon CloudWatch
- Python
- TypeScript

## Documentation

- [Amazon Personalize](https://docs.aws.amazon.com/personalize/)
- [AWS CDK](https://docs.aws.amazon.com/cdk/)
- [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/)
- [AWS CloudFormation](https://docs.aws.amazon.com/cloudformation/)

## License

Refer to the repository's LICENSE file for licensing information.
