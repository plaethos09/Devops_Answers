

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



### 21. Managing AWS Lambda functions and their configurations using Terraform:
   - Explanation: Define Lambda functions and their configurations using `aws_lambda_function` resource in Terraform.
   ```hcl
   resource "aws_lambda_function" "example" {
     function_name = "example-function"
     handler      = "example.handler"
     runtime      = "nodejs14.x"
     # ...other function configurations...
   }
   ```

### 22. Provisioning AWS RDS database instances using Terraform:
   - Explanation: Use `aws_db_instance` resource to provision RDS instances with specified configurations.
   ```hcl
   resource "aws_db_instance" "example" {
     identifier           = "example-db"
     engine               = "mysql"
     allocated_storage    = 20
     # ...other RDS configurations...
   }
   ```

### 23. Purpose of AWS CloudFront, and managing it using Terraform:
   - Explanation: CloudFront is a content delivery network (CDN), and its configurations can be defined using `aws_cloudfront_distribution` resource in Terraform.
   ```hcl
   resource "aws_cloudfront_distribution" "example" {
     # ...CloudFront distribution configurations...
   }
   ```

### 24. Provisioning and configuring AWS S3 buckets and objects using Terraform:
   - Explanation: Define S3 buckets and objects using `aws_s3_bucket` and `aws_s3_bucket_object` resources in Terraform.
   ```hcl
   resource "aws_s3_bucket" "example" {
     # ...S3 bucket configurations...
   }

   resource "aws_s3_bucket_object" "example" {
     # ...S3 object configurations...
   }
   ```

### 25. Provisioning AWS CloudWatch resources and alarms using Terraform:
   - Explanation: Use `aws_cloudwatch_metric_alarm` and other CloudWatch resources to define alarms and configurations.
   ```hcl
   resource "aws_cloudwatch_metric_alarm" "example" {
     # ...CloudWatch alarm configurations...
   }
   ```

### 26. Purpose of AWS Route 53, and managing it using Terraform:
   - Explanation: Route 53 is a DNS web service; use `aws_route53_record` and related resources to define DNS records and configurations.
   ```hcl
   resource "aws_route53_record" "example" {
     # ...Route 53 DNS record configurations...
   }
   ```

### 27. Provisioning and managing AWS ECS clusters and services using Terraform:
   - Explanation: Define ECS clusters and services using `aws_ecs_cluster` and `aws_ecs_service` resources.
   ```hcl
   resource "aws_ecs_cluster" "example" {
     # ...ECS cluster configurations...
   }

   resource "aws_ecs_service" "example" {
     # ...ECS service configurations...
   }
   ```

### 28. Provisioning AWS Elasticache (Redis or Memcached) using Terraform:
   - Explanation: Use `aws_elasticache_cluster` resource to define Elasticache clusters and their configurations.
   ```hcl
   resource "aws_elasticache_cluster" "example" {
     # ...Elasticache cluster configurations...
   }
   ```

### 29. Managing AWS Elastic File System (EFS) using Terraform:
   - Explanation: Define EFS filesystems and mount targets using `aws_efs_file_system` and `aws_efs_mount_target` resources.
   ```hcl
   resource "aws_efs_file_system" "example" {
     # ...EFS filesystem configurations...
   }

   resource "aws_efs_mount_target" "example" {
     # ...EFS mount target configurations...
   }
   ```

### 30. Purpose of AWS Secrets Manager, and integrating it with Terraform:
    - Explanation: Secrets Manager securely stores sensitive information; use `aws_secretsmanager_secret` and related resources for integration.
    ```hcl
    resource "aws_secretsmanager_secret" "example" {
      # ...Secrets Manager secret configurations...
    }
    ```

### 31. Provisioning AWS API Gateway and its resources using Terraform:
    - Explanation: Define API Gateway and its resources using `aws_api_gateway_rest_api` and related resources.
    ```hcl
    resource "aws_api_gateway_rest_api" "example" {
      # ...API Gateway configurations...
    }
    ```

