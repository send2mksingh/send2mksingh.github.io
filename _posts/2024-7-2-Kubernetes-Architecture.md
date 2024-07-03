---
 layout: post
 title: Kubernetes Architectures
--- 
   
   Kubernetes Cluster - is the collection of nodes (including master node and worker nodes).

   **Role of Master Node:**
    - Kubernetes cluster contains containers running on Bare metal/VM instance/Cloud instance or all mix.
    - Kubernetes designates one ore more of these or master and all others as workers.

    - The master is now going to run set of K8s processes. These processes will ensure smooth functioning
      of cluster and these processes are called "Control Plane".

    - This can be multi master for high availability.
    - Master runs control plane to run cluster smoothly.

    
   **Components of Control Plane(Master Node)**
    **Kube-api-server:**
    - (Responsible for all communication) : This api server interacts directly with user ( we           apply yml or json manifest to kube-api-server).

    - This Kube-api-server is meant to be scale automatically as per load.
    - Kube-api-server is fron-end of Control Plane.
    - this is the front-end of master node.

    **ETCD:**
    - Stores metadata and status of cluster.
    - etcd is consistent and high available store (stores value in key-value pair).
    - sourc of touch for cluster state (stores info about state of cluster)
    - means no. of pods and containers and their status.

    **etcd has following features:**
    - fully replicated - the entire state is available on every node in the cluster.
    - secure - implements automatic TLS with optimal client-certificate authentication.
    - fast - benchmarked at 10,000 within per second.

    **Kube-Scheduler:**
    - When users make request for the creation and management fo pods, kube-scheduler is going to 
      take   actions on these requests.
    - handls pod creation and management.
    - Kube-Scheduler match/assign any node to create and run pods.
    - A scheduler watches for newly created pods that have no node assigned for every pod that 
      the scheduler discovers, the scheduler becomes responsible for finding best nodes for that pod to run on.
    - Scheduler gets the information for hardware configuration from configuration files and scheduels  the pods on nodes accordingly.  


    **Controller Manager:**
    - Make sure actual state of cluster matches to desired state.
    - Two possible choices for Controller Manager-
    - 1-If K8s on cloud then it will be cloud-controller-manager.
    - 2-If K8 on non-cloud then it will be kube-controller-manager.
