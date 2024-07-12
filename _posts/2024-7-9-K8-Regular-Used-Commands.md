---
 layout: post
 title: K8 Regular used commands
---


Listing all Kubernetes commands with examples in a single response would be too extensive. Instead, here are some essential Kubernetes commands categorized by their common use cases, each with a brief explanation and example:

### Cluster Management

1. **kubectl cluster-info**
   - **Use**: Display cluster information.
   - **Example**: 
     ```bash
     kubectl cluster-info
     ```

2. **kubectl get nodes**
   - **Use**: List all nodes in the cluster.
   - **Example**: 
     ```bash
     kubectl get nodes
     ```

### Workload Management

1. **kubectl create deployment \<name\> --image=\<image\>**
   - **Use**: Create a deployment using a container image.
   - **Example**: 
     ```bash
     kubectl create deployment nginx --image=nginx:latest
     ```

2. **kubectl scale deployment \<name\> --replicas=\<count\>**
   - **Use**: Scale a deployment to a specific number of replicas.
   - **Example**: 
     ```bash
     kubectl scale deployment nginx --replicas=3
     ```

### Pod Management

1. **kubectl get pods**
   - **Use**: List all pods.
   - **Example**: 
     ```bash
     kubectl get pods
     ```

2. **kubectl logs \<pod-name\>**
   - **Use**: Display logs from a pod.
   - **Example**: 
     ```bash
     kubectl logs nginx-abc123
     ```

### Service Management

1. **kubectl get services**
   - **Use**: List all services.
   - **Example**: 
     ```bash
     kubectl get services
     ```

2. **kubectl expose deployment \<name\> --port=\<port\> --target-port=\<target-port\> --type=\<service-type\>**
   - **Use**: Expose a deployment as a service.
   - **Example**: 
     ```bash
     kubectl expose deployment nginx --port=80 --target-port=8080 --type=NodePort
     ```

### Configuration Management

1. **kubectl apply -f \<filename\>**
   - **Use**: Apply a configuration file to the cluster.
   - **Example**: 
     ```bash
     kubectl apply -f deployment.yaml
     ```

2. **kubectl get \<resource-type\>**
   - **Use**: List resources of a specific type.
   - **Example**: 
     ```bash
     kubectl get deployments
     ```

### Advanced Operations

1. **kubectl create namespace \<namespace-name\>**
   - **Use**: Create a new namespace.
   - **Example**: 
     ```bash
     kubectl create namespace development
     ```

2. **kubectl proxy**
   - **Use**: Start a proxy to the Kubernetes API server.
   - **Example**: 
     ```bash
     kubectl proxy
     ```

### Cluster Maintenance

1. **kubectl drain \<node-name\>**
   - **Use**: Drain a node for maintenance.
   - **Example**: 
     ```bash
     kubectl drain node-1
     ```

2. **kubectl delete deployment \<name\>**
   - **Use**: Delete a deployment.
   - **Example**: 
     ```bash
     kubectl delete deployment nginx
     ```

### Security

1. **kubectl auth can-i \<verb\> \<resource\>**
   - **Use**: Check permissions for a specific action on a resource.
   - **Example**: 
     ```bash
     kubectl auth can-i create deployments
     ```

### Troubleshooting

1. **kubectl describe \<resource-type\> \<resource-name\>**
   - **Use**: Show detailed information about a resource.
   - **Example**: 
     ```bash
     kubectl describe pod nginx-abc123
     ```

2. **kubectl exec -it \<pod-name\> -- \<command\>**
   - **Use**: Execute a command in a running pod.
   - **Example**: 
     ```bash
     kubectl exec -it nginx-abc123 -- /bin/bash
     ```




Sure, here's a comprehensive list of Kubernetes commands with examples covering various aspects of cluster management, workload deployment, service management, configuration, networking, storage, security, and troubleshooting:

### Cluster Management

1. **View Cluster Info**
   - **Command**: 
     ```bash
     kubectl cluster-info
     ```
   - **Example**: Displays information about the Kubernetes cluster.

2. **List Nodes**
   - **Command**: 
     ```bash
     kubectl get nodes
     ```
   - **Example**: Lists all nodes in the cluster.

