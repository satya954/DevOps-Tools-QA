				**Kubernetes Interview Questions:**

				---------- Beginner Level: -----------
 
1. What is Kubernetes. ?
Ans:

2. What are the main components of Kubernetes ?
Ans:

3. What is a Pod in Kubernetes ?
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









