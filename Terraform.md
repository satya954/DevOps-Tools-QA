                    ================= Terraform theory Questions ===================
## Q1: What happens if your state file is accidentally deleted?
**A**: Terraform loses track of all managed infrastructure. On next apply, it will attempt to recreate everything from scratch, potentially causing conflicts with existing resources.

## Q2: What happens if multiple team members run terraform apply simultaneously?
**A**: State file locking fails, risking corrupted state and inconsistent infrastructure. One process succeeds while others error out, potentially leading to drift if not managed properly.

## Q3: What happens if a resource fails halfway through a terraform apply?
**A**: Terraform leaves successfully created resources running but marks the state as tainted. Subsequent apply operations will attempt to recreate failed resources, but you're left in partial state.

## Q4: What happens when AWS API rate limits are hit during a large terraform apply?
**A**: Operations fail with throttling errors. Terraform retries a few times then fails the apply. Resources created before the limit was hit remain, creating partial deployments.

## Q5: What happens if terraform plan shows no changes but infrastructure was modified outside Terraform?
**A**: Terraform won't detect the drift until you run terraform refresh or terraform plan -refresh-only. This can lead to unexpected behavior when making future changes.

## Q6: What happens if you delete a resource definition from your configuration?
**A**: On next apply, Terraform will destroy that resource in your infrastructure unless you use terraform state rm to remove it from state first or use lifecycle { prevent_destroy = true }.

## Q7: What happens if a provider API changes between Terraform versions?
**A**: You may encounter compatibility issues and failed plans/applies. Resources might need to be rebuilt or configurations updated to match new API requirements.

## Q8: What happens if you have circular dependencies in your Terraform modules?
**A**: Terraform will fail to initialize or plan with dependency cycle errors. You'll need to refactor your module structure to break the circular references.

## Q9: What happens if you exceed AWS service quotas during deployment?
**A**: Resources will fail to create with quota exceeded errors. Terraform marks them as failed, and you'll need to request quota increases before retrying the apply.

## Q10: What happens if you lose access to the remote backend storing your state?
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
                    ================= Terraform Practical Questions ===================

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

**Q11**. **Resources already exist in the Cloud. How do you configure them with Terraform?**  
- Use the `terraform import` command to import existing resources into your Terraform state file.  
- After import, you must manually write the corresponding Terraform code to match the existing resource configuration.

**Q12**. **What is a backend in Terraform?**  
- A backend in Terraform determines how state is loaded and how operations such as apply are executed.  
- Common backends include local (default), S3, Azure Blob Storage, and HashiCorp's Terraform Cloud.

**Q13**. **In Terraform you automate creation, but someone manually changes a file or resource. How do you troubleshoot?**  
- Run `terraform plan` to detect drift between the actual infrastructure and Terraform state.  
- Use `terraform refresh` to update the state file with real-world infrastructure changes.

**Q14**. **In Terraform you create one EC2 instance, then want to create 10. How do you do it?**  
- Use the `count` or `for_each` meta-argument to create multiple resources:
  ```hcl
  resource "aws_instance" "example" {
    count         = 10
    ami           = "ami-xyz"
    instance_type = "t2.micro"
  }

**Q15**. **What is the Terraform directory structure?**  
- A typical Terraform project directory includes the following files:
├── main.tf            # Main configuration
├── variables.tf       # Input variable definitions
├── outputs.tf         # Output variable definitions
├── terraform.tfvars   # Variable values
├── backend.tf         # Backend configuration (if used)
└── modules/           # Reusable modules

## Q17. How do you import manually created AWS resources into Terraform?

To import manually created AWS resources into Terraform, follow these steps:

1. **Identify the Resource Type and ID**:  
   You first need to identify the type of resource and its ID that you want to import. For example, if you're importing an EC2 instance, you'll need the instance ID (e.g., `i-1234567890abcdef0`).

2. **Use the `terraform import` Command**:  
   Terraform provides the `terraform import` command to bring existing resources under its management. The syntax for this command is:

   ```bash
   terraform import <resource_type>.<resource_name> <resource_id>


## Q18. Why should we run `terraform plan` before `terraform apply`?

Running `terraform plan` before `terraform apply` is crucial for the following reasons:

1. **Preview Changes**:
   - `terraform plan` generates an execution plan that shows what actions Terraform will take (such as creating, modifying, or destroying resources). It allows you to review what will happen before actually applying any changes.
   - You can see exactly what Terraform intends to do, which helps avoid unintended changes to your infrastructure.

