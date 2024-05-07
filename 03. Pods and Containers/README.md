# Module-03: Pods and Containers

## Interview Questions:

1. **Intermittent Pod Performance Issues:**
   - **Question:** You're experiencing intermittent issues with a pod's performance. How would you troubleshoot and identify the root cause of these performance issues?

2. **Pod Unable to Access Storage Volume:**
   - **Question:** Describe a scenario where a pod is unable to access its storage volume. How do you diagnose and resolve this storage mounting issue?

3. **Excessive Resource Consumption by Container:**
   - **Question:** One of your containers is consuming excessive CPU or memory resources. How would you identify and mitigate resource contention issues within the pod?

4. **Unstable Pod Network Connectivity:**
   - **Question:** You've encountered a problem where a pod's network connectivity is unstable or intermittent. How would you investigate and fix this networking issue?

5. **DNS Resolution Issue:**
   - **Question:** Explain how you would troubleshoot and resolve issues related to DNS resolution within a Kubernetes cluster.

6. **Image Pull Errors:**
   - **Question:** You're unable to deploy a pod due to image pull errors. How do you diagnose and address these image-related issues?

7. **Docker Version Upgrade:**
   - **Question:** Describe the process of upgrading the Docker version used by containers within a Kubernetes cluster. What precautions would you take to ensure a smooth upgrade process?

8. **Stuck Pod Termination:**
   - **Question:** A pod is stuck in a terminating state and cannot be removed. How would you troubleshoot and force delete the stuck pod?

## Answers:

1. **Intermittent Pod Performance Issues:**
   - First, I'd check the pod's resource utilization using `kubectl top pod <pod-name>` to identify any spikes or patterns in CPU and memory usage.
   - Then, I'd inspect the pod's logs and application metrics using `kubectl logs <pod-name>` and monitoring tools like Prometheus to look for any performance-related errors or warnings.
   - Next, I'd consider enabling more detailed logging or profiling for the application to capture additional diagnostic information about its behavior.
   - If necessary, I might scale up the pod or adjust its resource requests and limits to provide additional capacity and improve performance.

2. **Pod Unable to Access Storage Volume:**
   - First, I'd check the pod's configuration to verify that the volume mounts are correctly specified using `kubectl describe pod <pod-name>`.
   - Then, I'd inspect the events associated with the pod using `kubectl describe pod <pod-name>` to see if there are any error messages related to volume mounting.
   - Next, I'd check the status of the underlying storage resources using `kubectl get pv` and `kubectl get pvc` to ensure they are available and correctly provisioned.
   - If the issue persists, I'd review the pod's security context and any relevant storage class configurations to ensure they are compatible with the volume type.
   - Finally, I might consider recreating the pod or deleting and recreating the associated persistent volume claim (PVC) to trigger a fresh volume mount attempt.

3. **Excessive Resource Consumption by Container:**
   - First, I'd use `kubectl top pod <pod-name>` to identify the container within the pod that is consuming the most CPU or memory resources.
   - Then, I'd inspect the container's resource requests and limits using `kubectl describe pod <pod-name>` to determine if they are appropriately configured.
   - Next, I'd review the container's configuration and workload to see if there are any resource-intensive processes or tasks contributing to the resource contention.
   - If necessary, I might adjust the container's resource requests and limits, or consider scaling up the pod to provide additional capacity and alleviate the resource constraints.

4. **Unstable Pod Network Connectivity:**
   - First, I'd check the pod's network configuration using `kubectl describe pod <pod-name>` to ensure it has the correct network policies and service endpoints configured.
   - Then, I'd use tools like traceroute or ping from within the pod to test connectivity to other pods or external endpoints and diagnose any network routing issues.
   - Next, I'd inspect the network policies and firewall rules using `kubectl get networkpolicies` and `iptables` to ensure that traffic is allowed to flow between the pods.
   - If necessary, I'd consider adjusting the pod's network configuration or service endpoints to use a different network interface or routing path to avoid intermittent timeouts.

5. **DNS Resolution Issue:**
   - First, I'd verify that the DNS service is running correctly within the cluster using `kubectl get svc kube-dns -n kube-system`.
   - Then, I'd check the DNS configuration of the affected pod using `kubectl exec <pod-name> -- nslookup <domain-name>` to see if DNS resolution is working as expected.
   - If DNS resolution is failing, I'd inspect the pod's network configuration and DNS settings to ensure they are correctly configured.
   - Next, I'd check for any issues with DNS caching or DNS server connectivity using tools like dig or nslookup from within the pod.
   - Finally, I might consider restarting the DNS service or updating the pod's DNS settings if necessary to resolve the issue.

6. **Image Pull Errors:**
   - First, I'd check the pod's status and events using `kubectl describe pod <pod-name>` to see if there are any error messages related to image pulling.
   - Then, I'd inspect the container's image pull policy and repository credentials to ensure they are correctly configured in the pod's manifest.
   - Next, I'd verify that the container image exists in the specified repository and is accessible from the cluster's network.
   - If necessary, I'd check for any network connectivity issues or firewall rules that may be preventing the pod from pulling the container image.
   - Finally, I might consider using a different container image repository or adjusting the pod's image pull settings to resolve the image pull errors.

7. **Docker Version Upgrade:**
   - First, I'd review the release notes for the new Docker version to identify any compatibility issues or breaking changes that may affect the Kubernetes cluster.
   - Then, I'd schedule a maintenance window for the upgrade and communicate the plan to stakeholders to minimize disruption to ongoing workloads.
   - Next, I'd drain and cordon the nodes in the cluster to gracefully evict any running pods and prevent new pods from being scheduled on the nodes during the upgrade process.
   - If necessary, I'd update the Docker version on each node using the appropriate package manager or container runtime tool, ensuring that all dependencies are met and configurations are preserved.
   - Finally, I'd uncordon the nodes and resume normal scheduling operations once the Docker upgrade is complete, monitoring the cluster for any issues or errors that may arise during the transition.

8. **Stuck Pod Termination:**
   - First, I'd attempt to delete the stuck pod using `kubectl delete pod <pod-name> --force --grace-period=0` to force delete the pod immediately.
   - If the pod cannot be deleted using the force delete command, I'd check the pod's status and events using `kubectl describe pod <pod-name>` to see if there are any error messages or warnings indicating why the pod is stuck.
   - Then, I'd inspect the node's logs and system metrics using `kubectl logs <kubelet-pod-name> -n kube-system` and `kubectl top node <node-name>` to identify any issues or resource constraints preventing the pod from terminating.
   - If necessary, I might try restarting the kubelet or other affected components on the node to clear any stuck pod termination processes and allow the pod to be deleted successfully.ss