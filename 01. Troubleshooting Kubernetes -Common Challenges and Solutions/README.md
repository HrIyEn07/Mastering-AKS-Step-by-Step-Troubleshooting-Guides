# Module-01: Troubleshooting Kubernetes: Common Challenges and Solutions

## Interview Questions

1. **Pod Failing to Start:** 
   - **Question:** Suppose a pod is failing to start. Walk me through the troubleshooting steps you would take to identify and resolve the issue.

2. **Kubernetes Deployment Stuck in 'Pending' State:** 
   - **Question:** You notice that a Kubernetes deployment is stuck in the 'Pending' state. How would you diagnose and troubleshoot this problem?

3. **Frequent Docker Container Crashes:** 
   - **Question:** One of your Docker containers within a pod is crashing frequently. How do you investigate the root cause of these crashes?

4. **Unresponsive Kubernetes API Server:** 
   - **Question:** Describe a scenario where the Kubernetes API server is unresponsive. How would you troubleshoot and restore its functionality?

5. **Inaccessible Service from External:** 
   - **Question:** A pod is running, but its associated service is not accessible externally. How would you troubleshoot this connectivity issue?

6. **Pod's Storage Volume Mounting Issue:** 
   - **Question:** You've encountered an issue where a pod's storage volume is not mounting correctly. What steps would you take to diagnose and fix this problem?

7. **DNS Resolution within a Kubernetes Cluster:** 
   - **Question:** Explain how you would troubleshoot and resolve issues related to DNS resolution within a Kubernetes cluster.

8. **Configuration Changes Not Applied:** 
   - **Question:** You've made changes to a pod's configuration, but they are not being applied. How do you debug and rectify this configuration issue? 

## Answers:

1. **Pod Failing to Start:** 
   - First, I'd check the pod's status and events using `kubectl describe pod <pod-name>` to identify any error messages or issues.
   - Then, I'd inspect the pod's logs using `kubectl logs <pod-name>` to look for any application-specific errors or failures.
   - Next, I'd verify that the necessary resources (CPU, memory) are available on the node where the pod is scheduled.
   - If the issue persists, I'd examine the pod's configuration, including its readiness and liveness probes, to ensure they are correctly configured.
   - Finally, I might consider restarting the pod or updating its configuration if necessary.

2. **Kubernetes Deployment Stuck in 'Pending' State:** 
   - First, I'd check the events associated with the deployment using `kubectl describe deployment <deployment-name>` to see if there are any error messages or warnings.
   - Then, I'd inspect the status of the underlying pods using `kubectl get pods -o wide` to determine if they are being scheduled correctly.
   - If the pods are stuck in a 'ContainerCreating' state, I'd examine the cluster's node resources using `kubectl describe node` to ensure there are sufficient resources available.
   - Additionally, I'd check for any issues with the container image or network connectivity that may be preventing the pods from starting.
   - If necessary, I might scale down the deployment or manually delete stuck pods to trigger rescheduling.

3. **Frequent Docker Container Crashes:** 
   - First, I'd retrieve the logs for the crashing container using `kubectl logs <pod-name> -c <container-name>` to identify the specific error messages.
   - Then, I'd inspect the container's resource usage and limits using `kubectl describe pod <pod-name>` to determine if resource constraints are contributing to the crashes.
   - If the crashes appear to be related to application code, I'd review the application logs and stack traces for any clues about the root cause.
   - Additionally, I'd consider updating the container image or adjusting the container's configuration to address any known issues.
   - Finally, I might enable more detailed logging or monitoring for the container to capture additional diagnostic information.

4. **Unresponsive Kubernetes API Server:** 
   - First, I'd check the status of the API server component using `kubectl get componentstatuses` to see if it's reporting as healthy.
   - If the API server is unresponsive, I'd examine the logs for the API server pod using `kubectl logs <api-server-pod-name>` to look for any error messages or stack traces.
   - Then, I'd verify the health of the etcd cluster, as the API server relies on etcd for storing cluster state. I'd use `etcdctl cluster-health` to check the health of the etcd cluster.
   - If necessary, I might try restarting the API server pod or the entire control plane to attempt to restore functionality.
   - Additionally, I'd consider scaling up the control plane nodes or optimizing the cluster's resource allocation to prevent future API server failures.

5. **Inaccessible Service from External:** 
   - First, I'd ensure that the service is correctly defined and exposes the appropriate ports using `kubectl get svc <service-name>`.
   - Then, I'd check if the service endpoints are correctly configured and pointing to the intended pods using `kubectl describe svc <service-name>`.
   - Next, I'd inspect the network policies and firewall rules to ensure that traffic is allowed to reach the service from external sources.
   - If necessary, I'd test connectivity to the service using tools like `curl` or `telnet` from external nodes to troubleshoot any network routing issues.
   - Finally, I might consider using a service mesh like Istio to manage and secure communication between pods and external services more effectively.

6. **Pod's Storage Volume Mounting Issue:** 
   - First, I'd check the pod's configuration to verify that the volume mounts are correctly specified using `kubectl describe pod <pod-name>`.
   - Then, I'd inspect the events associated with the pod using `kubectl describe pod <pod-name>` to see if there are any error messages related to volume mounting.
   - Next, I'd check the status of the underlying storage resources using `kubectl get pv` and `kubectl get pvc` to ensure they are available and correctly provisioned.
   - If the issue persists, I'd review the pod's security context and any relevant storage class configurations to ensure they are compatible with the volume type.
   - Finally, I might consider recreating the pod or deleting and recreating the associated persistent volume claim (PVC) to trigger a fresh volume mount attempt.

7. **DNS Resolution within a Kubernetes Cluster:** 
   - First, I'd verify that the DNS service is running correctly within the cluster using `kubectl get svc kube-dns -n kube-system`.
   - Then, I'd check the DNS configuration of the affected pod using `kubectl exec <pod-name> -- nslookup <domain-name>` to see if DNS resolution is working as expected.
   - If DNS resolution is failing, I'd inspect the pod's network configuration and DNS settings to ensure they are correctly configured.
   - Next, I'd check for any issues with DNS caching or DNS server connectivity using tools like `dig` or `nslookup` from within the pod.
   - Finally, I might consider restarting the DNS service or updating the pod's DNS settings if necessary to resolve the issue.

8. **Configuration Changes Not Applied:** 
   - First, I'd verify that the configuration changes have been applied to the desired resource using `kubectl get <resource-type> <resource-name> -o yaml` to inspect the current configuration.
   - Then, I'd check for any errors or warnings related to the configuration changes using `kubectl describe <resource-type> <resource-name>` to identify any issues preventing the changes from being applied.
   - Next, I'd ensure that the appropriate RBAC permissions are in place to allow the necessary modifications to the resource.
   - If the changes are still not being applied, I'd consider restarting the controller responsible for managing the resource using `kubectl rollout restart <controller-name>` to force a reconciliation of the desired state.