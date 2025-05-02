				**Kubernetes Interview Questions:**

				---------- Beginner Level: -----------
 
## Q1. What is Kubernetes. ?
**A**:

## Q2. What are the main components of Kubernetes ?
**A**:

## Q3.. What is a Pod in Kubernetes ?
**A**:

4. What is a Replicaset ?
5. What is a Deployment ?
6. What is a DaemonSet ?
7. What are Kubernetes Labels and selectors ?
8. How does kubernetes handles container scaling ?
9. What is a Kubernetes Namespace?
10. How does kubernetes handle service discovery and load balancing ?
11. What is the role of config map ?
12. How can you expose a kubernetes deployment to the outside world ?
13. Write a Kubernetes Deployment manifest to create an Nginx pod with 3 replicas. 
3. Write a Kubernetes ConfigMap YAML to store database configuration with keys `DB_HOST=db.example.com` and `DB_PORT=5432`. 
4. What is HPA (Horizontal Pod Autoscaler)? 
5. How do you scale up the replicas in a deployment using a command? 
6. How to copy files from the host to a container using a command? 
7. How to restart a pod without stopping the deployment? 
8. How do pods communicate with each other? 
9. What are the security best practices for a Kubernetes cluster? 
10. How do you ensure the application is highly available and scalable? 
11. How do you troubleshoot a pod in a **Pending** state? 
12. How do you create a Kubernetes cluster? Explain the steps. 
13. What critical issues have you faced with a Kubernetes cluster? 
14. What is an indentation error in a YAML file? 
15. How do you enter into a running pod in Kubernetes ?
16. What work you do in Cluster in kubernetes
17. Which version of kubernetes you used in current?
18. Difference between Service Principal and Managed Identity ?
19. What you will do if your Node is full?
20. Difference between PV and PVC and Storage classes.
21. Difference between Taint and tolration in Kubernetes?
22. Ingress Controller?
23. Are Pod IP addresses static or dynamic?
24. 

 				---------- Intermediate Level: -----------
    
1. What is a stateful set in Kubernetes ?
2. Explain the diff b/w a Deployment and Stateful Set ?
3. How does kubernetes handle storage for applications ?
4. Explain the concept of Rolling Update in Kubernetes ?
5. What is a Kubernetes Operator ?
6. How can u perform rolling updates with zero downtime ?
7. What is a kubernetes Helm ?
8. How does kubernetes handle security and access controls ?



				---------- Real time : -----------
	
1. How many microservices have you worked on ?

2. How many kubernetes cluster do u handle ?

3. What types of Network Policies are used in Pods for security ?

4. How do u handle senstive data used in microservices and how it is retrieved when required ?

5. Path-based routing ?

6. Why do we use stateful-Sets over Deployments for database applications ?

7. How to troubleshoot when the pod is not able to start ?

8. Disk pressurce for node, How to resolv it ?

9. How to the Upgrade the cluster ?

10. What happens (step-by-step) when you are upgrading the kubernetes cluster ?

11. How do you monitor the kubernetes Pods and Deployments ?

12. which Alerts mechanisms you have worked on ?

13. How do you get alerts ?

14. Let's say, if you are using Prometheus how do you recieve the alert to you ?

15. How to deploy microservice in AWS ?

16. How to stream the Kubernetes logs ?

17. How to monitor the Kubernetes services ?

18. On What parameters, how do u define kubernetes Hardware configuration ?

19. How to use Ingress Controller ?

20.  Explain the flow of YAML files in Kubernetes (i have explained from Deployment to Ingress).

21.  


				## Scenarios Based Questions & Answers ##

## IMP Q1: How do you recover a lost Kubernetes cluster if the etcd data is corrupted?
**A**: Check if etcd snapshots were taken (etcdctl snapshot restore).
If a snapshot isn’t available, attempt disaster recovery by:
i. Scaling down control plane nodes.
ii. Checking if any nodes still have valid etcd data.
iii. Restoring from a secondary backup system.
If all else fails, rebuild the cluster and reapply workloads from stored YAML files or Helm charts.