### 32. Provisioning AWS DynamoDB tables and their configurations using Terraform:
    - Explanation: Define DynamoDB tables using `aws_dynamodb_table` resource.
    ```hcl
    resource "aws_dynamodb_table" "example" {
      # ...DynamoDB table configurations...
    }
    ```

### 33. Purpose of AWS CloudTrail, and configuring it with Terraform:
    - Explanation: CloudTrail provides governance, define CloudTrail configurations using `aws_cloudtrail` resource.
    ```hcl
    resource "aws_cloudtrail" "example" {
      # ...CloudTrail configurations...
    }
    ```

### 34. Managing AWS SNS topics and subscriptions using Terraform:
    - Explanation: Define SNS topics and subscriptions using `aws_sns_topic` and `aws_sns_subscription` resources.
    ```hcl
    resource "aws_sns_topic" "example" {
      # ...SNS topic configurations...
    }

    resource "aws_sns_subscription" "example" {
      # ...SNS subscription configurations...
    }
    ```

### 35. Provisioning AWS Kinesis streams and their configurations using Terraform:
    - Explanation: Define Kinesis streams using `aws_kinesis_stream` resource.
    ```hcl
    resource "aws_kinesis_stream" "example" {
      # ...Kinesis stream configurations...
    }
    ```

### 36. Purpose of AWS Glue, and integrating it with Terraform:
    - Explanation: Glue is a fully-managed extract, transform, and load (ETL) service; use `aws_glue_catalog_database` and related resources for integration.
    ```hcl
    resource "aws_glue_catalog_database" "example" {
      # ...Glue database configurations...
    }
    ```

### 37. Provisioning AWS CloudWatch Events and their rules using Terraform:
    - Explanation: Define CloudWatch Events rules using `aws_cloudwatch_event_rule` resource.
    ```hcl
    resource "aws_cloudwatch_event_rule" "example" {
      # ...CloudWatch Events rule configurations...
    }
    ```

### 38. Provisioning AWS Step Functions using Terraform:
    - Explanation: Define Step Functions using `aws_sfn_state_machine` resource.
    ```hcl
    resource "aws_sfn_state_machine" "example" {
      # ...Step Functions configurations...
    }
    ```

### 39. Purpose of AWS Systems Manager, and using it with Terraform:
    - Explanation: Systems Manager automates operational tasks; use `aws_ssm_document` and related resources for integration.
    ```hcl
    resource "aws_ssm_document" "example" {
      # ...Systems Manager document configurations...
    }
    ```

### 40. Provisioning and managing AWS ECR (Elastic Container Registry) using Terraform:


    - Explanation: Define ECR repositories using `aws_ecr_repository` resource.
    ```hcl
    resource "aws_ecr_repository" "example" {
      # ...ECR repository configurations...
    }
    ```


### 41. Provisioning AWS SQS (Simple Queue Service) using Terraform:
   ```hcl
   resource "aws_sqs_queue" "example" {
     name = "example-queue"
     # ...other SQS configurations...
   }
   ```
   - Explanation: Defines an SQS queue named "example-queue" with specified configurations.

### 42. Purpose of AWS X-Ray, and configuring it with Terraform:
   ```hcl
   resource "aws_xray_sampling_rule" "example" {
     rule_name      = "example-rule"
     # ...X-Ray sampling rule configurations...
   }
   ```
   - Explanation: X-Ray provides tracing; configures a sampling rule named "example-rule" using Terraform.

### 43. Provisioning AWS CodePipeline and its stages using Terraform:
   ```hcl
   resource "aws_codepipeline" "example" {
     name     = "example-pipeline"
     role_arn = aws_iam_role.example.arn
     # ...other CodePipeline configurations...

     stage {
       # ...first stage configurations...
     }

     stage {
       # ...second stage configurations...
     }
   }
   ```
   - Explanation: Defines a CodePipeline named "example-pipeline" with stages and associated configurations.

