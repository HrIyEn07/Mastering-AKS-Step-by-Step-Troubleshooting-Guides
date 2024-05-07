 
# Module-02: Kubernetes Internals, Security, and Metrics

## Interview Questions:

1. **Spike in Network Traffic:**
   - **Question:** You've observed a sudden spike in network traffic within your Kubernetes cluster. How do you investigate and mitigate this issue?

2. **Failure of Critical Kubernetes Components:**
   - **Question:** A critical Kubernetes component, such as the kubelet or kube-proxy, is reporting errors or failures. How would you troubleshoot and address these issues?

3. **Pod Unable to Communicate with External Service:**
   - **Question:** Describe a scenario where a Kubernetes pod is unable to communicate with an external service. How would you diagnose and resolve this connectivity issue?

4. **Misconfigured Security Policy:**
   - **Question:** You suspect that a misconfigured security policy is preventing pods from accessing certain resources within the cluster. How do you troubleshoot and correct this issue?

5. **High CPU Utilization in Control Plane:**
   - **Question:** The Kubernetes control plane is experiencing high CPU utilization. How would you identify the source of this increased resource usage and mitigate it?

6. **Node Instability and Eviction:**
   - **Question:** One of your Kubernetes nodes is repeatedly becoming unhealthy and being evicted from the cluster. How do you diagnose and address this node instability?

7. **Stuck Rolling Update of Deployment:**
   - **Question:** You've encountered a problem where a Kubernetes deployment is stuck in a rolling update, with some pods failing to terminate. How would you troubleshoot and resolve this issue?

8. **Intermittent Network Timeouts Between Pods:**
   - **Question:** A Kubernetes pod is experiencing intermittent network timeouts when communicating with other pods in the same cluster. How would you investigate and fix this networking issue?

## Answers:

1. **Spike in Network Traffic:**
   - First, I'd use tools like `kubectl top nodes` and `kubectl top pods` to identify the nodes and pods experiencing the highest network traffic.
   - Then, I'd inspect the network policies and service configurations using `kubectl get networkpolicies` and `kubectl get services` to ensure there are no misconfigurations or bottlenecks.
   - Additionally, I'd check for any abnormal network activity using network monitoring tools or packet capture utilities like `tcpdump`.
   - If necessary, I might scale up the affected pods or nodes to handle the increased traffic, or implement rate limiting or traffic shaping to prevent overload.

2. **Failure of Critical Kubernetes Components:**
   - First, I'd check the logs for the failing component using `kubectl logs <component-pod-name>` to look for any error messages or stack traces.
   - Then, I'd examine the health of the node where the component is running using `kubectl describe node <node-name>` to see if there are any underlying issues such as resource constraints or hardware failures.
   - If the component continues to report errors, I might try restarting the component pod or the entire node to attempt to restore functionality.
   - Additionally, I'd consider upgrading the Kubernetes version or applying any relevant patches or updates to address known issues with the component.

3. **Pod Unable to Communicate with External Service:**
   - First, I'd ensure that the service is correctly defined and exposes the appropriate ports using `kubectl get svc <service-name>`.
   - Then, I'd check if the service endpoints are correctly configured and pointing to the intended pods using `kubectl describe svc <service-name>`.
   - Next, I'd inspect the network policies and firewall rules to ensure that traffic is allowed to reach the service from external sources.
   - If necessary, I'd test connectivity to the service using tools like `curl` or `telnet` from external nodes to troubleshoot any network routing issues.
   - Finally, I might consider using a service mesh like Istio to manage and secure communication between pods and external services more effectively.

4. **Misconfigured Security Policy:**
   - First, I'd review the existing network policies and role-based access control (RBAC) rules using `kubectl get networkpolicies` and `kubectl get roles` to identify any policies that may be restricting pod communication.
   - Then, I'd examine the logs for the affected pods using `kubectl logs <pod-name>` to see if there are any permission denied errors or other indications of access issues.
   - If necessary, I'd adjust the network policies or RBAC rules to allow the required traffic, ensuring that pods have the necessary permissions to access the required resources.
   - Additionally, I'd consider using tools like `kubectl auth can-i` to test whether a given user or service account has the necessary permissions to perform specific actions within the cluster.

5. **High CPU Utilization in Control Plane:**
   - First, I'd identify the specific components within the control plane experiencing high CPU utilization using `kubectl top pods -n kube-system` to inspect resource usage.
   - Then, I'd check the logs for the affected components using `kubectl logs <component-pod-name> -n kube-system` to look for any error messages or stack traces.
   - Next, I'd examine the configuration and workload of the control plane components to see if there are any misconfigurations or resource-intensive tasks causing the CPU spike.
   - If necessary, I'd consider scaling up the control plane nodes or optimizing the resource allocation for the affected components to mitigate the increased resource usage.

6. **Node Instability and Eviction:**
   - First, I'd check the events associated with the node using `kubectl describe node <node-name>` to see if there are any error messages or warnings indicating instability.
   - Then, I'd inspect the logs for the kubelet and other node components using `kubectl logs <kubelet-pod-name> -n kube-system` to look for any issues or failures.
   - Next, I'd examine the node's resource usage and capacity using `kubectl top node <node-name>` to see if there are any resource constraints or bottlenecks contributing to instability.
   - If the node continues to experience instability, I might try restarting the kubelet or other affected components, or consider draining and decommissioning the node if it cannot be stabilized.

7. **Stuck Rolling Update of Deployment:**
   - First, I'd check the events associated with the deployment using `kubectl describe deployment <deployment-name>` to see if there are any error messages or warnings indicating issues with the update process.
   - Then, I'd inspect the status of the pods being rolled out using `kubectl get pods -l <selector>` to determine if any pods are failing to start or terminate.
   - Next, I'd examine the deployment's rollout history using `kubectl rollout history deployment <deployment-name>` to identify any failed or incomplete updates that may need to be rolled back.
   - If necessary, I might try manually updating the deployment using `kubectl set image deployment/<deployment-name> <container-name>=<image>:<tag>` to trigger a fresh rollout and resolve any stuck updates.

8. **Intermittent Network Timeouts Between Pods:**
   - First, I'd check the logs for the affected pods using `kubectl logs <pod-name>` to look for any network-related errors or warnings.
   - Then, I'd inspect the network policies and firewall rules using `kubectl get networkpolicies` and `iptables` to ensure that traffic is allowed to flow between the pods.
   - Next, I'd use tools like `traceroute` or `ping` from within the pods to diagnose any network routing issues or connectivity problems.
   - If necessary, I'd consider adjusting the pod's network configuration or service endpoints to use a different network interface or routing path to avoid intermittent timeouts.