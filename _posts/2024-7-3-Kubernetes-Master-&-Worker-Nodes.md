---
 layout: post
 title: Master node and Worker nodes Working
---

- Components on master that runs controller:

   Node Controller: for checking the cloud provider to determine if a node has been detected in the cloud ofter it stops responding.

   Route Controller: responsible for sharing up network routes on your cloud.

   Service Controller: responsible for load balances on your cloud against services of type load balancer.

   Volume Controller: for creating, attching and mounting volumes and interacting with the cloud porvider to orchestrate volume.

 **Workder nodes**
 - node is going to run 3 important piece of software/process.

 **Kubelete**
 - Agent running on the node.
 - Listens to kubernetes master (eg- pod creation request).
 - Use port 10255
 - send successful/faile reports to master.

 **Container Enginer/Runtime**
 - works with kubelet
 - pulling image
 - start/stop containers
 - exposing containers on ports specified in manifest
 - it could be docker, containerd and rocket

 **Kube-Proxy**
 - assign ip to each pod
 - it is required to assign ip addresses to pods (dynamic)
 - kube-proxy