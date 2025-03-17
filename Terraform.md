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

## Q16: 
**A**: 
## Q11:
**A**: 
## Q11: 
## Q11: 