### 44. Provisioning AWS Elasticsearch Service using Terraform:
   ```hcl
   resource "aws_elasticsearch_domain" "example" {
     domain_name           = "example-domain"
     elasticsearch_version = "7.10"
     # ...other Elasticsearch configurations...
   }
   ```
   - Explanation: Defines an Elasticsearch domain named "example-domain" with specified configurations.

### 45. urpose of AWS Data Pipeline, and integrating it with Terraform:
   ```hcl
   resource "aws_datapipeline_pipeline" "example" {
     name     = "example-pipeline"
     # ...Data Pipeline configurations...
   }
   ```
   - Explanation: Data Pipeline orchestrates data workflows; configures a pipeline named "example-pipeline" using Terraform.

### 46. Provisioning AWS CloudFormation stacks using Terraform:
   ```hcl
   resource "aws_cloudformation_stack" "example" {
     name = "example-stack"
     # ...other CloudFormation stack configurations...
   }
   ```
   - Explanation: Defines a CloudFormation stack named "example-stack" with specified configurations.

### 47. Provisioning AWS KMS (Key Management Service) using Terraform:
   ```hcl
   resource "aws_kms_key" "example" {
     description = "example-key"
     # ...other KMS configurations...
   }
   ```
   - Explanation: Defines a KMS key named "example-key" with specified configurations.

### 48. Purpose of AWS Cognito, and configuring it with Terraform:
   ```hcl
   resource "aws_cognito_user_pool" "example" {
     name = "example-pool"
     # ...other Cognito configurations...
   }
   ```
   - Explanation: Cognito manages user identities; configures a user pool named "example-pool" using Terraform.

### 49. Provisioning AWS Redshift clusters using Terraform:
   ```hcl
   resource "aws_redshift_cluster" "example" {
     cluster_identifier = "example-cluster"
     # ...other Redshift configurations...
   }
   ```
   - Explanation: Defines a Redshift cluster named "example-cluster" with specified configurations.

### 50. Provisioning AWS Secrets Manager using Terraform:
    ```hcl
    resource "aws_secretsmanager_secret" "example" {
      name = "example-secret"
      # ...other Secrets Manager configurations...
    }
    ```
    - Explanation: Defines a Secrets Manager secret named "example-secret" with specified configurations.

### 51. Purpose of AWS Batch, and managing it using Terraform:
    ```hcl
    resource "aws_batch_compute_environment" "example" {
      compute_environment_name = "example-environment"
      # ...other Batch configurations...
    }
    ```
    - Explanation: AWS Batch runs batch computing workloads; configures a compute environment using Terraform.

### 52. Provisioning AWS Certificate Manager (ACM) using Terraform:
    ```hcl
    resource "aws_acm_certificate" "example" {
      domain_name = "example.com"
      # ...other ACM configurations...
    }
    ```
    - Explanation: Defines an ACM certificate for the domain "example.com" with specified configurations.

### 53. Provisioning AWS Transit Gateway using Terraform:
    ```hcl
    resource "aws_ec2_transit_gateway" "example" {
      # ...Transit Gateway configurations...
    }
    ```
    - Explanation: Defines a Transit Gateway with specified configurations using Terraform.

### 54. Purpose of AWS CodeBuild, and configuring it with Terraform:
    ```hcl
    resource "aws_codebuild_project" "example" {
      name = "example-project"
      # ...other CodeBuild configurations...
    }
    ```
    - Explanation: CodeBuild compiles source code; configures a project named "example-project" using Terraform.

### 55. Provisioning AWS CloudWatch Logs using Terraform:
    ```hcl
    resource "aws_cloudwatch_log_group" "example" {
      name = "/example/log/group"
      # ...other CloudWatch Logs configurations...
    }
    ```
    - Explanation: Defines a CloudWatch Logs group named "/example/log/group" with specified configurations.

