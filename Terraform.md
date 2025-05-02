                    ================= Terraform Interview Questions ===================

1. Resources already exists in the Cloud, so how to configure it with terraform ?
2. What is back end in Terraform.
3. In terraform you create and automate but somebody manually change the file or Resources how do you troubleshoot ?
4. In Terraform you create Ec2 instance 1 then you want to create 10 instance how do create ?
5. Terraform Directory Structure?
6. what is state file in Terrform?
7. Locals in Terraform?
8. Variables in Terraform (Input, Output)?
9. How you can create an storage account in three different location with three different Name?
10. How do you import manually created AWS resources into Terraform?
11. Why should we run terraform plan before terraform apply?
12. What happens if cloud infrastructure changes between terraform plan and terraform apply?
13. If a Virtual Machine is already exists and you write the same Terraform configuration, what happens when you run Terraform commands?
14. What is terraform taint?
15. What is terraform user data ?
16. What is terraform workspace ?
17. How will you configure Terraform to use AWS?
18. Write a Terraform script to create an EC2 instance and install a web server.
19. 


                                  ## Scenario Based Question & Answers ##
## Q1: What happens if your state file is accidentally deleted?
**A**: Terraform loses track of all managed infrastructure. On next apply, it will attempt to recreate everything from scratch, potentially causing conflicts with existing resources.

## Q2) What happens if multiple team members run terraform apply simultaneously?
**A**: State file locking fails, risking corrupted state and inconsistent infrastructure. One process succeeds while others error out, potentially leading to drift if not managed properly.

 ## Q3) What happens if a resource fails halfway through a terraform apply?
**A**: Terraform leaves successfully created resources running but marks the state as tainted. Subsequent apply operations will attempt to recreate failed resources, but you're left in partial state.

## Q4) What happens when AWS API rate limits are hit during a large terraform apply?
**A**: Operations fail with throttling errors. Terraform retries a few times then fails the apply. Resources created before the limit was hit remain, creating partial deployments.

## Q5) What happens if terraform plan shows no changes but infrastructure was modified outside Terraform?
**A**: Terraform won't detect the drift until you run terraform refresh or terraform plan -refresh-only. This can lead to unexpected behavior when making future changes.

## Q6) What happens if you delete a resource definition from your configuration?
**A**: On next apply, Terraform will destroy that resource in your infrastructure unless you use terraform state rm to remove it from state first or use lifecycle { prevent_destroy = true }.

## Q7) What happens if a provider API changes between Terraform versions?
**A**: You may encounter compatibility issues and failed plans/applies. Resources might need to be rebuilt or configurations updated to match new API requirements.

## Q8) What happens if you have circular dependencies in your Terraform modules?
**A**: Terraform will fail to initialize or plan with dependency cycle errors. You'll need to refactor your module structure to break the circular references.

## Q9) What happens if you exceed AWS service quotas during deployment?
**A**: Resources will fail to create with quota exceeded errors. Terraform marks them as failed, and you'll need to request quota increases before retrying the apply.

## Q10) What happens if you lose access to the remote backend storing your state?
**A**: All Terraform operations fail until access is restored. Teams can't collaborate, and changes can't be applied safely. This effectively blocks all infrastructure changes.

## Q11: Why do we use the Kubernetes provider in Terraform when we already have EKS in AWS or AKS in Azure?
**A**: EKS and AKS are managed Kubernetes services, but they only provide the control plane. To manage Kubernetes resources (like deployments, services, and config maps) within the cluster, we use the Kubernetes provider in Terraform. It allows us to define and manage cluster resources declaratively, ensuring consistency and automation in infrastructure provisioning.

## Q12: What is the difference between Terraform count and for_each?
**A**: count is used when you need to create multiple identical resources. It works with lists and numerical values.
for_each is used when you need to create resources dynamically from a map or a set, ensuring better control and flexibility. Use count for simple replication and for_each for more complex configurations.

## Q13: How does Terraform handle state management, and why is it important? 
**A**: Terraform uses a state file (terraform.tfstate) to track the real-world infrastructure and manage updates efficiently. 
The state file helps:
✅ Maintain resource dependencies
✅ Speed up plan and apply processes
✅ Avoid resource duplication
For team collaboration, it's recommended to store state remotely (e.g., AWS S3, Azure Blob Storage, or Terraform Cloud) to prevent conflicts.

## Q14: What is the purpose of terraform import, and how does it work?
**A**: Terraform import allows Terraform to take control of existing infrastructure that wasn’t originally created using Terraform. It brings external resources into the Terraform state but does not generate the corresponding configuration files automatically.
To complete the process, you need to manually define the resource in your .tf files.

## Q15: How can you prevent accidental deletions of resources in Terraform?
**A**:  You can use the prevent_destroy lifecycle rule in Terraform to ensure critical resources are not deleted accidentally.
``resource "aws_s3_bucket" "example" {
 bucket = "my-important-bucket"

 lifecycle {
 prevent_destroy = true
 }
}``
This ensures that even if a terraform destroy or a change attempts to delete the resource, Terraform will throw an error, protecting essential infrastructure.

---



## ✅ Terraform

