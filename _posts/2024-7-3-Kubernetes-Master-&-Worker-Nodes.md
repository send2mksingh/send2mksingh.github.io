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
  - kube-proxy runs on each node and this make sure that each pod will get its own unique ip addresses.
  - These 3 components collectively consist "node".

 **POD**
  - Smallest unit of kubernetes.
  - Pod is a group of one or more container that are deployed together on the same host.
  - A Cluster is a gorup of nodes.
  - A Cluster has atleast one worker node and master node.
  - In Kubernetes, the control unit is the POD, not containers.
  - Consist of one or more tightly coupled containers.
  - POD runs on node, which is control by master.
  - Kubernetes only knows about PODs (does not know about individual containers).
  - Can not start containers without a POD.
  - One POD usually contains one container.




      ***............................to learn more follow this blog...............................***