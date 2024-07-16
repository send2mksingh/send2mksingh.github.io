---
 layout: post
 title: Affinity in K8s
---


With the help of affinity we can define where to schedule pods for running on the bases of certain criteria and conditions. There are different types of affinities you can use to guide the scheduler in making these decisions:

### 1. Node Affinity

**Node Affinity** helps you specify rules about which nodes a pod should be scheduled on based on the labels on those nodes.

**Simple Example:**

Imagine you have nodes labeled with `type=fast` and `type=slow`. If you want a pod to only run on nodes labeled as `type=fast`, you can use node affinity to enforce this.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: type
            operator: In
            values:
            - fast
  containers:
  - name: my-container
    image: nginx
```

### 2. Pod Affinity

**Pod Affinity** we can add rules about placing pods close to other pods. This is useful when pods need to be co-located for reasons like low latency.


**Simple Example:**

Suppose you have a frontend pod that needs to run on the same node as your backend pod. You can set up pod affinity to achieve this.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: frontend
spec:
  affinity:
    podAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchExpressions:
          - key: app
            operator: In
            values:
            - backend
        topologyKey: "kubernetes.io/hostname"
  containers:
  - name: frontend-container
    image: nginx
```

### 3. Pod Anti-Affinity

**Pod Anti-Affinity** is the opposite of pod affinity. It helps you specify rules about placing pods away from other pods. This is useful when you want to ensure that certain pods do not run on the same node to avoid single points of failure.

**Simple Example:**

Imagine you have multiple instances of a database pod, and you don't want them all running on the same node. You can set up pod anti-affinity to ensure they are spread out.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-database-pod
spec:
  affinity:
    podAntiAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchExpressions:
          - key: app
            operator: In
            values:
            - database
        topologyKey: "kubernetes.io/hostname"
  containers:
  - name: my-database-container
    image: mysql
```

### In Summary
- **Node Affinity**: Determines on which nodes a pod can run based on node labels.
- **Pod Affinity**: Ensures pods are scheduled on the same or specific nodes with other specified pods.
- **Pod Anti-Affinity**: Ensures pods are not scheduled on the same nodes as other specified pods.

These affinities help in optimizing the placement of pods in a Kubernetes cluster, improving performance, fault tolerance, and resource utilization.