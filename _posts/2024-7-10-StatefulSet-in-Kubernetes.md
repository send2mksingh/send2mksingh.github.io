---
 layout: post
 title: Statefulset in Kubernetes
---

 ### StatefulSet in Kubernetes

**Definition**: A StatefulSet is a Kubernetes resource used to manage stateful applications, which require
stable and unique network identities and persistent storage.

**Use**: StatefulSets ensure that each pod has a consistent name and storage, which is crucial for applications
like databases, where data consistency and stable network identities are important.

### Key Points:
- **Stable Network Identity**: Each pod gets a unique, stable hostname (e.g., `pod-name-0`, `pod-name-1`).
- **Persistent Storage**: Each pod can have its own persistent storage, which remains even if the pod is deleted or
rescheduled.
- **Ordered Deployment and Scaling**: Pods are created, updated, and deleted in a specific order, ensuring 
dependencies are met.

### Example Use Case:
- **Databases**: Running a database like MySQL or MongoDB where each instance needs its own storage and a stable
network identity.

### Simple Example:
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  serviceName: "nginx"
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
  volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      accessModes: [ "ReadWriteOnce" ]
      resources:
        requests:
          storage: 1Gi
```

This example sets up an Nginx StatefulSet with 3 replicas, each having its own persistent storage.
                                      
