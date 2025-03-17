                    ================= Terraform Interview Questions ===================

1. Resources alreadt exists in the Cloud, so how to configure it with terraform ?
2. What is back end in Terraform.
3. In terraform you create and automate but somebody manually change the file or Resources how do you troubleshoot ?
4. In Terraform you create Ec2 instance 1 then you want to create 10 instance how do create


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


