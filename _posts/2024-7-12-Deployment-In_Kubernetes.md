---
 layout: post
 title: Deployment In Kubernetes
---
  
  We can create container using any container platform eg. docker to run this container

eg. docker run -it -d --name container_name image_name.



**Kubernetes**
In kubernetes we create yml file and mention required all things to run pod so pod is running specifications by giving parameters.
So only difference is pod can be single container or multiple containers.
Why do we create multiple container suppose you have an application that is depended on other apps without which it can not run. eg service mesh we have a sidecar container that contians all the necessary data and support actual container.

So, if we use the pod both can share the same network and communicate using localhost and also share the same storage or volume.


**Deployment**
Why we move from docker container to kubernetes, it offers something called Autohealing and Autoscaling but the pod does not have the capability of these services, because pod is equivalent to container, pod is doing nothing just providing the yaml specification of running your container, in some cases it can run multiple containers and some advantages that can share the network and storage. Autohealing and Autoscaling are provided by deployment, if we want to provide zero down time and autoscaling and autohealing then deploy the deployment what happens when we do deployment, it further create an intermediate resource called replica set which is kubernetes controller and replica set creates pod.

In our deployment yaml manifest you can just say replica count as two.

Autohealing - support we have update replica set as two so it will ensure two pods will always running and if any one failed or deleted replica set will again create the pods sothat it will match the replica count.



eg : Deployment ====> RS ====> Pod

**What is the controller?** this will ensure desired state should match the actual cluster state.

Question1. what is the difference between Container, Pod and Deployment?

Question2. What is the difference between Deployment and Replica Set?

Ans. Replica set is the kubernetes controller that is the one that is implementing autohealing feature of your pods if a pod is getting killed or if a deployment says that increase the pod by one so who is doing this replica set controller so replica set controller is the one is actually implementing the autohealing capability by saying that the actual state of deployment should be on the cluster.

So, when we create a deployment a replica set is created automatically which is responsible for tracking this control controller behavior in kubernetes.


--------------------------------------------------------

command : kubectl get all # by running this we get everything like pods, service, deployments in particular namespace.

command : kubectl get all -A # resources available in all namespace.

command : minikube ssh # to access pods, login to K8 cluster.
Command : ssh -i <identity_file> server_IP  #to login to remote K8 Cluster.
command : kubectl get pods -w  # watch live activity happening

The YAML configuration you provided is for deploying an NGINX application using Kubernetes. This configuration creates a Deployment resource, which manages a set of replica Pods running NGINX. Here's a breakdown of the configuration:



```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 5
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
        image: nginx:1.14.2
```


### Explanation:

- **apiVersion: apps/v1**: Specifies the API version of the resource.
- **kind: Deployment**: Indicates that the resource being created is a Deployment.
- **metadata**: Provides metadata about the resource.
  - **name**: The name of the Deployment.
  - **labels**: Key-value pairs for organizing and selecting resources.
    - **app: nginx**: A label with the key `app` and the value `nginx`.
- **spec**: Defines the desired state of the Deployment.
  - **replicas: 5**: Specifies the number of Pod replicas to run.
  - **selector**: Defines how to identify the Pods managed by this Deployment.
    - **matchLabels**: A selector to match the Pods with the given labels.
      - **app: nginx**: The label used to select the Pods.
  - **template**: Describes the Pods to be created.
    - **metadata**: Metadata for the Pods.
      - **labels**: Labels for the Pods.
        - **app: nginx**: The Pods will have this label.
    - **spec**: The specification for the Pod's containers.
      - **containers**: A list of containers within the Pod.
        - **name: nginx**: The name of the container.
        - **image: nginx:1.14.2**: The Docker image to use for the container.
        - **ports**: A list of ports to expose from the container.
          - **containerPort: 80**: The port number to expose.


### Usage:

1. **Save the YAML Configuration**: Save the above configuration into a file, for example, `nginx-deployment.yaml`.

2. **Apply the Configuration**:
   - Use the `kubectl` command to apply the configuration to your Kubernetes cluster:
     ```sh
     kubectl apply -f nginx-deployment.yaml
     ```

5. **Verify the Deployment**:
   - Check the status of the Deployment:
     ```sh
     kubectl get deployments #check deployments
     kubectl get rs      #check replica set
     ```
   - Check the status of the Pods:
     ```sh
     kubectl get pods    #check pods
     ```

