**════════════════════════════════════════════════════════════════════**  
**CATEGORY 5: CLOUD PLATFORMS (AWS & AZURE)**  
**════════════════════════════════════════════════════════════════════**

**Covering: 8 articles on AWS IAM, VPC, Auto Scaling, EC2, Azure VMs, CLI commands, and DevOps service maps**

**/\* COMMENT: Cloud platforms are the foundation of modern infrastructure. AWS and Azure**  
   **dominate the market. Understanding core services, networking, IAM, and CLI tools**  
   **is essential for DevOps and cloud engineering roles. \*/**

**5.1 AWS FUNDAMENTALS:**

**CORE AWS SERVICES FOR DEVOPS:**

**Compute:**  
**● EC2: Virtual servers**  
**● Lambda: Serverless compute**  
**● ECS/EKS: Container orchestration**  
**● Auto Scaling: Automatic scaling**

**Storage:**  
**● S3: Object storage**  
**● EBS: Block storage for EC2**  
**● EFS: Elastic file system**

**Networking:**  
**● VPC: Virtual Private Cloud**  
**● Route 53: DNS service**  
**● CloudFront: CDN**  
**● Elastic Load Balancing: Traffic distribution**

**Databases:**  
**● RDS: Managed relational databases**  
**● DynamoDB: NoSQL database**  
**● ElastiCache: In-memory cache**

**DevOps Tools:**  
**● CodePipeline: CI/CD**  
**● CodeBuild: Build service**  
**● CodeDeploy: Deployment automation**  
**● CloudFormation: Infrastructure as Code**

**Monitoring & Logging:**  
**● CloudWatch: Monitoring and logging**  
**● X-Ray: Distributed tracing**  
**● CloudTrail: Audit logs**

**Security:**  
**● IAM: Identity and Access Management**  
**● Secrets Manager: Secret storage**  
**● KMS: Key Management Service**

**AWS CLI ESSENTIAL COMMANDS:**

**\# Configure AWS CLI**  
**aws configure**  
**\# Enter: Access Key, Secret Key, Region, Output format**

**\# EC2**  
**aws ec2 describe-instances**  
**aws ec2 start-instances \--instance-ids i-1234567890abcdef0**  
**aws ec2 stop-instances \--instance-ids i-1234567890abcdef0**  
**aws ec2 create-tags \--resources i-1234567890abcdef0 \--tags Key=Name,Value=WebServer**

**\# S3**  
**aws s3 ls**  
**aws s3 cp file.txt s3://mybucket/**  
**aws s3 sync ./local/ s3://mybucket/**  
**aws s3 mb s3://mynewbucket**  
**aws s3 rb s3://mybucket \--force**

**\# IAM**  
**aws iam list-users**  
**aws iam create-user \--user-name newuser**  
**aws iam attach-user-policy \--user-name newuser \--policy-arn arn:aws:iam::aws:policy/ReadOnlyAccess**

**\# Lambda**  
**aws lambda list-functions**  
**aws lambda invoke \--function-name myfunction output.json**

**\# CloudFormation**  
**aws cloudformation create-stack \--stack-name mystack \--template-body file://template.yaml**  
**aws cloudformation describe-stacks \--stack-name mystack**  
**aws cloudformation delete-stack \--stack-name mystack**

**5.2 AWS VPC ARCHITECTURE:**

**/\* COMMENT: VPC is fundamental to AWS networking. Understanding subnets, route tables,**  
   **security groups, and NACLs is crucial for secure, scalable architectures. \*/**

**VPC COMPONENTS:**

**● Subnets: Public (internet-facing) and Private (internal)**  
**● Internet Gateway: Connects VPC to internet**  
**● NAT Gateway: Allows private subnets to access internet**  
**● Route Tables: Define traffic routing**  
**● Security Groups: Stateful firewalls (instance level)**  
**● Network ACLs: Stateless firewalls (subnet level)**  
**● VPC Peering: Connect VPCs**