### 66. Provisioning AWS S3 Glacier using Terraform:
    ```hcl
    resource "aws_glacier_vault" "example" {
      name = "example-vault"
      # ...other S3 Glacier configurations...
    }
    ```
    - Explanation: Defines an S3 Glacier vault named "example-vault" with specified configurations.

### 67. Purpose of AWS AppSync, and configuring it with Terraform:
    ```hcl
    resource "aws_appsync_graphql_api" "example" {
      name = "example-api"
      # ...other AppSync configurations...
    }
    ```
    - Explanation: AppSync simplifies development of GraphQL APIs; configures an API named "example-api" using Terraform.

### 68. Provisioning AWS Glue Data Catalog using Terraform:
    ```hcl
    resource "aws_glue_catalog_database" "example" {
      name = "example-database"
      # ...other Glue Data Catalog configurations...
    }
    ```
    - Explanation: Defines a Glue Data Catalog database named "example-database" with specified configurations.

### 69. Provisioning AWS WAF (Web Application Firewall) using Terraform:
    ```hcl
    resource "aws_wafv2_web_acl" "example" {
      name = "example-web-acl"
      # ...other WAF configurations...
    }
    ```
    - Explanation: Defines a WAFv2 web ACL named "example-web-acl" with specified configurations.

### 70. Purpose of AWS IoT Core, and integrating it with Terraform:
    ```hcl
    resource "aws_iot_core_endpoint" "example" {
      endpoint_type = "iot:Data-ATS"
      # ...other IoT Core configurations...
    }
    ```


### 71. Provisioning AWS Config using Terraform:
   ```hcl
   resource "aws_config_configuration_recorder" "example" {
     name     = "example-recorder"
     role_arn = aws_iam_role.example.arn
     # ...other AWS Config configurations...
   }
   ```
   - Explanation: Defines an AWS Config recorder named "example-recorder" with specified configurations.

### 72. Provisioning AWS App Runner using Terraform:
   ```hcl
   resource "aws_apprunner_service" "example" {
     service_name = "example-app-runner-service"
     # ...other App Runner configurations...
   }
   ```
   - Explanation: Defines an App Runner service named "example-app-runner-service" with specified configurations.

### 73. Purpose of AWS Lex, and configuring it with Terraform:
   ```hcl
   resource "aws_lex_bot" "example" {
     name = "example-lex-bot"
     # ...other Lex bot configurations...
   }
   ```
   - Explanation: Lex is for building conversational interfaces; configures a Lex bot named "example-lex-bot" using Terraform.

### 74. Provisioning AWS CloudFormation StackSets using Terraform:
   ```hcl
   resource "aws_cloudformation_stack_set" "example" {
     name = "example-stack-set"
     # ...other StackSet configurations...
   }
   ```
   - Explanation: Defines a CloudFormation StackSet named "example-stack-set" with specified configurations.

### 75. Provisioning AWS Service Catalog using Terraform:
   ```hcl
   resource "aws_servicecatalog_portfolio" "example" {
     name = "example-portfolio"
     # ...other Service Catalog configurations...
   }
   ```
   - Explanation: Defines a Service Catalog portfolio named "example-portfolio" with specified configurations.

### 76. Purpose of AWS Amplify, and configuring it with Terraform:
   ```hcl
   resource "aws_amplify_app" "example" {
     name = "example-amplify-app"
     # ...other Amplify app configurations...
   }
   ```
   - Explanation: Amplify is for building scalable web applications; configures an Amplify app named "example-amplify-app" using Terraform.

### 77. **Provisioning AWS CloudFront distributions using Terraform:**
   ```hcl
   resource "aws_cloudfront_distribution" "example" {
     # ...CloudFront distribution configurations...
   }
   ```
   - Explanation: Defines a CloudFront distribution with specified configurations using Terraform.

### 78. Provisioning AWS Elastic Transcoder using Terraform:
   ```hcl
   resource "aws_elastictranscoder_pipeline" "example" {
     name = "example-pipeline"
     # ...other Elastic Transcoder configurations...
   }
   ```
   - Explanation: Defines an Elastic Transcoder pipeline named "example-pipeline" with specified configurations.

