**\========================================**  
**CATEGORY 8: INFRASTRUCTURE AS CODE**  
**\========================================**

**8.1 TERRAFORM FUNDAMENTALS:**

**/\* COMMENT: Terraform enables infrastructure provisioning using declarative code.**  
   **It supports multiple cloud providers and maintains state to track resources.**  
   **Understanding HCL syntax and state management is crucial. \*/**

**KEY CONCEPTS:**  
**• HCL (HashiCorp Configuration Language): Terraform's language**  
**• State File: Tracks current infrastructure state**  
**• Providers: Plugins for cloud platforms (AWS, Azure, GCP)**  
**• Resources: Infrastructure components to manage**  
**• Modules: Reusable infrastructure code**

**TERRAFORM MAIN EXAMPLE:**  
**terraform {**  
  **required\_version \= "\>= 1.0"**  
  **required\_providers {**  
    **aws \= {**  
      **source  \= "hashicorp/aws"**  
      **version \= "\~\> 5.0"**  
    **}**  
  **}**  
  **backend "s3" {**  
    **bucket \= "terraform-state-bucket"**  
    **key    \= "prod/terraform.tfstate"**  
    **region \= "us-east-1"**  
  **}**  
**}**

**provider "aws" {**  
  **region \= var.aws\_region**  
**}**

**resource "aws\_vpc" "main" {**  
  **cidr\_block \= "10.0.0.0/16"**  
    
  **tags \= {**  
    **Name \= "main-vpc"**  
    **Environment \= var.environment**  
  **}**  
**}**

**resource "aws\_subnet" "public" {**  
  **vpc\_id     \= aws\_vpc.main.id**  
  **cidr\_block \= "10.0.1.0/24"**  
    
  **tags \= {**  
    **Name \= "public-subnet"**  
  **}**  
**}**

**VARIABLES FILE:**  
**variable "aws\_region" {**  
  **description \= "AWS region"**  
  **type        \= string**  
  **default     \= "us-east-1"**  
**}**

**variable "environment" {**  
  **description \= "Environment name"**  
  **type        \= string**  
**}**

**COMMON COMMANDS:**  
**terraform init          \# Initialize working directory**  
**terraform plan          \# Show execution plan**  
**terraform apply         \# Apply changes**  
**terraform destroy       \# Destroy infrastructure**  
**terraform validate      \# Validate configuration**  
**terraform fmt           \# Format code**  
**terraform state list    \# List resources in state**

**BEST PRACTICES:**  
**• Use remote state backend (S3, Terraform Cloud)**  
**• Implement state locking to prevent conflicts**  
**• Use modules for reusable components**  
**• Version your Terraform and provider versions**  
**• Separate environments (dev, staging, prod)**  
**• Use workspaces or separate state files per environment**

**8.2 CLOUDFORMATION:**

**/\* COMMENT: AWS CloudFormation is AWS's native IaC service using JSON or YAML.**  
   **It provides deep AWS integration and automatic rollback on failures.**  
   **Understanding stacks, templates, and change sets is essential. \*/**

**KEY CONCEPTS:**  
**• Templates: JSON/YAML files defining resources**  
**• Stacks: Deployed instances of templates**  
**• Change Sets: Preview changes before applying**  
**• Parameters: Input values for templates**  
**• Outputs: Values exported from stack**

**CLOUDFORMATION TEMPLATE EXAMPLE:**  
**AWSTemplateFormatVersion: '2010-09-09'**  
**Description: 'VPC with public and private subnets'**

**Parameters:**  
  **EnvironmentName:**  
    **Type: String**  
    **Description: Environment name**  
    
  **VpcCIDR:**  
    **Type: String**  
    **Default: 10.0.0.0/16**

**Resources:**  
  **VPC:**  
    **Type: AWS::EC2::VPC**  
    **Properties:**  
      **CidrBlock: \!Ref VpcCIDR**  
      **EnableDnsHostnames: true**  
      **Tags:**  
        **\- Key: Name**  
          **Value: \!Ref EnvironmentName**  
    
  **InternetGateway:**  
    **Type: AWS::EC2::InternetGateway**  
    **Properties:**  
      **Tags:**  
        **\- Key: Name**  
          **Value: \!Ref EnvironmentName**  
    
  **InternetGatewayAttachment:**  
    **Type: AWS::EC2::VPCGatewayAttachment**  
    **Properties:**  
      **InternetGatewayId: \!Ref InternetGateway**  
      **VpcId: \!Ref VPC**  
    
  **PublicSubnet:**  
    **Type: AWS::EC2::Subnet**  
    **Properties:**  
      **VpcId: \!Ref VPC**  
      **CidrBlock: 10.0.1.0/24**  
      **MapPublicIpOnLaunch: true**

**Outputs:**  
  **VPCId:**  
    **Description: VPC ID**  
    **Value: \!Ref VPC**  
    **Export:**  
      **Name: \!Sub ${EnvironmentName}-VPCID**

**COMMON CLI COMMANDS:**  
**aws cloudformation create-stack \--stack-name mystack \--template-body file://template.yml**  
**aws cloudformation update-stack \--stack-name mystack \--template-body file://template.yml**  
**aws cloudformation delete-stack \--stack-name mystack**  
**aws cloudformation describe-stacks \--stack-name mystack**  
**aws cloudformation validate-template \--template-body file://template.yml**

**BEST PRACTICES:**  
**• Use nested stacks for complex infrastructures**  
**• Implement proper IAM roles for CloudFormation**  
**• Use change sets to preview changes**  
**• Version control your templates**  
**• Use parameters and mappings for flexibility**
