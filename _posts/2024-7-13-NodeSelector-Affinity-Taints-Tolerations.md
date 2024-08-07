---
 layout: post
 title: Node Selector-Affinity-Taints and Tolerations
---

**Topics to cover -Node Selector, Node affinity, Taints and Tolerations**

- **Ref - https://www.youtube.com/watch?v=O61HDmGUBJM**

- **Ref - https://github.com/iam-veeramalla/kubernetes-troubleshooting-zero-to-hero** 

- **Ref - https://github.com/iam-veeramalla/kubernetes-troubleshooting-zero-to-hero/blob/main/03-pods-not-schedulable/01-kind-cluster.yaml**

**Pods Scheduling** to work on this concept we need multi node cluster for this we can use kind or k3d.
**kind** kubernetes inside docker - that is if you are using things like kind your entire kubernetes cluster runs within a docker container and advantage because your kubernetes cluster running inside container they are very light weight so you can create multiple kubernetes cluster and also with large no. of nodes.


**Steps to install kind**

```

# For AMD64 / x86_64
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.23.0/kind-linux-amd64
# For ARM64
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.23.0/kind-linux-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

```
  
**Using go command**

```
go install sigs.k8s.io/kind@latest
```

**Create multi-node-config.yml file**

```

kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
  - role: worker

```

**Create the Cluster with Increased Timeout:**
```
kind create cluster --config kind-config.yaml --wait 5m --loglevel debug
```

**Commands to create clusters and check**

```
kind create cluster --name test-cluster    #creating test cluster
kind get clusters   #check all clusters
kubectl get nodes    #check the nodes
```

- creating, deleting and switching between different kubernetes cluster-------

```
kind delete cluster --name test-cluster   #delete the cluster
kubectl get nodes   #check nodes
kubectl config view  #show all kubernetes cluster connected to kube-config
kubectl config view| grep kind   #grep cluster name
kubectl config use-context  kind-kind    #switch between different clusters
kubectl get nodes -o wide

```

------------------------------------------------------------------

**Practical of NodeSelector**


```

vim deploy.yml


apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      nodeSelector:
        node-name: arm-worker
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80

```

- adding nodeSelector name in deploy yaml

```
kubectl apply -f deploy.yml
kubectl get pods    

```

- This will show pending pods



```

kubectl describe pods nginx-deployment-695f7dbcdd-d2kjx
 	

Warning  FailedScheduling  68s (x2 over 6m29s)  default-scheduler  0/4 nodes are available: 1 node(s) 
had untolerated taint {node-role.kubernetes.io/control-plane: }, 3 node(s) didn't match Pod's node 
affinity/selector. preemption: 0/4 nodes are available: 4 Preemption is not helpful for scheduling.

```


**- If you don't use node selector properly your pod scheduling will go to Failed Scheduling.**
- When we are doing **kubectl get nodes** it is showing 4 nodes but none of them are helpful to schedule the pods.

**Do**
```
kubectl edit pods nginx-deployment-695f7dbcdd-d2kjx

```
- you will see this pod or complete deployment is using the nodeSelector which says node name xyz 

------------------------------------------------------------------------


**nodeSelector** is the field in the Kubernetes pod and this field will help the nodes or tell the kube
scheduler that schedule the pod only on a particular.
**How do you indentify that node** in the deployment yml file or within the pod yml file you will provide a certain label
and if there is any node with that particular label only then schedule the pod on that particular node.

- If there is no node keep my pod in unschedulable status.

**Why do we need nodeSelector** assume you have a pod which is running an app that runs only on ARM processor, if you run same app on AMD processor linux then may be it will not work properly so for this reason you are telling the scheduler to schedule the pod
only on matching labels.


```
manoj@Ubuntu:~/kubernetes_practice$ kubectl get nodes
NAME                 STATUS   ROLES           AGE   VERSION
kind-control-plane   Ready    control-plane   91m   v1.30.0
kind-worker          Ready    <none>          91m   v1.30.0
kind-worker2         Ready    <none>          91m   v1.30.0
kind-worker3         Ready    <none>          91m   v1.30.0


kubectl edit node kind-worker   #same we can do using kubectl label node  command

- Go to the label section write **node-name: arm-worker  --adding label to the **worker node**

```


---------------------------------------------------------------------------
**Replay** We have an pod or app in our organization may be that will if it runs on window or node with adm processor or node with arm processor.

**Two things we have to follow** 
1. You will go to the node and you will add the particular label to the node once you get the this type of requirements from you developers

2. Once you add the label to the particuler node, you will go to the particular pod and add something called as field node selector within the pod


-----------------------------------------------------------------------------
**Debug** using **kubectl describe** command you can find the issue for pending or unschedule pods 
and resolve the issue.

