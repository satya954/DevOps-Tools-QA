
############################ AWS Interview Questions & Answers #########################

1. What is AWS?
2. What are the key services provided by AWS?
3. What is EC2 in AWS?
4. What is an S3 bucket?
5. Explain the difference between S3 and EBS.
6. What is IAM in AWS?
7. How does AWS VPC work?
8. What are Security Groups and how do they work?
9. What is an AWS region?
10. What are Availability Zones in AWS?
11. What is Auto Scaling?
12. What is Elastic Load Balancing?
13. What is Route 53?
14. Explain the difference between a public and private subnet.
15. What is CloudFormation?
16. What is AWS Lambda?
17. What is Amazon RDS?
18. How do you monitor AWS resources?
19. What is Amazon DynamoDB?
20. What is AWS Elastic Beanstalk?
21. What is Amazon CloudFront?
22. Explain Amazon SNS.
23. What is the difference between RDS and DynamoDB?
24. What are EIPs (Elastic IPs)?
25. How does AWS CloudTrail work?
26. What is Amazon CloudWatch?
27. What is the AWS Free Tier?
28. What is a NAT Gateway?
29. Explain the Shared Responsibility Model in AWS.
30. What are AWS Tags and why are they used?
31. How do you troubleshoot VPC issues.
32. What is difference between NACL and SG in VPC
33. How do communicate 4 or 5 VPC
34. What is VPC end point
35. What is Transit Gate way.
36. You create EC2 and S3 how can attach ec2 to s3 what policies is used.
37. What is Trusted role in IAM.
38. What is the difference between IAM Users and IAM Roles?
39. How do you secure data at rest and in transit in AWS?
40. Explain the difference between AWS S3 Standard and S3 Glacier.
41. How does AWS S3 versioning work?
34. What is AWS Elasticache?
35. Explain the concept of a bastion host.
36. How do you implement high availability in AWS?
37. What is AWS Direct Connect?
38. What are AWS Managed Services?
39. What is AWS Config?
40. How do you set up cross-region replication in S3?
41. Explain AWS KMS.
42. What is Amazon Redshift?
43. How does AWS handle data encryption?
44. What is Amazon EFS?
45. Explain AWS Elastic Transcoder.
46. What is AWS CodePipeline?
47. How do you implement disaster recovery in AWS?
48. What is AWS OpsWorks?
49. What is AWS Step Functions?
50. Explain the difference between Spot Instances and Reserved Instances.
51. What is Amazon SWF?
52. How do you secure an AWS API Gateway?
53. What are Placement Groups in AWS?
54. What is AWS CodeDeploy?
55. How does Amazon Athena work?
56. What is AWS Snowball?
57. Explain the concept of AWS CloudHSM.
58. What is AWS X-Ray?
59. How do you manage secrets in AWS?
60. Explain AWS Systems Manager.
61. What is the difference between horizontal and vertical scaling in AWS?
62. How does AWS Lambda handle cold starts?
63. What is a VPC peering connection and how does it work?
64. Explain the use of AWS Transit Gateway.
65. What is Amazon EKS?
66. How do you manage multi-account AWS environments?
67. Explain the concept of serverless architecture in AWS.
68. What are AWS Organizations?
69. How do you optimize costs in AWS?
70. What are the best practices for securing an AWS environment?
71. How do you configure a Load Balancer to allow only a specific port for internet traffic?
72. How will you connect an EC2 instance in a private subnet to an S3 bucket?
73. Why do we need a Security Group (SG) for an EC2 instance in a private subnet?
74. What is the role of IAM roles and policies?
75. Can you explain the Terraform plan and its purpose?
76. What is AWS Lambda, and how does it work?
77. How do you invoke a Lambda function, and where do you configure it?
78. Can you describe how Lambda handles scaling and event-based invocations?
79. What is Amazon CloudWatch, and have you configured any custom metrics?
80. What metrics are available on your CloudWatch dashboard?
81. How do you configure CPU utilization on your CloudWatch dashboard?
82. How do you attach an SSL certificate to an S3 bucket?
83. What type of encryption have you implemented in your project?
84. If an S3 bucket has a read-only policy, can you modify objects in the bucket?
85. What is a Content Delivery Network (CDN), and how does it work?
86. How do you attach policies to IAM users, either individually or by group?
87. What type of deployment strategies are you using in your project?
88. Have you used any tools to create customized Amazon Machine Images (AMIs)?
89. What is connection draining, and how does it work?
90. How does an Elastic Load Balancer (ELB) distribute traffic?
91. What is auto-scaling, and how does it work?
92. Can you describe the different types of Load Balancers and provide examples?
93. What is the maximum memory size for a Lambda function?
94. How can you increase the runtime for a Lambda function?
95. What automations have you performed using Lambda in your project?
96. What is the maximum runtime for a Lambda function?
97. What modules have you used in your Lambda function?
98. Have you created an SNS topic for your project?
99. If you've exhausted IP addresses in your VPC, how would you provision new resources?
100. Where do you run Terraform code, remotely or locally?
10. What is the purpose of access keys and secret keys in AWS?
102. What environments have you set up for your project?
103. Do you use the same AWS account for all environments?
104. Where do you write and save your Lambda function code?



