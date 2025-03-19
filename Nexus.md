                        ### Nexus Interview Questions & Answers #######
---
### 1. What is Nexus?
**A:** Nexus is a software repository manager that is used to store build artifacts.

### 2. What is the difference between Nexus and GitHub?
**A:** GitHub is an Source Code Management used to store the code where as Nexus is build artifactory storage repository.

### 3. As a DevOps Engineer, what are the roles and responsibilities you take care?
**A:** Creation of Nexus repositories, Access Control, Removal of older builds.

### 4. What is the tag name which we will use to integrate Nexus repo details in pom.xml?
**A:** Under distributionManagement tag

### 5. In which file we will store the nexus credentials?
**A:** In ${NEXUS_HOME}/bin/nexus.properties

---
              **Nexus Repository Manager Interview Questions & Answers (7+ Years Experience)**

---
### **General Nexus Repository Questions**  
1. **What is Nexus Repository Manager, and why is it used?**  
   - Nexus is a repository manager that helps store, organize, and distribute software artifacts. It is used for dependency management, artifact storage, and as a proxy for remote repositories.

2. **What are the different types of repositories in Nexus?**  
   - **Hosted Repository:** Stores internal artifacts.  
   - **Proxy Repository:** Caches artifacts from remote repositories.  
   - **Group Repository:** Combines multiple repositories under a single URL.

3. **How do you set up a new hosted repository in Nexus?**  
   - Navigate to **Repositories > Create Repository**  
   - Select the format (Maven, Docker, NPM, etc.)  
   - Set **Type** as **Hosted**  
   - Configure storage, cleanup policies, and access permissions  
   - Save and apply changes.

4. **What is the difference between Nexus 2 and Nexus 3?**  
   - Nexus 3 supports **more repository formats** like Docker, NPM, PyPI.  
   - It provides **better scalability** and **high availability**.  
   - The **UI and REST API** have been improved.  

---
### **Security & Access Control**  
5. **How do you configure user authentication in Nexus?**  
   - Nexus supports **LDAP, Active Directory, and SSO** for authentication.  
   - Users can be created manually or assigned roles via external authentication providers.

6. **What are Nexus roles and privileges?**  
   - Roles are a collection of permissions (privileges).  
   - Privileges include actions like **read, write, delete** for specific repositories.

7. **How do you secure a Nexus repository?**  
   - Enable **HTTPS** and enforce **strong authentication**.  
   - Implement **repository cleanup policies**.  
   - Restrict access with **role-based permissions**.
---
### **Integration & CI/CD**  
8. **How do you integrate Nexus with Jenkins?**  
   - Use the **"Nexus Artifact Uploader"** plugin in Jenkins.  
   - Configure a Jenkins pipeline to **push artifacts** to Nexus.  
   - Example:  
     ```groovy
     nexusArtifactUploader(
         nexusVersion: 'nexus3',
         protocol: 'http',
         nexusUrl: 'http://nexus.example.com',
         repository: 'maven-releases',
         credentialsId: 'nexus-credentials',
         groupId: 'com.example',
         artifactId: 'my-app',
         version: '1.0.0',
         packaging: 'jar',
         file: 'target/my-app-1.0.0.jar'
     )
     ```
9. **How do you configure Nexus as a Docker registry?**  
   - Enable the **Docker repository format** in Nexus.  
   - Configure **port binding** for Docker.  
   - Authenticate using **Docker login**.

---
### **Performance & Troubleshooting**  
10. **How do you optimize Nexus performance?**  
    - Configure **blob stores** and enable **storage cleanup policies**.  
    - Use **proxy caching** to reduce remote fetch times.  
    - Allocate **more memory** and optimize **GC tuning**.

11. **How do you troubleshoot Nexus repository issues?**  
    - Check **Nexus logs** (`nexus.log`, `audit.log`).  
    - Verify **service status** using `systemctl status nexus` or `docker logs`.  
    - Debug **proxy issues** with network tools like `curl` or `wget`.

---
                  **Nexus Repository Manager - Real-Time Scenario Based Interview Questions & Answers**

---

### **Scenario 1: Jenkins Build Fails Due to Missing Dependencies**  
**Q:** You are using Nexus as a Maven repository, and a Jenkins build fails because it cannot find a dependency in Nexus. How would you troubleshoot this?  

**A:**  
1. **Check if the dependency exists in Nexus**:  
   - Navigate to Nexus UI and search for the artifact using **Group ID, Artifact ID, or Version (GAV coordinates)**.  
   - If missing, verify if it was deleted due to **cleanup policies**.  

2. **Check Proxy Repository Configuration**:  
   - If it is a remote dependency, ensure the **Proxy Repository (e.g., Maven Central, JCenter)** is correctly configured.  
   - Verify the **remote URL and connectivity**.  

3. **Check Jenkins Logs**:  
   - Look for **HTTP 404 errors** or **timeout issues**.  
   - If the issue is intermittent, it could be a **network issue**.  

4. **Manually Download & Deploy Artifact (if needed)**:  
   ```sh
   mvn deploy:deploy-file -DgroupId=com.example -DartifactId=my-lib -Dversion=1.0.0 \
   -Dpackaging=jar -Dfile=my-lib-1.0.0.jar -DrepositoryId=nexus \
   -Durl=http://nexus.example.com/repository/maven-releases/
   ```