- If you don't have node scheduler then kubernetes scheduler will take its own decision by using its scheduling algorithm.




----------------------------------------------------------------------------------------------------------------------

**Node Affinity** what is the difference between node affinity and node selector - with node selector you are forcing the scheduler to schedule the pod only if you find the right node matching with label also called as hard match.

- Whereas node affinity is the feature it has two options --
1. Preferred - we are telling the scheluer to first try to find the exact label match node and just use that node otherwise if you don't find i am okay schedule on any other node, there is flexibility.

2. Required - it works similar to the node selector if fully matched only then schedule otherwise keep unschedule. 


```

spec:
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:    #required example just add the word required
            nodeSelectorTerms:
              - matchExpressions:
                  - key: node-name
                    operator: In
                    values:
                      - arm-worker




spec:
      affinity:
        nodeAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:    #preferred example just add the work preferred
            nodeSelectorTerms:
              - matchExpressions:
                  - key: node-name
                    operator: In
                    values:
                      - arm-worker


```

**Difference** although the features are little similar node affinity grants more granular level of configuration or flexibility for the devops engineers which says the Kube Scheduler you can got with the preferred configuration and if you don't find the preferred configuration, you can schedule it anywhere so, this is about the node selector and node affinity.



------------------------------------------------------------------------------------------------------


**Taint** let's say you have a kubernetes node and you don't want anything to be scheduled on this node, that is completely unschedulable...
eg. upgrades 
- Support we have a production cluster and we have 3 worker nodes and want to upgrade them but we can not upgrade all of them at the the one time so what we will do we drain the node means move all the running pods from node to different node and once all the pods are evicted, moved to other nodes then you make the node unschedulable and once this node is unschedulable, node is idle and scheduler is not going to schedule any pod on this node.

So, you can bring this node down, upgrade this and later you can remove the unschedulable status so the new version is up and down.Same we are achieving using the taint.

**What is Taint** is the label or particular stamp that you are applying to a particular node which explains the Kube Scheduler my node has to be unschedulable.

**Three differenct types of Taints:** 
1. No Schedule: Where your node will go to complete no schedule status.
2. No Exuecute: its little bit dangerous because when you are doing no execute all the pods that are on particular node will immediately stop working.
3. Preferred No Schedule: eg. you have a node and the performance of the node is declining, node is going through some CPU or memory issues. So, we are telling the scheduler in worst cases schedule otherwise not try to schedule on this node.


**Practical**

```

manoj@Ubuntu:~/kubernetes_practice$ kubectl get nodes
NAME                 STATUS   ROLES           AGE     VERSION
kind-control-plane   Ready    control-plane   3h40m   v1.30.0
kind-worker          Ready    <none>          3h40m   v1.30.0
kind-worker2         Ready    <none>          3h40m   v1.30.0
kind-worker3         Ready    <none>          3h40m   v1.30.0

manoj@Ubuntu:~/kubernetes_practice$ kubectl taint nodes kind-worker key1=value1:NoSchedule
node/kind-worker tainted


```
**Important Points** usually we don't schedule pods on control-plane or master node and if we run below command
```
kubectl edit nodes control-plane 


spec:
  podCIDR: 10.244.0.0/24
  podCIDRs:
  - 10.244.0.0/24
  providerID: kind://docker/kind/kind-control-plane
  taints:
  - effect: NoSchedule
    key: node-role.kubernetes.io/control-plane
status:
  addresses:
  - address: 172.18.0.5

````
-- There is already added **NoSchedule**


----------------------------------------------------------------------------------------------

****
**Conditions1**
****

-if we taint two nodes from three above nodes then pods will be auto schedule on last available node only.
```
kubectl taint nodes kind-worker2 key1=value1:NoSchedule
kubectl apply -f deploy.yml
```


**Tolerations** is basically an exception that is given to certain pods for example in our case we have 3 nodes we have tainted the 3 nodes as no schedule but for some reasons you still want some high priority that must run so what we can do, we can add a tolerations or an exception with which they can still run on the No Schedule or any tainted nodes.


**How to set Tolerations** When we were tainting the node we used key and value pair, No Schedule is an effect on the node but if you add the tolerations to pod which are matching these key value pair with taint.


- We are simply taiting our last pending node

```
kubectl taint nodes kind-worker3 key1=value1:NoSchedule
``  

**How to apply tolerations on pods**


```
manoj@Ubuntu:~/kubernetes_practice$ cat deploy.yml 
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
      tolerations:
        - key: "key1"
          operator: "Equal"
          value: "value1" 
          effect: "NoSchedule"  
```


```
kubectl apply -f deploy.yml
kubectl get pods -w
```

- Finaly we got our pod scheduled on nodes even after taiting as NoSchedule with the help of Tolerations.
