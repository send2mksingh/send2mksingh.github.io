---
 layout: post
 title: Service In Kubernetes
---


**Without the Service in kubernetes**
What happens basically suppose if you have deployed deployment and we have get the auto healing and auto scaling feature.

There is case when we have set replica set count as 3, with pods ip like : 172.16.1.2, 172.16.1.3 and 172.16.1.4 all are working fine and accessible from team side.
But all of sudden one or any pod (172.16.1.2) gets killed then because of auto healing relica set controller auto recreates the deleted pod again, the problem is now the pod is running the same application but the ip address (172.16.1.10) has changed so when the users or team will try to access the pod using previous pod ip (172.16.1.2) it will not be accessible or show not reachable.

So, what we are doing, we are telling the users instead of using the pod ip, use service (svc), we create service on top of the deployment.
We can say this is the deployment that creates 3 pods using the replica set on top of this we create something called as service.
What does service do, it acts as Load Balancer for this it uses components in kubernetes called as kube proxy.

So, we are telling the user to access applications using the service's ip or load balancer's ip instead of pod ip, so please try to access these applications on the same ip address underlying what this service using kube proxy will do is it will forward the request let's say send 10 requests here  172.16.1.2, send 10 requests here  172.16.1.3 and send 10 request here 172.16.1.4.


**Service Advantages**

1. Load Balancer

2. Service Discovery  : This is the mechanism and for this it uses labels and selectors.

3. Expose to World : service can expose application to outside.

**Service can be three types**
1. Cluster IP : Application will be accessed only inside the kubernetes cluster, nothing will change in this type - we get two benefits that are Discovery and Load Balancing. Only if you can login to kubernetes cluster and if you have access to the network inside the kubernetes cluster, that is you have access to the container network or you have access to flannel, calico, whatever you have configured only they can access.

2. NodePort : When we create service NodePort type, it allows your application to be accessed inside your organization, so anybody within your network, can access the application using Worker node ip address.

3. Load Balancer : In this type your service will expose your application to external world


**Service Discovery:**There is another case where service is taking request from users and sending to pods but what happens same pod deleted again ip will change, so service can face the same problem, using the service accessing the pods would failed, this is the another problem service solve that is called as Discovery. What service says, if i am keeping track of deployments let's say this service and keeping track of a deployment which is creating three pods for example, and if one of these ip address changed, if service also follows the same problem of keeping track of ip address the problem is not solved at all.

So, what service is doing it will follow Service Discovery by using labels and selectors, unlike following ip address that can change at any time, eg. every pod that is getting created will be applied label and these labels will be common for all pods related to same type of applications.

Next time when the pods get down and created again with new ip so service will watch only label that will remain the same and why will label remain the same because replica set controller what it will do it will deploy the pod with the same yaml that it got that is auto healing.

So, if service is keeping track of pod using labels instead of ip address and the label is always same the problem is solved.
So, this is the service Discovery mechanism of Kubernetes service.


----------------------------------------------------------------
Whenever you create your deployment you provide all the required specification along with that inside your metadata, metadata of your deployment you create something called as label, label is just a tag, you can just say app payment for example.

Now what will this deployment will do, create replica set and what this replica set suppose it counts set 2 so, it will create two pods, pod1 and pod2 both the pods will have same label
==> pod1
label:
app: payment

==> pod2
label:
app: payment

**Scenario** now try to understand if one pod gets killed, replica set will create again pod with new ip address but the label and selectors will be same because its creating from the existing yaml file.



------------------------------------------------------------------

The YAML configuration you provided is for deploying an NGINX application using Kubernetes. This configuration creates a Deployment resource, which manages a set of replica Pods running NGINX. Here's a breakdown of the configuration:



```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: sample-app
spec:
  replicas: 5
  selector:
    matchLabels:
      app: sample-app
  template:
    metadata:
      labels:
        app: sample-app
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
      - containerPort: 80
```


-------------------------------------------------------------------------


```
command : kubectl get pods -v=7  #to see verbose, working progress of deployment.

command : minikube ssh  # login to kubernetes cluster
command : curl Pod_IP
or
command : kubectl exec -it Pod_name  -- /bin/bash
command : curl Pod_IP
```


-------------------------------------------------------------------------


`minikube ssh` and `kubectl exec -it podname -- bash` are both commands used in the context of Kubernetes, but they serve different purposes and target different parts of the Kubernetes ecosystem.

### 1. `minikube ssh`

- **Purpose**: `minikube ssh` is used to SSH into the virtual machine (VM) running the Minikube cluster.
- **Scope**: This command gives you access to the underlying VM, not to any specific Kubernetes pods or containers. You can use this to manage the VM itself, inspect the environment, check logs, install software, etc.
- **Typical Use Case**: Useful for debugging or configuring the Minikube VM, examining system logs, or troubleshooting issues at the VM level.