### 79. Purpose of AWS Budgets, and managing them using Terraform:
   ```hcl
   resource "aws_budgets_budget" "example" {
     budget_name  = "example-budget"
     # ...other AWS Budgets configurations...
   }
   ```
   - Explanation: Budgets help control AWS costs; configures a budget named "example-budget" using Terraform.

### 80. Provisioning AWS API Gateway custom domain names using Terraform:
    ```hcl
    resource "aws_apigatewayv2_domain_name" "example" {
      domain_name = "example-api-gateway-domain"
      # ...other API Gateway custom domain configurations...
    }
    ```
    - Explanation: Defines an API Gateway custom domain named "example-api-gateway-domain" with specified configurations.

### 81. Provisioning AWS DataSync using Terraform:
    ```hcl
    resource "aws_datasync_location_s3" "example" {
      # ...DataSync S3 location configurations...
    }
    ```
    - Explanation: Defines a DataSync S3 location with specified configurations using Terraform.

### 82. Purpose of AWS Fargate, and managing it using Terraform:
    ```hcl
    resource "aws_ecs_task_definition" "example" {
      # ...ECS task definition configurations...
    }
    ```
    - Explanation: Fargate is for running containers without managing infrastructure; configures an ECS task definition using Terraform.

### 83. Provisioning AWS Glue ETL (Extract, Transform, Load) jobs using Terraform:
    ```hcl
    resource "aws_glue_job" "example" {
      name = "example-etl-job"
      # ...other Glue ETL job configurations...
    }
    ```
    - Explanation: Defines a Glue ETL job named "example-etl-job" with specified configurations.

### 84.Provisioning AWS Network Firewall using Terraform:
    ```hcl
    resource "aws_networkfirewall_firewall" "example" {
      name = "example-firewall"
      # ...other Network Firewall configurations...
    }
    ```
    - Explanation: Defines a Network Firewall named "example-firewall" with specified configurations using Terraform.

### 85. Purpose of AWS Lake Formation, and configuring it with Terraform:
    ```hcl
    resource "aws_lakeformation_data_lake_settings" "example" {
      # ...Lake Formation data lake settings configurations...
    }
    ```
    - Explanation: Lake Formation simplifies data lake setup; configures data lake settings using Terraform.

### 86. Provisioning AWS SimpleDB using Terraform:
    ```hcl
    resource "aws_sdb_domain" "example" {
      name = "example-simpledb-domain"
      # ...other SimpleDB configurations...
    }
    ```
    - Explanation: Defines a SimpleDB domain named "example-simpledb-domain" with specified configurations.

### 87. Provisioning AWS Storage Gateway using Terraform:
    ```hcl
    resource "aws_storagegateway_gateway" "example" {
      gateway_name = "example-gateway"
      # ...other Storage Gateway configurations...
    }
    ```
    - Explanation: Defines a Storage Gateway named "example-gateway" with specified configurations.

### 88. Purpose of AWS Security Hub, and integrating it with Terraform:
    ```hcl
    resource "aws_securityhub_account" "example" {
      # ...Security Hub account configurations...
    }
    ```
    - Explanation: Security Hub provides a comprehensive view of security; configures Security Hub account settings using Terraform.

### 89.Provisioning AWS RoboMaker resources using Terraform:
    ```hcl
    resource "aws_robomaker_simulation_application" "example" {
      name = "example-simulation-app"
      # ...other RoboMaker configurations...
    }
    ```
    - Explanation: Defines a RoboMaker simulation application named "example-simulation-app" with specified configurations.

### 90.Provisioning AWS GameLift using Terraform:
    ```hcl
    resource "aws_gamelift_fleet" "example" {
      name = "example-game-fleet"
      # ...other GameLift configurations...
    }
    ```
    - Explanation: Defines a GameLift fleet named "example-game-fleet" with specified configurations using Terraform.
