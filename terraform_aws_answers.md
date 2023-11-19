

### 1. Difference between AWS CloudFormation and Terraform:
   - Terraform is a multi-cloud infrastructure provisioning tool, while AWS CloudFormation is specific to AWS and provides a native way to define and deploy infrastructure.

### 2. How Terraform handles AWS resource provisioning and management:
   - Terraform uses declarative configuration files to define and manage AWS resources, creating an execution plan to apply changes efficiently.

### 3. Concept of "Infrastructure as Code" and its significance in AWS and Terraform:
   - Infrastructure as Code (IaC) is the practice of managing infrastructure through machine-readable scripts, providing version control and automation benefits, crucial for AWS and Terraform for consistent and scalable deployments.

### 4. Defining AWS resources in Terraform:
   - Resources are defined using HCL (HashiCorp Configuration Language) syntax in Terraform configuration files, specifying the desired state of AWS infrastructure.

### 5. Purpose of AWS provider in Terraform and its configuration:
   - The AWS provider in Terraform serves as the interface to AWS services, and it is configured with AWS access credentials and region information.

### 6. Terraform authentication and authorization for AWS API calls:
   - Terraform uses AWS access keys or IAM roles for authentication, and authorization is managed through IAM policies associated with these credentials.

### 7. Difference between AWS access keys and IAM roles in Terraform authentication:
   - Access keys are static credentials, while IAM roles provide temporary security credentials with defined permissions, enhancing security in Terraform.

## 8. Significance of Terraform state in managing AWS resources:
   - Terraform state stores the current state of infrastructure and is crucial for tracking changes, enabling Terraform to plan and apply updates accurately.

### 9. Managing and sharing Terraform state in a team:
   - Terraform state can be stored remotely (e.g., in AWS S3) and locked to prevent concurrent modifications, facilitating collaboration and version control in a team.

### 10. Handling AWS resource dependencies and provisioning order in Terraform:
    - Terraform automatically manages dependencies based on resource definitions, ensuring correct provisioning order during execution.

### 11. Purpose of the `terraform init` command in AWS Terraform:
    - `terraform init` initializes a Terraform configuration, downloading required plugins and modules, preparing the environment for subsequent commands.

## 12. Managing multiple AWS environments using Terraform workspaces:
    - Terraform workspaces enable the creation of isolated environments within a single configuration, allowing for efficient management of development, staging, and production environments.

### 13. Creating and managing an AWS VPC with Terraform:
    - A VPC in Terraform is defined using the `aws_vpc` resource, specifying details like CIDR block, subnets, and route tables.

## 14. Provisioning and configuring AWS EC2 instances with Terraform:
    - AWS EC2 instances are defined in Terraform using the `aws_instance` resource, specifying instance type, AMI, and other configurations.

### 15. Difference between AWS Elastic IP and AWS Elastic Network Interface (ENI):
    - An Elastic IP is a static public IP, while an ENI is a virtual network interface that can have both private and public IPs.

### 16. Managing AWS security groups and their rules with Terraform:
    - Security groups are defined using the `aws_security_group` resource in Terraform, specifying inbound and outbound rules for network traffic.

### 17. Provisioning AWS IAM roles and policies with Terraform:
    - Terraform uses `aws_iam_role` and `aws_iam_policy` resources to define IAM roles and policies, enabling fine-grained access control.

### 18. Configuring AWS Auto Scaling groups and launch configurations with Terraform:
    - Terraform defines Auto Scaling groups and launch configurations using `aws_autoscaling_group` and `aws_launch_configuration` resources, facilitating dynamic scaling.

### 19. Provisioning AWS Elastic Load Balancers (ELBs) with Terraform:
    - ELBs are provisioned using the `aws_lb` resource in Terraform, specifying listeners, target groups, and other configurations.

### 20. Purpose of AWS Elastic Beanstalk and managing it with Terraform:
    - AWS Elastic Beanstalk simplifies application deployment and scaling, and Terraform can manage Beanstalk environments through the `aws_elastic_beanstalk_environment` resource.