## IMP Q2: Your Kubernetes nodes are in Ready state, but pods are not scheduling. What do you check?
**A**: kubectl describe node <node-name> → Look for taints & tolerations issues.
i. kubectl get events -A → Check for insufficient resources (CPU, memory).
ii. kubectl get pods -o wide → Ensure pods are not stuck in Pending state due to scheduling constraints.
iii. Node affinity rules (requiredDuringSchedulingIgnoredDuringExecution) could be misconfigured.
iv. Check API server logs if nodes aren't communicating properly.

## IMP Q3: How do you troubleshoot intermittent network failures between Kubernetes pods?
**A**: Run ``kubectl exec -it <pod> -- ping <target-pod>`` to check connectivity.
Verify ``kubectl get pods -o wide`` to ensure pods are on the correct nodes.
``kubectl describe networkpolicy`` to check if Network Policies are blocking traffic.
Check the CNI plugin (Calico, Flannel, Cilium) logs for any failures.
Use tcpdump or wireshark on the node to inspect dropped packets.
Enable Kubernetes Debugging with ephemeral containers (kubectl debug).

## Q1: What happens if the k8s master node and worker node firewall gets broken?
**A:**  Existing pods will continue running, but you can't deploy new workloads or updates. API server can't communicate with worker nodes, breaking cluster management capabilities.

## Q2: What happens if etcd backup is corrupted during a cluster restore?
**A:** Complete cluster failure. The control plane won't initialize and you can't manage resources. Only options are using an older backup or rebuilding the cluster from scratch.
 
## Q3: What happens if a node's kubelet crashes but the container runtime continues?
**A:** Existing pods keep running, but the node is marked "NotReady." After grace period (~5min), pods are evicted and rescheduled elsewhere. No new pods will be scheduled to this node.

## Q4: How would applications behave if Kubernetes DNS (CoreDNS) fails?
**A:** Existing connections work but new service discovery fails. Applications show connection timeouts, and probes using DNS names fail, potentially causing cascading pod restarts.

## Q5: What happens during a network partition between control plane and worker nodes?
**A:** Worker nodes continue running existing workloads, but controllers can't manage them. New deployments, scaling, and updates fail. Nodes might eventually be marked unreachable.

## Q6: What happens if your CNI plugin starts dropping packets intermittently?
**A:** Pod-to-pod communication becomes unreliable with sporadic timeouts. Services appear down randomly, causing difficult-to-troubleshoot application failures and inconsistent behavior.

## Q7: What happens to StatefulSets if underlying storage experiences high latency?
**A:** Pod startup times increase dramatically. Database pods may trigger restart loops, write operations timeout, and new pods get stuck in "ContainerCreating" state.

## Q8: What happens if pod resource limits are set too low?
**A:** Containers face OOM kills during peak loads. Applications become unstable with unexpected restarts, and horizontal scaling can't solve the problem since each instance is resource-starved.

## Q9: What happens when control plane can't reach cloud provider's API?
**A:** Cloud-specific features like LoadBalancers and persistent volumes fail. Node initialization is incomplete, and external resource provisioning stops working.

## Q10: What happens if your cluster's certificate authority expires?
**A:** Complete cluster failure. All component communications fail with TLS errors. API server rejects connections, kubectl stops working, and the entire cluster becomes unusable.



#######################################################################################################################################################################
## ✅ Kubernetes

**Q1**. **How do you secure MySQL data running in a container?**
  - To secure MySQL data in a container:
    - Use **Docker volumes** or **Kubernetes Persistent Volumes (PVs)** to store data outside the container, ensuring it persists even if the container is destroyed or restarted.
    - Ensure MySQL is configured with **strong passwords** for user accounts.
    - Use **Kubernetes Secrets** to store sensitive information, such as MySQL credentials.
    - Configure MySQL to only listen on the internal network or set up **Ingress** with proper firewall rules to limit access.
    - Use **TLS encryption** for database connections to secure data in transit.

**Q2**. **What is Ingress and Deployment in Kubernetes?**
  - **Ingress**: A Kubernetes resource that manages external access to services within a cluster, typically HTTP and HTTPS traffic. It allows you to define rules for routing traffic based on hostnames and paths to different services. An Ingress controller is required to implement these rules.
  - **Deployment**: A Kubernetes resource that manages the deployment and scaling of containerized applications. It ensures the desired number of replicas of a pod are running, provides updates to applications, and allows rollback to previous versions if needed.