Identity & Access Management  
1. How would you use AWS Control Tower for secure multi-account setup?  
2. How do you manage permission boundaries in AWS SSO?  
3. How do you enable MFA in AWS Cognito?  
4. How do you secure/manage identities in Cognito?  
5. How do you implement RBAC in AWS?  
6. How do you enforce MFA for IAM users?  
7. How do you design IAM policies with least privilege?

➡️ Networking & DNS  
8. How would you configure Route 53 for global HA?  
9. How do you implement weighted routing across regions?  
10. What’s the process to map a custom domain to an S3 static site?

➡️ Security & WAF  
11. How do you use AWS WAF to block bot attacks?  
12. How do you configure AWS Shield for DDoS protection?  
13. How to create custom WAF rules for specific threats?

➡️ Storage & Backup  
14. How to securely store files in S3?  
15. How to restrict public access but allow uploads?  
16. How to enable automatic backup & versioning?

➡️ Email with AWS SES  
17. How to configure SES for transactional emails?  
18. How to improve deliverability & avoid spam?  
19. How to set up SPF, DKIM & DMARC?

➡️ Compute & Scaling  
20. How do you configure EC2 Auto Scaling for traffic spikes?  
21. How to secure EC2 instances from unauthorized access?  
22. What are EC2 cost optimization techniques?

➡️ Database & Migration  
23. How do you migrate SQL Server with minimal downtime?  
24. How to implement automated RDS backups?  
25. How to configure RDS for high availability?

➡️ Infrastructure as Code  
26. How would you structure Terraform for AWS infra?  
27. What’s your preferred on-prem to AWS migration strategy?

➡️ Monitoring & Auditing  
28. How do you use CloudWatch alarms for CPU usage?  
29. How to analyze app performance with CloudWatch + X-Ray?  
30. How to audit API activity with CloudTrail?

➡️ Load Balancing  
31. Which ELB type supports both HTTP & TCP traffic?  
32. How to set up ALB with Auto Scaling for traffic spikes?  
33. How to protect ALB from DDoS & authenticate users?


######################################################## Person Jyoti Sharma ########################################################
1. How would you use AWS Control Tower to manage a secure multi-account setup?
2. How do you manage permission boundaries in AWS SSO?
3. What’s the best way to set up AWS WorkSpaces for 500 remote employees?
4. Which migration strategy would you choose to move on-prem servers to AWS?
5. How would you migrate a SQL Server database to AWS with minimal downtime?
6. How do you ensure automatic failover between AWS regions?
7. How would you structure Terraform code for AWS provisioning?
8. How would you enable social login (Google/Facebook) using AWS Cognito?
9. What’s your approach to securing and managing identities in Cognito?
10. How do you enable Multi-Factor Authentication (MFA) in AWS Cognito?
11. How would you configure Route 53 for global high availability?
12. What’s the process to set up a custom domain for an S3 static website?
13. How do you implement weighted routing between AWS regions?
14. What’s your design for a secure file storage solution using S3?
15. How would you restrict public access while allowing specific users to upload files?
16. How do you enable automatic backup and versioning in S3?
17. How would you configure EC2 Auto Scaling based on traffic patterns?
18. What are the best practices to secure EC2 instances from unauthorized access?
19. What steps do you take to optimize EC2 costs?
20. How would you configure RDS for high availability?
21. How do you implement automated backups and snapshots in RDS?
22. What’s your method for migrating an on-premises DB to RDS with minimal downtime?
23. How do you use AWS CloudTrail for API activity auditing?
24. How do you set up CloudWatch alarms to detect high CPU usage?
25. How do you use CloudWatch and X-Ray to analyze application performance?
26. How would you set up AWS SES for sending transactional emails?
27. How do you improve email deliverability and avoid spam filters in SES?
28. How do you configure SPF, DKIM, and DMARC for domain authentication in SES?
29. How would you protect your website against bot attacks using AWS WAF?
30. How do you configure AWS Shield for DDoS protection?
31. How would you create custom WAF rules to block specific attack patterns?
32. How would you design IAM policies based on the principle of least privilege?
33. How do you implement role-based access control (RBAC) in AWS?
34. How do you enforce MFA for all IAM users?
35. Which ELB type would you choose to handle both HTTP and TCP traffic, and why?
36. How would you set up ALB with Auto Scaling for unpredictable traffic spikes?
37. How would you protect your ALB against DDoS attacks using AWS services?
38. How would you configure ALB to authenticate users before backend access?

######################################################## Person 9 ########################################################
What is the difference between ALB and NLB?
 🔹 An ALB is routing requests to 3 EC2 instances. Users log in, but they keep getting redirected to the login page. What could be the issue?
 🔹 What are placement groups in AWS?
 🔹 Which placement group should I use for high availability across multiple AZs?
 🔹 Traffic has increased on a t2.medium EC2 instance. How can you upgrade it without downtime or data loss?
 🔹 You have a private S3 bucket. You don’t want to make it public or create roles/policies, but you need to share a file. How?
 🔹 What are the different Route 53 routing policies?
 🔹 Your Terraform script is trying to replace an existing EC2 instance while upgrading from CentOS 6 to CentOS 8. How do you avoid downtime?
 🔹 What is the difference between IAM Policies and IAM Roles?
 🔹 An EC2 instance needs access to an S3 bucket. What is the best way to configure it?
 🔹 What is Kubernetes, and why is it used?
 🔹 Write a shell script to check if the last executed command was successful.
