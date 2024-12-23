1. Why Ansible?
 . With its agentless approach, YAML-based playbooks, and Python dependencies, Ansible is a game-changer for:
   . Server Provisiong
   . Configuration management
   . Application Deployment
   . Continous Delivery and Orcherstration.
   
1️⃣ What is Ansible?
An open-source tool for automation, known for its simplicity and agentless architecture.

2️⃣ Setting Up Master & Worker Nodes:
Step-by-step instructions to configure Ansible on multiple servers, including SSH key setup and hosts file configuration.

3️⃣ Modules and Commands:
Examples of ad hoc commands to check server status, install packages like NGINX, and troubleshoot issues.

4️⃣ Common Errors and Troubleshooting:
How to resolve permission issues and other common challenges in Ansible setups.

5️⃣ Installing and Managing NGINX and Docker:
Automating the installation and management of NGINX and Docker on Ubuntu and redhat Linux 2 servers.

6️⃣ Introduction to Inventory and Playbooks:
A glimpse into inventory file configurations and a teaser for the next post about creating and using playbooks in Ansible.


              			**Interview Questions**:

1. How would you ensure that a specific package is installed on multiple servers?
Answer: You can use the package module in a playbook to ensure that a specific package is installed across multiple servers. 

2. How do you handle different environments (development, testing, production) with Ansible?
Answer: You can manage different environments by using inventory files and group variables. Create separate inventory files for each environment and use group variables to specify environment-specific configurations. Each hosts file would define the servers for that specific environment, and you can create a group_vars directory for each environment.

3. How would you restart a service after updating a configuration file?
Answer: You can use the notify feature in Ansible to restart a service after a configuration file is updated.

4. How can you ensure idempotency in your Ansible playbook?
Answer: Ansible modules are designed to be idempotent, meaning they can be run multiple times without changing the result beyond the initial application. For instance, if you use the file module to create a file, Ansible will check if the file already exists before trying to create it.

5. How do you handle secrets or sensitive data in Ansible?
Answer: You can handle sensitive data using Ansible Vault, which allows you to encrypt files or variables. 

6. Can you explain how you would deploy an application using Ansible?
Answer: Define Inventory: Create an inventory file with the target hosts.
Create a Playbook: Write a playbook that includes tasks for pulling the application code from a repository, installing dependencies, configuring files, and starting services.

7. How would you handle task failures and retries in Ansible?
Answer: You can use the retry and when directives to handle task failures in Ansible. The retries and delay parameters can be specified for tasks that might need to be retried.

8. How would you roll back a deployment if the new version fails?
Answer: To roll back a deployment, you can maintain a previous version of the application and use a playbook that checks the health of the new version before deciding to switch back.

9. How can you manage firewall rules across multiple servers using Ansible?
Answer: You can use the firewalld or iptables modules to manage firewall rules. 

10. How do you implement a continuous deployment pipeline using Ansible?
Answer: To implement a continuous deployment pipeline, you can integrate Ansible with a CI/CD tool like Jenkins, GitLab CI, or GitHub Actions. 

11. How can you check if a file exists and create it if it doesn't?
Answer: You can use the stat module to check if a file exists and then use the copy or template module to create it if it doesn’t.

12. How can you execute a command on remote hosts and capture its output?
Answer: You can use the command or shell module to run commands on remote hosts and register the output