2. **Validate Configuration**:
   - The `terraform plan` command helps validate your configuration files (HCL code). It checks if there are any syntax errors or logical mistakes before applying changes to the infrastructure.
   - It ensures that your Terraform configuration is consistent with your desired state.

3. **Avoid Unwanted Changes**:
   - Running `terraform plan` helps prevent accidental or unwanted modifications to live resources. By reviewing the plan, you can ensure that no unexpected resource modifications or deletions will occur.
   - For example, you might realize that a change in your configuration would delete a critical resource, such as a database or an EC2 instance, and you can adjust the configuration to prevent that.

4. **Understand Dependencies**:
   - Terraform determines dependencies between resources and will show how changes to one resource might affect others. The plan output helps identify such dependencies, which is useful for complex infrastructure.
   - You can verify that your changes do not break other resources or services that depend on them.

5. **Collaborative Verification**:
   - If you are working in a team, the output of `terraform plan` can be shared with other team members to get feedback before applying changes. This is useful for collaborative verification and review of infrastructure changes.

6. **Avoiding Unintended Cost Implications**:
   - Running `terraform plan` can help you spot potential issues such as the unintended provisioning of large resources (e.g., an instance with a high cost) or redundant infrastructure components. This can prevent unnecessary costs in cloud environments.

7. **Dry Run**:
   - `terraform plan` acts as a "dry run," meaning it simulates the changes without actually applying them. This allows you to assess the impact of the changes without causing any disruption to your existing infrastructure.

### Summary:
- **`terraform plan`** gives you a chance to review and validate the changes before applying them.
- It helps you catch potential mistakes and unintended consequences.
- Running `terraform plan` first reduces the risk of errors, downtime, and unnecessary costs.


## Q19. What happens if cloud infrastructure changes between `terraform plan` and `terraform apply`?

When cloud infrastructure changes between the execution of `terraform plan` and `terraform apply`, Terraform handles the changes based on its state and the configuration files. The following scenarios can occur:

1. **Infrastructure Changes Detected**:
   - If any changes occur in the cloud infrastructure after `terraform plan` but before `terraform apply`, Terraform will compare the current state of the infrastructure to the desired state as described in the configuration files.
   - During `terraform apply`, Terraform will re-run its comparison and may find differences, which it will attempt to reconcile by making the necessary updates, additions, or deletions to the infrastructure.

2. **Drift in the Infrastructure**:
   - Infrastructure drift refers to the scenario when changes are made manually (outside of Terraform) or via other automation tools, causing the actual state of the infrastructure to differ from the state Terraform expects.
   - If drift occurs, Terraform will try to align the infrastructure back to the desired state based on the current configuration and its state file. For example, it might try to recreate or modify resources to match the plan if drifted resources were manually changed.

3. **Terraform State vs. Real State**:
   - Terraform keeps track of the state of infrastructure in its state file. If the infrastructure changes between `terraform plan` and `terraform apply`, Terraform will detect discrepancies between the state file (which represents the last known infrastructure state) and the actual infrastructure state.
   - Terraform will prompt the user with updated information regarding the changes, and depending on the configuration, it will either attempt to modify or recreate the resource as needed.

4. **Handling Resource Conflicts**:
   - If the resource changes between `terraform plan` and `terraform apply` result in a conflict (for example, if a manual change invalidates the current configuration), Terraform might fail to apply the changes. In such cases, it will display an error or warning indicating that the current state doesn't match expectations.
   - Terraform will suggest how to resolve the conflict (e.g., through manual intervention or using `terraform refresh` to update the state file).

5. **Resource Destruction**:
   - If Terraform's planned changes involve the destruction of resources that were modified outside of Terraform, the infrastructure might be lost or adversely affected during the apply phase. For example, a manual change to a resource might cause Terraform to attempt a delete-and-create action, which could result in downtime or data loss if not handled carefully.

6. **Manual Modifications Outside of Terraform**:
   - If a user manually modifies the infrastructure during the period between `terraform plan` and `terraform apply`, those changes will not be reflected in the state file. This could result in Terraform trying to recreate or delete the manually modified resources to bring them into alignment with the configuration.

7. **Best Practices**:
   - To avoid issues with changes between `terraform plan` and `terraform apply`, it is recommended to:
     - **Use `terraform refresh`** before `terraform apply` to synchronize the Terraform state with the real infrastructure.
     - **Minimize manual changes** to infrastructure when Terraform is managing it.
     - **Lock resources** during updates to prevent conflicts.
     - **Collaborate with the team** to ensure all changes to the infrastructure are tracked and versioned properly.

