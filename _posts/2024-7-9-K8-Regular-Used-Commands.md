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

These examples cover various aspects of Kubernetes management and operations. For detailed options and additional commands, refer to the Kubernetes documentation or use `kubectl --help` for comprehensive command details.