**Q3**. **What are Kubernetes Services?**
  - **Kubernetes Services** provide stable IP addresses and DNS names for accessing sets of pods. There are different types of services:
    - **ClusterIP**: Exposes the service on an internal IP within the cluster.
    - **NodePort**: Exposes the service on each node's IP at a static port.
    - **LoadBalancer**: Exposes the service externally through a cloud provider’s load balancer.
    - **ExternalName**: Maps the service to an external DNS name.

**Q4**. **How does Kubernetes control and manage containers?**
  - Kubernetes manages containers through **Pods**, which are the smallest deployable units in Kubernetes. Containers are encapsulated within Pods and are scheduled across nodes in the cluster.
  - **Kubernetes Controllers** (such as Deployments, StatefulSets, and ReplicaSets) are responsible for managing the desired state of applications and ensuring that the actual state matches the desired state. If a container crashes, Kubernetes will automatically restart it to maintain the desired state.
  - **Kubernetes Scheduler** determines which nodes the pods should run on, based on resource availability and constraints.

**Q5**. **How do you implement resource limits and requests?**
  - In Kubernetes, you can specify resource limits and requests for Pods in their specifications. Resource **requests** define the minimum amount of resources (CPU, memory) required by a container to run. **Limits** define the maximum resources a container can consume.
  - Example:
    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
      name: example-pod
    spec:
      containers:
      - name: example-container
        image: nginx
        resources:
          requests:
            memory: "64Mi"
            cpu: "250m"
          limits:
            memory: "128Mi"
            cpu: "500m"
    ```

**Q6**. **What are sidecar containers in a service mesh?**
  - **Sidecar containers** are secondary containers that run alongside the main application container within the same Pod in Kubernetes. In a service mesh, sidecar containers are used to handle tasks such as **logging**, **monitoring**, **security**, or **service communication** (e.g., through a proxy like Envoy). These sidecars offload responsibilities from the main application container, enabling a more modular and scalable system.

**Q7**. **Explain Kubernetes Network Policies with examples.**
  - **Kubernetes Network Policies** are used to define rules for controlling the network traffic between Pods. They can restrict which Pods can communicate with each other based on labels, IP addresses, and ports.
  - Example of a network policy that allows traffic from Pods with the label `role=frontend` to Pods with the label `role=backend`:
    ```yaml
    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: allow-frontend-to-backend
    spec:
      podSelector:
        matchLabels:
          role: backend
      ingress:
        - from:
            - podSelector:
                matchLabels:
                  role: frontend
    ```

**Q8**. **Difference between StatefulSets and Deployments?**
  - **StatefulSets** are used to manage stateful applications that require stable, unique network identifiers and persistent storage. Pods created by StatefulSets have a predictable identity (e.g., `pod-0`, `pod-1`) and persistent volumes that are retained across restarts.
  - **Deployments** are used for stateless applications, where Pods can be replaced or recreated freely without losing state. Deployments manage the scaling and rolling updates of Pods, but Pods do not have persistent identities.

**Q9**. **Kubernetes architecture explanation.**
  - Kubernetes follows a **master-slave** architecture:
    - **Master Node**: The control plane that manages the cluster. It includes the API server, scheduler, controller manager, and etcd (distributed key-value store).
    - **Worker Nodes**: These are the nodes where the application workloads (Pods) run. Each worker node contains a Kubelet (manages the node), a container runtime (e.g., Docker), and a Kube Proxy (manages network connectivity).
    - **etcd**: A key-value store that holds the cluster's configuration data, state, and metadata.

**Q10**. **If a Kubernetes node is unresponsive, what steps do you take?**
  - First, check the node’s status using `kubectl get nodes` to identify if it's `NotReady`.
  - Use `kubectl describe node <node-name>` to check for any issues related to CPU, memory, or disk usage.
  - Check the **kubelet** logs on the node to see if there are any errors.
  - If the node is persistently unresponsive, cordon it to prevent new Pods from being scheduled (`kubectl cordon <node-name>`), and then drain it to safely evict the Pods (`kubectl drain <node-name>`).
  - Restart the node if possible, or consider removing it from the cluster if it cannot be recovered.

**Q11**. **What are the different Kubernetes objects?**
  - Common Kubernetes objects include:
    - **Pod**: The smallest and simplest Kubernetes object, which represents a running container or group of containers.
    - **Service**: A stable network endpoint to access a set of Pods.
    - **Deployment**: Manages stateless applications and controls rolling updates.
    - **StatefulSet**: Manages stateful applications with persistent storage.
    - **ReplicaSet**: Ensures that a specified number of Pod replicas are running.
    - **DaemonSet**: Ensures that a copy of a Pod runs on all or specific nodes in the cluster.
    - **Job**: Manages batch jobs that run to completion.
    - **CronJob**: Schedules jobs to run periodically based on a cron expression.

**Q12**. **Difference between ClusterIP and NodePort?**
  - **ClusterIP**: The default Kubernetes service type. It exposes the service on an internal IP address within the cluster, making it accessible only from within the cluster.
  - **NodePort**: Exposes the service on a static port on each node’s IP address. This allows external access to the service via `<NodeIP>:<NodePort>`, making it accessible from outside the cluster.

**Q13**. **When would you use LoadBalancer service?**
  - A **LoadBalancer** service is used when you want to expose a service to external clients (usually over the internet) and need a cloud provider’s load balancer to distribute traffic to the service. This is typically used in cloud environments like AWS, Azure, or GCP, where the load balancer automatically provisions and manages traffic.

**Q14**. **How do you troubleshoot a CrashLoopBackOff pod?**
  - To troubleshoot a `CrashLoopBackOff` pod:
    1. Check the logs of the pod using `kubectl logs <pod-name>`.
    2. If the pod has multiple containers, specify the container using the `-c` flag: `kubectl logs <pod-name> -c <container-name>`.
    3. Check the **events** related to the pod using `kubectl describe pod <pod-name>`.
    4. If necessary, update the pod’s configuration to fix issues, such as missing environment variables, misconfigured ports, or insufficient resources.
    5. Use `kubectl get pods` to see if the pod keeps restarting, and verify the resource limits.

**Q15**. **Implement blue-green deployments in Kubernetes.**
  - A blue-green deployment strategy involves running two identical environments (blue and green). The blue environment represents the live version, while the green environment is used for the new version. The switch between the environments is done by updating the service to point to the green environment.
  - Example:
    1. Deploy the new version as a new deployment (green).
    2. Update the service to point to the green deployment.
    3. Once green is stable, delete or scale down the blue deployment.

**Q16**. **How do you secure a Kubernetes cluster?**
  - Secure a Kubernetes cluster by:
    - Using **Role-Based Access Control (RBAC)** to limit permissions.
    - Enabling **Network Policies** to restrict pod-to-pod communication.
    - Using **PodSecurityPolicies** to enforce security constraints on pods.
    - Ensuring that etcd is encrypted and properly secured.
    - Implementing **TLS** for all communication between components.
    - Using **Kubernetes Secrets** to store sensitive data securely.

**Q17**. **What security measures do you implement in Kubernetes?**
  - Implement security measures like:
    - **Image scanning** to detect vulnerabilities in container images.
    - Enforcing the use of **immutable images**.
    - Setting resource limits and requests to prevent DoS attacks.
    - Enabling **audit logging** to track access and actions.
    - Restricting **privileged containers** and running containers with non-root users.

**Q18**. **EKS autoscaling Pods for high traffic.**
  - In AWS EKS, you can use the **Horizontal Pod Autoscaler (HPA)** to automatically scale pods based on CPU, memory, or custom metrics. Set the autoscaler to scale up or down as traffic increases or decreases.
    Example HPA setup:
    ```bash
    kubectl autoscale deployment my-app --cpu-percent=50 --min=1 --max=10
    ```

**Q19**. **Setup alerts when Pod CPU exceeds 80% for 5+ mins.**
  - Set up **Prometheus** with **Alertmanager** to monitor CPU usage and send alerts when usage exceeds 80% for more than 5 minutes. Example alert rule in Prometheus:
    ```yaml
    groups:
    - name: cpu-alerts
      rules:
      - alert: HighCPUUsage
        expr: sum(rate(container_cpu_usage_seconds_total{container!="",pod!="",namespace="default"}[5m])) by (pod) > 0.8
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "Pod CPU usage exceeds 80% for 5+ minutes"
    ```

**Q20**. **Grafana dashboard for HTTP latency in EKS.**
  - To monitor HTTP latency in EKS using Grafana:
    - Install **Prometheus** in the cluster to collect metrics.
    - Set up **Prometheus** as a data source in **Grafana**.
    - Create a Grafana dashboard to visualize the HTTP latency using the Prometheus query:
      ```prometheus
      http_request_duration_seconds_bucket{job="my-app",le="0.5"}
      ```

## ✅ Monitoring & Logging

**Q1**. **Troubleshoot high CPU in Kubernetes pods.**
  - To troubleshoot high CPU usage in Kubernetes pods:
    - **Step 1**: Use `kubectl top pod <pod_name>` to check the resource utilization of the pod.
    - **Step 2**: Check the pod's resource limits and requests to ensure they are set appropriately in the deployment YAML file.
    - **Step 3**: Use `kubectl describe pod <pod_name>` to check for events and logs that could indicate issues.
    - **Step 4**: Inspect logs using `kubectl logs <pod_name>` to see if there are any processes consuming excessive CPU.
    - **Step 5**: Consider scaling the application by increasing the number of replicas or adjusting CPU limits.

**Q2**. **Difference between blackbox and whitebox monitoring.**
  - **Blackbox monitoring** refers to monitoring systems from the outside, without knowledge of the internal workings. It typically tests the system's behavior from the user's perspective (e.g., monitoring HTTP response times, availability, etc.).
    - Example: Ping tests, HTTP/HTTPS health checks, monitoring a website's uptime.
  - **Whitebox monitoring** refers to monitoring systems from within, having access to the internal metrics, logs, and performance data. It gives insights into the application's internal operations, such as memory usage, CPU utilization, and error rates.
    - Example: Monitoring Kubernetes pod CPU/memory usage, application-level logging, database query performance.

**Q3**. **Visualize logs using Loki and Grafana.**
  - **Loki** is a log aggregation system that stores logs from various sources. It integrates well with **Grafana**, which can be used to visualize logs from Loki.
  - **Steps**:
    - Install and configure Loki on the cluster or infrastructure.
    - Install **Grafana** and configure it to connect to the Loki data source.
    - Create dashboards in Grafana to visualize log data (e.g., error logs, request logs).
    - Use the query language (LogQL) in Grafana to filter, aggregate, and visualize log data.
    - Set up alerts based on log patterns or error thresholds.

**Q4**. **Configure Grafana dashboard.**
  - To configure a **Grafana dashboard**:
    - **Step 1**: Install Grafana and configure it to connect to data sources (e.g., Prometheus, Loki).
    - **Step 2**: Create a new dashboard by navigating to the "Create Dashboard" option.
    - **Step 3**: Add panels to the dashboard by selecting the data source and writing the relevant query (e.g., Prometheus query to show CPU usage).
    - **Step 4**: Customize the panels by setting graph types, thresholds, and legends.
    - **Step 5**: Save the dashboard for future use and configure access permissions if needed.
    - **Step 6**: Set up alerts to notify when a metric crosses a threshold (e.g., high CPU usage).

**Q5**. **Alerting using CloudWatch, SNS, and other tools.**
  - **Amazon CloudWatch** is a monitoring service for AWS resources. It can be used to set up alerts based on metrics such as CPU usage, memory usage, or custom metrics.
  - **Steps**:
    - **Step 1**: Create CloudWatch Alarms for specific metrics (e.g., if CPU usage > 80%).
    - **Step 2**: Configure **SNS (Simple Notification Service)** to send notifications when an alarm is triggered.
    - **Step 3**: Subscribe to the SNS topic (e.g., email or SMS notifications).
    - **Step 4**: Use third-party tools like **PagerDuty** or **Opsgenie** for advanced alerting and on-call management.

**Q6**. **Importance of close monitoring.**
  - **Close monitoring** is essential for maintaining system health, performance, and reliability. It helps identify and resolve issues before they become critical.
  - Key benefits:
    - **Early detection of failures**: By monitoring key metrics like CPU, memory, and network, you can detect performance degradation or failures early.
    - **Optimized resource utilization**: Monitoring helps identify underutilized resources, allowing you to right-size them and reduce costs.
    - **Improved reliability**: By setting up alerts and proactively addressing issues, you can ensure high availability and prevent downtime.
    - **Compliance and security**: Close monitoring is vital for auditing, meeting regulatory requirements, and identifying potential security breaches.

---