---

### **Scenario 2: Nexus Storage Reaching Capacity**  
**Q:** Your Nexus repository storage is reaching its limit. How would you handle this situation?  

**A:**  
1. **Enable Cleanup Policies**:  
   - Configure **"Cleanup Policies"** to delete old or unused artifacts.  
   - Define retention rules like "Delete artifacts older than 90 days".  

2. **Check and Delete Unused Snapshots**:  
   - Navigate to **Blob Stores** and find large-sized repositories.  
   - Use a **scheduled task** to delete old snapshots.  

3. **Move Large Artifacts to Another Blob Store**:  
   - Create a **new blob store** in a different disk location.  
   - Migrate large repositories to the new blob store.  

4. **Expand Storage**:  
   - Attach additional storage to the Nexus instance.  
   - If using **Docker-based deployment**, mount a new volume for Nexus storage.  

---

### **Scenario 3: Unauthorized Access Detected**  
**Q:** You notice unauthorized access attempts in Nexus logs. How do you secure the repository?  

**A:**  
1. **Check Logs** for Suspicious Activity:  
   - Review `nexus.log` and `audit.log` for failed login attempts.  
   - Look for brute-force attack patterns.  

2. **Enforce Strong Authentication**:  
   - Enable **LDAP/SSO authentication** instead of default user management.  
   - Enforce **strong passwords** and disable default accounts.  

3. **Restrict Repository Access**:  
   - Apply **RBAC (Role-Based Access Control)**.  
   - Limit "Anonymous Access" and restrict read/write privileges.  

4. **Enable HTTPS & Firewall Rules**:  
   - Configure **HTTPS** for secure communication.  
   - Restrict access to **trusted IPs** using a firewall or security groups.  

---

### **Scenario 4: Slow Artifact Downloads**  
**Q:** Developers report that downloading artifacts from Nexus is very slow. How do you troubleshoot this?  

**A:**  
1. **Check Nexus Server Performance**:  
   - Monitor CPU, memory, and disk I/O usage (`top`, `htop`, `iostat`).  
   - Increase allocated heap memory in `nexus.vmoptions`:  
     ```sh
     -Xms2g  
     -Xmx4g  
     ```

2. **Optimize Proxy Repository Settings**:  
   - Enable **caching** for frequently accessed artifacts.  
   - Increase **HTTP connection timeout** settings in Nexus.  

3. **Check Network Latency & DNS Issues**:  
   - Run `ping` or `traceroute` to see if the Nexus server is reachable.  
   - If using **AWS, Azure, or GCP**, check **load balancer configurations**.  

4. **Enable Content Compression**:  
   - Enable **gzip compression** for artifact transfers.  

---

### **Scenario 5: CI/CD Pipeline Fails Due to Nexus Downtime**  
**Q:** Your Jenkins CI/CD pipeline fails because Nexus is down. What steps do you take?  

**A:**  
1. **Check Nexus Service Status**:  
   ```sh
   systemctl status nexus  
   journalctl -u nexus --since "10 minutes ago"  
   ```

2. **Restart Nexus** (if needed):  
   ```sh
   systemctl restart nexus  
   ```

3. **Check Logs for Errors**:  
   - Look at `nexus.log` for potential issues like database corruption or disk space errors.  

4. **Verify External Dependencies**:  
   - If Nexus is running as a Docker container, check:  
     ```sh
     docker ps | grep nexus  
     docker logs <container_id>  
     ```

5. **Set Up a Backup Nexus Instance**:  
   - Use **High Availability (HA) Nexus setup** or a **standby backup** to avoid downtime.  

---

### **Scenario 6: Need to Migrate Nexus from One Server to Another**  
**Q:** Your team needs to migrate Nexus to a new server. How would you do it?  

**A:**  
1. **Backup Current Data**:  
   - Backup **`sonatype-work`** directory (contains repositories and configuration).  
   - Use `tar` or `rsync` to copy data to the new server:  
     ```sh
     rsync -avz /opt/sonatype-work/ new-server:/opt/sonatype-work/  
     ```

2. **Install Nexus on the New Server**:  
   - Download and install the same Nexus version.  
   - Configure `nexus.properties` with new settings.  

3. **Restore Data and Start Nexus**:  
   ```sh
   systemctl start nexus  
   ```

4. **Test & Validate**:  
   - Verify repository URLs and permissions.  
   - Run `curl` or a sample deployment to ensure Nexus is working.  

---

### **Scenario 7: Nexus Repository Cleanup is Not Working**  
**Q:** You configured cleanup policies in Nexus, but old artifacts are not being deleted. How do you debug this?  

**A:**  
1. **Check Cleanup Policy Rules**:  
   - Ensure rules like **"Remove artifacts older than X days"** are correctly set.  

2. **Manually Trigger Cleanup**:  
   - Navigate to **Admin > Cleanup Policies > Run Now**.  
   - Check logs (`nexus.log`) for errors.  

3. **Check Permissions**:  
   - The user running Nexus should have permission to delete files in **blob store**.  

4. **Verify Scheduled Tasks Execution**:  
   - Ensure **"Cleanup Service"** is running in **Scheduled Tasks**.  


  