**Q1**. **How do you use Terraform for multiple regions?**
  - To manage resources in multiple regions with Terraform:
    - Define provider blocks for each region.
    - Use the `provider` block with the `region` argument to specify the region.
    - Example:
      ```hcl
      provider "aws" {
        region = "us-east-1"
      }

      provider "aws" {
        region = "us-west-2"
        alias  = "west"
      }

      resource "aws_instance" "east_instance" {
        provider = aws
        ami           = "ami-0c55b159cbfafe1f0"
        instance_type = "t2.micro"
      }

      resource "aws_instance" "west_instance" {
        provider = aws.west
        ami           = "ami-0c55b159cbfafe1f0"
        instance_type = "t2.micro"
      }
      ```

**Q2**. **Terraform modules: purpose and usage.**
  - **Modules** in Terraform are containers for multiple resources that are used together. They allow for the reuse of configuration across multiple projects or environments.
  - **Purpose**:
    - **Reusability**: Encapsulates resources to make them reusable.
    - **Organization**: Helps in logically grouping resources.
    - **Maintainability**: Easier to maintain and update infrastructure.
  - **Usage**:
    - To use a module, define a `module` block in your Terraform configuration:
      ```hcl
      module "vpc" {
        source = "terraform-aws-modules/vpc/aws"
        name   = "my-vpc"
        cidr   = "10.0.0.0/16"
      }
      ```

**Q3**. **Difference between Terraform and Boto3?**
  - **Terraform**:
    - Terraform is an infrastructure-as-code tool that allows you to define and provision infrastructure across multiple cloud providers in a declarative manner.
    - It supports multiple providers (AWS, Azure, Google Cloud, etc.) and focuses on managing infrastructure lifecycle.
    - Terraform is declarative, where you define the desired end state, and it automatically manages resources.
  - **Boto3**:
    - Boto3 is a Python SDK for AWS, which provides programmatic access to AWS services.
    - It is imperative, meaning you specify the exact steps to achieve a desired state (e.g., creating EC2 instances).
    - Boto3 is specific to AWS and is used for scripting and automation using Python.

**Q4**. **What modules have you used?**
  - Common modules used in Terraform for AWS include:
    - **VPC module**: To create VPCs, subnets, route tables, and related resources.
    - **EC2 module**: To manage EC2 instances, security groups, and EBS volumes.
    - **S3 module**: To create and manage S3 buckets.
    - **IAM module**: To manage IAM roles, policies, and users.
    - **Security Group module**: To configure security groups and associated rules.
  - Example:
    ```hcl
    module "vpc" {
      source = "terraform-aws-modules/vpc/aws"
      name   = "my-vpc"
      cidr   = "10.0.0.0/16"
    }
    ```

**Q5**. **How do you lock Terraform state files?**
  - **State locking** ensures that only one process can modify the state at a time, preventing race conditions and conflicts.
  - **Backend configuration** like S3 with DynamoDB can be used to lock Terraform state files:
    ```hcl
    terraform {
      backend "s3" {
        bucket         = "my-terraform-state"
        key            = "path/to/state.tfstate"
        region         = "us-east-1"
        encrypt        = true
        dynamodb_table = "my-lock-table"
      }
    }
    ```
  - DynamoDB table is used to provide state locking and consistency.

**Q6**. **Terraform init, plan, apply commands?**
  - **terraform init**: Initializes a Terraform working directory by downloading the necessary provider plugins and initializing the backend.
  - **terraform plan**: Creates an execution plan by comparing the current state of infrastructure with the desired state in the configuration files. It shows the changes Terraform will apply.
  - **terraform apply**: Applies the changes required to reach the desired state of the configuration.

**Q7**. **What happens if the state file is deleted?**
  - If the Terraform state file is deleted:
    - Terraform loses track of the resources it previously managed.
    - It will not know the current state of the infrastructure, and as a result, any future runs of `terraform plan` or `terraform apply` will treat the infrastructure as "new" and might attempt to recreate resources.
    - It is essential to back up the state file, especially in team environments, to avoid losing the current state.

**Q8**. **Backend configuration in Terraform?**
  - A **backend** in Terraform defines where the Terraform state is stored.
  - The backend is responsible for storing and managing state files, ensuring state consistency and enabling features like state locking.
  - Example configuration for using an S3 backend with DynamoDB for state locking:
    ```hcl
    terraform {
      backend "s3" {
        bucket         = "my-terraform-state"
        key            = "path/to/state.tfstate"
        region         = "us-east-1"
        encrypt        = true
        dynamodb_table = "my-lock-table"
      }
    }
    ```

**Q9**. **Resources provisioned using Terraform?**
  - Terraform can provision a wide range of infrastructure resources, including:
    - **Compute resources**: EC2 instances, autoscaling groups, Lambda functions.
    - **Networking**: VPC, subnets, security groups, route tables.
    - **Storage**: S3 buckets, EBS volumes, Glacier.
    - **Identity and Access Management (IAM)**: Users, roles, policies.
    - **Databases**: RDS instances, DynamoDB tables, Aurora clusters.

**Q10**. **What happens if EC2s are manually deleted?**
  - If EC2 instances managed by Terraform are manually deleted:
    - The next `terraform apply` will see the instance as "missing" and will attempt to recreate it.
    - Terraform maintains state files, so manual deletions can lead to discrepancies between the actual infrastructure and Terraform's state.
    - It is best practice to manage infrastructure using Terraform to prevent this kind of drift.

---