3. **View Kubernetes Version**
   - **Command**: 
     ```bash
     kubectl version
     ```
   - **Example**: Shows the client and server Kubernetes version information.

### Workload Management

1. **List Pods**
   - **Command**: 
     ```bash
     kubectl get pods
     ```
   - **Example**: Lists all pods in the current namespace.

2. **Describe Pod**
   - **Command**: 
     ```bash
     kubectl describe pod <pod-name>
     ```
   - **Example**: Provides detailed information about a specific pod.

3. **Create Deployment**
   - **Command**: 
     ```bash
     kubectl create deployment nginx --image=nginx:latest
     ```
   - **Example**: Deploys an nginx container using the latest nginx image.

4. **Scale Deployment**
   - **Command**: 
     ```bash
     kubectl scale deployment nginx --replicas=3
     ```
   - **Example**: Scales the number of replicas of the nginx deployment to 3.

5. **Delete Deployment**
   - **Command**: 
     ```bash
     kubectl delete deployment nginx
     ```
   - **Example**: Deletes the nginx deployment.

### Service Management

1. **List Services**
   - **Command**: 
     ```bash
     kubectl get services
     ```
   - **Example**: Lists all services in the current namespace.

2. **Expose Deployment**
   - **Command**: 
     ```bash
     kubectl expose deployment nginx --port=80 --target-port=80 --type=LoadBalancer
     ```
   - **Example**: Exposes the nginx deployment as a LoadBalancer service on port 80.

3. **Delete Service**
   - **Command**: 
     ```bash
     kubectl delete service nginx
     ```
   - **Example**: Deletes the nginx service.

### Configuration Management

1. **List ConfigMaps**
   - **Command**: 
     ```bash
     kubectl get configmaps
     ```
   - **Example**: Lists all ConfigMaps in the current namespace.

2. **Create ConfigMap from File**
   - **Command**: 
     ```bash
     kubectl create configmap my-config --from-file=config.yaml
     ```
   - **Example**: Creates a ConfigMap named `my-config` using data from `config.yaml`.

### Networking

1. **List Network Policies**
   - **Command**: 
     ```bash
     kubectl get networkpolicies
     ```
   - **Example**: Lists all network policies in the current namespace.

2. **Create Network Policy**
   - **Command**: 
     ```bash
     kubectl apply -f network-policy.yaml
     ```
   - **Example**: Applies a network policy defined in `network-policy.yaml`.

### Storage

1. **List PersistentVolumes**
   - **Command**: 
     ```bash
     kubectl get pv
     ```
   - **Example**: Lists all persistent volumes in the cluster.

2. **Create PersistentVolumeClaim**
   - **Command**: 
     ```bash
     kubectl apply -f pvc.yaml
     ```
   - **Example**: Applies a PersistentVolumeClaim (PVC) defined in `pvc.yaml`.

### Security

1. **List ServiceAccounts**
   - **Command**: 
     ```bash
     kubectl get serviceaccounts
     ```
   - **Example**: Lists all service accounts in the current namespace.

2. **Create RoleBinding**
   - **Command**: 
     ```bash
     kubectl create rolebinding my-rolebinding --role=my-role --user=my-user --namespace=my-namespace
     ```
   - **Example**: Creates a role binding granting `my-user` access to `my-role` in `my-namespace`.

### Troubleshooting

1. **View Pod Logs**
   - **Command**: 
     ```bash
     kubectl logs <pod-name>
     ```
   - **Example**: Displays logs from a specific pod.

2. **Exec into Pod**
   - **Command**: 
     ```bash
     kubectl exec -it <pod-name> -- /bin/bash
     ```
   - **Example**: Opens an interactive shell session inside a specific pod.

3. **View Events**
   - **Command**: 
     ```bash
     kubectl get events
     ```
   - **Example**: Lists recent events in the cluster.

These examples cover various Kubernetes commands used for managing clusters, deploying workloads, configuring services, networking, storage, security, and troubleshooting. Each command has specific options and flags that can be explored further using `kubectl --help` or by referring to the Kubernetes documentation for more details.