```sh
minikube ssh
```

### 2. `kubectl exec -it podname -- bash`

- **Purpose**: `kubectl exec -it podname -- bash` is used to execute a command inside a specific container running in a Kubernetes pod.
- **Scope**: This command gives you access to the shell of a container inside a pod. You can interact with the application running inside the container, inspect its environment, view application logs, or troubleshoot issues at the application level.
- **Typical Use Case**: Useful for debugging applications, running commands inside a container, inspecting the container's filesystem, or performing operations specific to the application running in the pod.

```sh
kubectl exec -it podname -- bash
```

### Summary

- **`minikube ssh`**: Accesses the Minikube VM.
- **`kubectl exec -it podname -- bash`**: Accesses a container inside a Kubernetes pod.

These commands are used at different layers of the Kubernetes stack, with `minikube ssh` focusing on the VM level and `kubectl exec` focusing on the container level.



------------------------------------------------------------------------------

**Important points**
- By default when we curl pod ip we get response within the kubernetes cluster only this is because a pod by default will have only the cluster ip addresses, it is attached to the cluster network. So, if it is the cluster network you have to access it using the cluster itself, you have to login to cluster and access it.




**NodePort Practical**: what happens in NodePort your application will be exposed on the Node IP address.
Just simply create the service yaml file and in selectors mention the pod template labels from deployment yaml file, because at the end service will just care about the label and selectors of particular pod.


eg.

Here is the YAML configuration for the Kubernetes service:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service  # mention the service name
spec:
  type: NodePort   #this is the type NodePort
  selector:
    app.kubernetes.io/name: MyApp  #this is the selector, matching from the pod template from deployment yml file
  ports:
    - port: 80
      targetPort: 80       #this is the port where the application is running
      nodePort: 30007   #this is node port where the service is exposed
```



### Explanation

1. **apiVersion: v1**
   - Specifies the API version of the Kubernetes object. For Services, the API version is `v1`.

2. **kind: Service**
   - Indicates that the object being created is a Kubernetes Service.

3. **metadata:**
   - **name: my-service**
     - Provides the name of the Service. This name must be unique within the namespace.

4. **spec:**
   - **type: NodePort**
     - Specifies the type of Service. `NodePort` exposes the Service on each Node's IP at a static port (NodePort). A `NodePort` Service makes the pods accessible from outside the Kubernetes cluster.

   - **selector:**
     - **app.kubernetes.io/name: MyApp**
       - Defines a label selector. The Service will route traffic to the Pods that match this label.

   - **ports:**
     - A list of ports that the Service should expose.
     - **- port: 80**
     - The port that the Service will listen on. This is the port that clients will connect to.
                                                                                          - **targetPort: 80**
     - The port on the Pod that the traffic should be forwarded to. By default, it is set to the same value as the `port` field.
     - **nodePort: 30007**
     - A specific port on the Node where the Service is exposed. If not specified, Kubernetes will allocate a port from the default range (30000-32767). Here, it is explicitly set to `30007`.

### Summary

This YAML configuration creates a Kubernetes Service named `my-service` of type `NodePort`. The Service listens on port 80 and routes traffic to Pods that have the label `app.kubernetes.io/name: MyApp` on their port 80. The Service is accessible externally on port `30007` of any Node in the cluster.




**How it works:**When you are creating service using any mode whether it is NodePort mode or Load Balancer, cluster ip will be definitely there. additionally when you are creating service in NodePort mode you will get a port mapping and that port mapping is nothing but what kubernetes service has done for you, it says if you don't want to access the using the cluster the ip, you can use the Node IP address and i have mapped the port suppose 80 with the port 3007 that you have provided in the service.yml file.


```
**Commands:**
minikube ip  #to check the ip of minikube node
curl -L http://minikube IP

###same you can search from web browser.

```


```
kubectl edit svc service_name   #edit service details

```

**Service Discovery:**Do one practical just change the selectors in service resource and check if service discovery is able to detect the pods or not, it should not because now the labels and selectors are different, by working on this you can understand how service is using service discovery concept using the labels and selectors.


---------------------------------------------------------------------------------------

**Load Balancing:**We can use Kubeshark to see the work flow of traffic within kubernetes cluster...


- Simply download the Kubeshark from it's official website from Google "search on google Kubeshark Documentation "

```
===> sh <(curl -Ls https://kubeshark.co/install)  #to install the package
===> kubeshark tap   #to capture traffic

http://localhost:8899  or http://127.0.0.1:8899  #to access directly from the browser

```
                                                                                                                



                                                                                                                                             

