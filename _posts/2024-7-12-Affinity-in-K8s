---
 layout: post
 title: Affinity in K8s
---


In Kubernetes, **affinity** is a way to influence the scheduling of pods based on various rules and constraints. It helps ensure that pods are placed on specific nodes or alongside other pods based on certain conditions, improving workload distribution, availability, and performance.

There are three types of affinity/anti-affinity rules:

1. **Node Affinity**: Influences which nodes a pod can be scheduled on based on node labels.
2. **Pod Affinity**: Ensures that pods are scheduled on nodes with other specified pods.
3. **Pod Anti-Affinity**: Ensures that pods are not scheduled on nodes with other specified pods.

### Node Affinity

Node affinity works similarly to nodeSelector but provides more expressive and flexible rules.

Example:

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
          - key: disktype
            operator: In
            values:
            - ssd
  containers:
  - name: my-container
    image: nginx
```

In this example, the pod will only be scheduled on nodes that have the label `disktype=ssd`.

### Pod Affinity

Pod affinity ensures that a pod is scheduled on the same node or in the same topology domain as other specified pods.

Example:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  affinity:
    podAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchExpressions:
          - key: security
            operator: In
            values:
            - S1
        topologyKey: "kubernetes.io/hostname"
  containers:
  - name: my-container
    image: nginx
```

In this example, the pod will only be scheduled on nodes that already have pods with the label `security=S1`.

### Pod Anti-Affinity

Pod anti-affinity ensures that a pod is not scheduled on the same node or in the same topology domain as other specified pods.

Example:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  affinity:
    podAntiAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
      - labelSelector:
          matchExpressions:
          - key: app
            operator: In
            values:
            - frontend
        topologyKey: "kubernetes.io/hostname"
  containers:
  - name: my-container
    image: nginx
```

In this example, the pod will not be scheduled on nodes that already have pods with the label `app=frontend`.

### Soft vs. Hard Affinity

- **Required (Hard)**: The pod **must** be scheduled according to the rules. Uses `requiredDuringSchedulingIgnoredDuringExecution`.
- **Preferred (Soft)**: The pod **should** be scheduled according to the rules, but it's not mandatory. Uses `preferredDuringSchedulingIgnoredDuringExecution`.

Example of preferred affinity:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  affinity:
    nodeAffinity:
      preferredDuringSchedulingIgnoredDuringExecution:
      - weight: 1
        preference:
          matchExpressions:
          - key: disktype
            operator: In
            values:
            - ssd
  containers:
  - name: my-container
    image: nginx
```

In this example, Kubernetes will try to schedule the pod on a node with the label `disktype=ssd`, but it's not required.

### Summary

Using affinity rules in Kubernetes helps control pod placement, ensuring optimal use of resources and adherence to various constraints. This is crucial for applications that require specific hardware, need to be co-located, or should avoid certain nodes for reasons such as high availability or fault tolerance.