### Summary:
- **Changes between `terraform plan` and `terraform apply`** may lead to infrastructure drift or conflicts.
- Terraform will compare the planned infrastructure changes to the current state and apply necessary updates to reconcile the differences.
- Manual changes to infrastructure may cause conflicts, which Terraform will try to resolve, but it may require manual intervention to avoid unexpected behavior.
- It is crucial to regularly refresh the Terraform state and minimize manual changes to infrastructure during Terraform management.


## Q20. If a Virtual Machine already exists and you write the same Terraform configuration, what happens when you run Terraform commands?

When a Virtual Machine (VM) already exists and you run Terraform with the same configuration again, the following steps happen:

1. **Terraform State Check**:
   - Terraform first checks the **state file** to see if it is already managing the existing VM. The state file contains information about the resources Terraform has previously created and their properties.

2. **No Changes Detected**:
   - If the VM already exists and its configuration matches the one in your Terraform configuration file (i.e., no changes are required), Terraform will not make any modifications to the VM.
   - Terraform will output a message saying that no changes are necessary, and the VM will remain unchanged.

3. **If Configuration Matches the Existing VM**:
   - If the Terraform configuration is identical to the existing VM (e.g., same resource name, type, and settings), Terraform will detect that the resource already exists and is in the desired state. It will not attempt to recreate or modify the VM.
   - Example output: `No changes. Infrastructure is up-to-date.`

4. **Resource Drift (Manual Changes)**:
   - If there are any changes made manually to the existing VM (e.g., changing the VM size, adding disks, etc.), Terraform will detect the differences between the actual infrastructure state and the state defined in the configuration file.
   - Terraform will then try to **reconcile the differences**, either by modifying the VM to match the configuration or by issuing an error if it cannot make the changes automatically.

5. **Terraform Plan and Apply**:
   - When you run `terraform plan`, Terraform will show you the current state of the resources and highlight any changes that would occur if you ran `terraform apply`.
   - If there are no differences between the existing VM and the configuration, Terraform will output a message stating that no changes are needed.
   - If there are differences, Terraform will propose changes and prompt you to apply them.

6. **If Changes are Made to the Configuration**:
   - If the configuration is modified (e.g., changing the VM size or adding additional settings), Terraform will try to update the existing VM to reflect the new desired state.
   - Depending on the type of change, Terraform may update the VM in place, or it may recreate the VM (if the change requires it).

7. **Terraform Import**:
   - If the VM was created manually or outside Terraform's management, you will need to **import** the existing VM into Terraform's state using the `terraform import` command before you can manage it with Terraform.
   - Example: `terraform import aws_instance.example i-0abcd1234efgh5678`

8. **Idempotency**:
   - One of the key features of Terraform is **idempotency**, which means that running the same configuration multiple times will not result in changes unless there are differences between the desired state (configuration) and the actual state (infrastructure).

### Summary:
- If the Virtual Machine exists and the configuration matches, Terraform will detect no changes and leave the VM as it is.
- If manual changes have been made to the VM, Terraform will detect and attempt to reconcile the differences.
- Any modifications to the configuration will be applied to the VM as needed.
- Terraform commands are idempotent, meaning they only apply changes when necessary.


**Q21**. **What is Terraform taint?**

- **Terraform taint** is a command used to mark a resource as **tainted**. A tainted resource will be destroyed and recreated during the next `terraform apply`. This can be helpful when a resource is in a faulty state and you need to force Terraform to recreate it.
  
- The **`terraform taint`** command explicitly tells Terraform to consider a resource as broken, even if there are no changes in the configuration. The next time you run `terraform apply`, Terraform will destroy and recreate the resource.

- **Command Syntax**:
  ```bash
  terraform taint <resource_type>.<resource_name>

  Example: terraform taint aws_instance.example
           terraform untaint aws_instance.example


## Q22. What is Terraform user data?

- **Terraform User Data** refers to the configuration or script that you pass to an instance during its creation. It is typically used in cloud environments like AWS, Azure, or Google Cloud to run scripts or configure the instance at the time of provisioning.

- **User Data in Terraform**:
  - In AWS, user data is commonly used to configure EC2 instances during their initial launch. This can include installing software, configuring system settings, or running custom scripts.
  - When creating an EC2 instance in Terraform, you can specify user data in the `aws_instance` resource by using the `user_data` argument.

- **Usage of User Data**:
  - **Automation**: It automates the setup of instances by running scripts automatically upon instance creation.
  - **Bootstrapping**: You can use user data to bootstrap a machine with all necessary configurations or software, like installing packages or starting services.

- **Example** (AWS EC2 with User Data):
  ```hcl
  resource "aws_instance" "example" {
    ami           = "ami-12345678"
    instance_type = "t2.micro"
    
    user_data = <<-EOF
      #!/bin/bash
      apt-get update -y
      apt-get install -y nginx
      systemctl start nginx
    EOF
  }


