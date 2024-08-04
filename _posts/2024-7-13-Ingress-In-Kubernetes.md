---
 layout: post
 title: Ingress In Kubernetes
---


**What is Ingress in Kubernetes?**- before the ingress, when Kubernetes launch it's first version in 2015, it did not have ingress, Business were using legacy system, like there was VM and on top of that running applications and to manage using Load Balancer like Nginx and F5, but that was enterprise level and providing **ratio based load balacing** eg. 3 requests to VM-1, 5 requests to VM-2, **sticky session:**if any specific users request is going to VM-1 then all it's request will go to VM-1 only.
Some more eg. like: Path based
- Domain based
- White listing
- Black listing



**Problems-1:**Enterprise level load balancing, security and good Load Balancing, When businesses are migrating from legacy to kubernetes they faced some issues, like they were using deployment and on top that service, from that getting all the features and facility like Auto healing and Auto scaling but the issue is service is providing the load balancing mechanism that is simple Round Robin load balancing what is Round Robin, if you doing 10 requests what this spcific service using Kube Proxy is updating the IP Table rules, what it will do, it will send 5 requests to Pod-1 and 5 requests to Pod-2 but this is very simple kind of load balancing, because people are coming from VM and they were getting more benefits from there.

**Problem-2:**To expose the applications to external kubernetes offers service with Load Balancer mode, what if you have 100 services in that case the cloud providers are charging for each Static Public IP. So, secondly it is costly.


**Kubernetes** to overcome all above issues they introduced Ingress, where the users are allowed to create a resource called ingress and the logics or say Ingress Controller will be created by the load balancing company like: **Nginx, F5, Traffic and HA Proxy**, you will only have to deploy Ingress Controller using Helm Chart or using the Yaml manifest. So, as the user you have to create ingress resource as well as you have to deploy ingress controller of required type or say load balancer type. After that it can be one service or many service they will only write the Ingress resource once they write the ingress resource, Ingress does not have to be one to one mapping, you can create one ingress and you can handle hundreds of services as well using path like you can say if Path is A go to service one, Path is B go to service two

**Explaining:**you have one Kubernetes cluster and you are creating a pod so, you are writing a yaml manifest for this and you created the pod.
There is the Component called **Kubelet**this will deploy your pod on one of the worker node, kubelet is sitting on the worker node and Api-Server will notify kubelet using scheduler that a pod is created and kubelet will deploy the pod. 


Or Let's say you are creating service manifest so there is the Kube Proxy, it will udpate IP Table rules, so for resource you are creating in Kubernetes there is the component that is watching for that resource and it is performing the required action. 


  

```

What is Ingress?
Ingress exposes HTTP and HTTPS routes from outside the cluster to services within the cluster. 
Traffic routing is controlled by rules defined on the Ingress resource.

```


**Image source Kubernetes official website: https://kubernetes.io/docs/concepts/services-networking/ingress/** used for learning purpose only.

![Example image](https://kubernetes.io/docs/images/ingress.svg)



**Deploy ingress resource:**

```

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-example
spec:
  rules:
  - host: "example.com"
    http:
      paths:
      - pathType: Prefix
        path: "/learning"
        backend:
          service:
            name: my-service
            port:
              number: 80

```



This YAML configuration defines an Ingress resource for a Kubernetes cluster. Ingress resources manage external access to services within the cluster, typically HTTP and HTTPS routes. Let's break down each part of this configuration:

### 1. **apiVersion**
```yaml
apiVersion: networking.k8s.io/v1
```
- This specifies the version of the Kubernetes API that you are using for the Ingress resource. In this case, it's `networking.k8s.io/v1`.

### 2. **kind**
```yaml
kind: Ingress
```
- This indicates that the kind of Kubernetes resource being defined is an `Ingress`.

### 3. **metadata**
```yaml
metadata:
  name: ingress-example
```
- Metadata provides information about the Ingress resource. Here, the Ingress resource is named `ingress-example`.

### 4. **spec**
```yaml
spec:
  rules:
  - host: "example.com"
    http:
      paths:
      - pathType: Prefix
        path: "/learning"
        backend:
          service:
            name: my-service
            port:
              number: 80
```
- The `spec` field contains the specification of the Ingress resource, detailing how it should behave.

#### **4.1. rules**
```yaml
  rules:
  - host: "example.com"
```
- `rules` define how the traffic should be routed. Each rule applies to a specific host. Here, the rule is for traffic that matches the host `example.com`.

#### **4.2. http**
```yaml
    http:
      paths:
      - pathType: Prefix
        path: "/learning"
        backend:
          service:
            name: my-service
            port:
              number: 80
```
- The `http` section defines HTTP rules. It contains an array of paths that specify how different URL paths should be routed.

##### **4.2.1. paths**
- Each path rule has several components:

###### **pathType**
```yaml
        pathType: Prefix
```
- `pathType` defines how the path matching should be done. The `Prefix` path type means that the path specified should be a prefix of the request's path. For example, `/learning` will match `/learning`, `/learning/abc`, etc.

###### **path**
```yaml
        path: "/learning"
```
- `path` specifies the URL path that this rule should apply to. Here, it applies to any request starting with `/learning`.

###### **backend**
```yaml
        backend:
          service:
            name: my-service
            port:
              number: 80
```
- `backend` specifies the backend service that the traffic should be routed to if the path matches. 

##### **backend.service.name**
- The `name` field within `service` specifies the name of the service to which the traffic should be sent. In this example, the service is named `my-service`.

##### **backend.service.port.number**
- The `port` field specifies the port number on the backend service where the traffic should be directed. Here, it’s port `80`.

### Summary
This Ingress configuration routes HTTP traffic coming to `example.com` with a path that starts with `/learning` to the backend service named `my-service` on port `80`. It allows external users to access the service by specifying a clear rule for routing traffic based on the host and path.




------------------------------------------------------------------------------------------

**Now Install the Ingress Controller as we are doing host based or domain based load balancing:**


- We are going to install Nginx ingress controller because it's very popular...

```

https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/

=> minikube addons enable ingress    #to install Nginx ingress controller


manoj@Ubuntu:~/kubernetes_practice$ kubectl get pods -A | grep nginx
default         nginx-deployment-779585ff84-c2hmb           1/1     Running     1 (17h ago)   22h
default         nginx-deployment-779585ff84-rqzmj           1/1     Running     1 (17h ago)   22h
ingress-nginx   ingress-nginx-admission-create-6qrt8        0/1     Completed   0             6m18s
ingress-nginx   ingress-nginx-admission-patch-ld4wc         0/1     Completed   1             6m18s
ingress-nginx   ingress-nginx-controller-768f948f8f-n5fz6   1/1     Running     0             6m18s


kubectl get ingress-controller-pod -n ingress-nginx
kubectl get ingress


```


**Do entry in the /etc/hosts file for name resolution**
```
sudo vim /etc/hosts
192.168.49.2  example.com

:wq



curl example.com
or on browser
http://example.com/leaning
```