## Q23. What is Terraform workspace?

- **Terraform Workspace** is a feature that allows you to manage multiple distinct environments or configurations within a single working directory. It helps in isolating different states of infrastructure for various environments such as `dev`, `prod`, or `staging`.

- **Purpose of Workspaces**:
  - **Environment Isolation**: Workspaces allow you to manage multiple environments with the same configuration. For example, you can use the same Terraform code to create resources in a `dev` workspace and `prod` workspace, ensuring they remain separate.
  - **State Management**: Each workspace has its own state file, which keeps track of the resources managed by Terraform. This means that changes in one workspace do not affect other workspaces.
  
- **How Workspaces Work**:
  - By default, when you initialize a Terraform configuration, Terraform creates a `default` workspace.
  - You can create additional workspaces using the `terraform workspace` commands to isolate different configurations for various environments.

- **Common Operations with Workspaces**:
  - **Switching Workspaces**: You can switch between workspaces using the following command:
    ```bash
    terraform workspace select <workspace_name>
    ```
  - **Creating a New Workspace**: You can create a new workspace using:
    ```bash
    terraform workspace new <workspace_name>
    ```
  - **Listing Workspaces**: To see all the available workspaces, use:
    ```bash
    terraform workspace list
    ```
  - **Delete Workspace**: To delete a workspace, you can use:
    ```bash
    terraform workspace delete <workspace_name>
    ```

- **Example Usage**:
     ```bash
     terraform workspace new dev
     terraform workspace select dev
     terraform workspace list
     ```

- **Use Case for Workspaces**:
  - You may use workspaces to manage separate infrastructure configurations for different stages of development (e.g., `dev`, `staging`, `prod`) within the same project or repository. Each workspace will have its own set of variables, state, and resource configurations.
  
- **Important Notes**:
  - Workspaces do not create separate directories; they only isolate state files within the same directory.
  - Workspaces are primarily used for managing multiple environments but do not provide full isolation of configurations (i.e., you may still need to use variable files or other tools for full environment management).
  - When switching between workspaces, Terraform automatically uses the corresponding state file.

## Q27. How will you configure Terraform to use AWS?

To configure Terraform to use AWS, follow these steps:
     a. **Using dynamic AWS Credentials**
          ```bash
          export AWS_ACCESS_KEY_ID="your-access-key-id"
          export AWS_SECRET_ACCESS_KEY="your-secret-access-key"
          export AWS_DEFAULT_REGION="ap-south-1"  # Optional: Set the AWS region (default region)
          ```
     
     b. **AWS CLI Configuration** (Recommended):
          ```bash
          aws configure
          ```
- **Using AWS Profiles**:
  If you are working with multiple AWS accounts, you can specify a named profile in your Terraform configuration:
  ```hcl
  provider "aws" {
    region  = "us-west-2"
    profile = "your-profile-name"
  }

  provider "aws" {
    region = "us-west-2"
    assume_role {
      role_arn = "arn:aws:iam::123456789012:role/RoleName"
    }
  }


## Q28. Write a Terraform script to create an EC2 instance and install a web server .

```hcl
# Define the provider
provider "aws" {
  region = "us-west-2"  # Replace with your desired region
}

# Define a security group
resource "aws_security_group" "web_sg" {
  name        = "web_sg"
  description = "Allow inbound HTTP traffic"
  
  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# Define the EC2 instance
resource "aws_instance" "web_server" {
  ami           = "ami-0c55b159cbfafe1f0"  # Replace with your desired AMI ID
  instance_type = "t2.micro"              # Instance type
  key_name      = "my-key"                # Replace with your SSH key name
  security_groups = [aws_security_group.web_sg.name]
  
  # User data to install Apache Web Server
  user_data = <<-EOF
              #!/bin/bash
              yum update -y
              yum install -y httpd
              systemctl start httpd
              systemctl enable httpd
              EOF

  tags = {
    Name = "WebServerInstance"
  }
}

# Output the public IP of the instance
output "web_server_public_ip" {
  value = aws_instance.web_server.public_ip
}

