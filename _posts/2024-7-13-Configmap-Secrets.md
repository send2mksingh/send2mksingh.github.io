---
 layout: post
 title: Configmap And Secrets
---


**What is Cofigmap and Secrets:**What happens in general scenario suppose you are an app developer and let's say there is an backend application and this backend application is talking to the database and it retrives data from database and give back to users, now what are information that is application required from database like: what is the database port, database username and database password. And how this information is retrived using the Env variable and you know the hard core and thumb rule, application should not have these info as hardcoded and what happens if these details are hard coded, and details changed in future in that case user will not get desired result or output, like username or password changed.

So, first we will not hard code these information into application and general practice is to save this as part of Env variable or save in a specific file and retrive this info using OS Modules.

**How we work in Kubernetes**- Because Kubernetes basically deals with containers, so we can create the Config map inside kubernetes cluster and put the information related to DB port or DB connection type inside the config map and you can mount the config map or use the details inside your kubernetes pods. So, the information can stored inside your pod as Env variable or as a file inside your pod on your container file system but this information has to be retrived from the config map because as a user you can not login to pod or go to container this is not the right practice.

**Config map**- config map is solving the problem of storing the information that can be used by your application later point of time. So, config map is used to store data and this data can be used in future by your application, pod and deployments. Basically we are storing normal data or non-sensitive data.

**Secrets**whenever we are creating resource in Kubernetes all information get saved in etcd and data is saved as objects so, if any outsiders want to access and enter, and want to get details from etcd they can get, it means we are compromising all applications related details, to solve this problem, what kubernetes says, if you have normal data save in Config map and if you have non-sensitive data save in secrets, it will encrypt the data at the rest, before the data is saved in etcd, kubernetes will encrypt this oneby default kubernetes uses default encryption mechanism but it also you to use your own custom encryption mechanism, so you can pass this value to the API server, it is feeding information to etcd, hackers can get the details of configmap by running the commandslike: kubectl edit configmap, kubectl describe configmap.


**Least privilege**kubernetes says whenever you are creating secrets use strong RBACK, there is popular concept least privilege where you grant least access, in the user RBACK you can just say user should have the access to all resource except secrets.


------------------------------------------------------------------------------------------------

**Create configmap.yml file**
```

apiVersion: v1
kind: ConfigMap
metadata: 
 name: test-cm
data:
 db-port: "3306"

```

**Run below commands**
```
kubectl apply -f configmap.yml
kubectl get cm
kubectl describe cm test-cm
kubectl exec -it pod_name -- bash
env | grep db    #searching for the db env
```


- **Then modify the deployment yml file**
- deployment.yml 

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: sample-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: sample-app
  template:
    metadata:
      labels:
        app: sample-app
    spec:
      containers:
      - name: my-container
        image: nginx:latest
        env:
         - name: DB-PORT
           valueFrom:
            configMapKeyRef:
             name: test-cm
             key: db-port  
        ports:
        - containerPort: 80


```


```
kubectl apply -f deployment.yml
kubectl get pods
kubectl exec -it pod_name -- bash
env | grep DB

```



**Consider the Issue**
- go to the configmap.yml file and change the value of port from 3306 to 3307

```
apiVersion: v1
kind: ConfigMap
metadata:
 name: test-cm
data:
 db-port: "3307"

```

kubectl exec -it pod_name -- bash
env | grep DB

- it will display the old value that is 3306.
DB-PORT=3306



- So our application is continuosly using the same data and it will fail because the port has changed. 
Application is trying to connect to DB but it will fail.

- So what kubernetes said if you have this type of information that keeps changing, in that case changing env variable inside the kubernetes or container is not possible.

**VolumeMounts:** Instead of using the evn variable, you can use the file, your configmap information will be saved inside a file and developers can read the file.

- To do a Volume Mount you have to create the volume first 

- do changes in deployment.yml file as per Volume Mounts

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: sample-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: sample-app
  template:
    metadata:
      labels:
        app: sample-app
    spec:
      containers:
      - name: my-container
        image: nginx:latest
        volumeMounts:
         - name: db-connection
           mountPath: /opt
        ports:
        - containerPort: 80
      volumes:
        - name: db-connection
          configMap:
            name: test-cm


```

```
kubectl get pods
kubectl exec -it pod_name -- bash
evn| grep DB
cat /opt/dp-port

```



- go to the configmap.yml file and change the value of port from 3306 to 3307

```
apiVersion: v1
kind: ConfigMap
metadata:
 name: test-cm
data:
 db-port: "3307"

```



```
kubectl apply -f configmap.yml 
kubectl describe cm test-cm
kubectl exec -it nginx-deployment-5f6b7b77c9-4jcb2 -- bash
cat /opt/db-port

```

**Working with Secrets using commands**

```

manoj@Ubuntu:~/kubernetes_practice$ kubectl create secret generic testing --from-literal=name="manoj"
secret/testing created

manoj@Ubuntu:~/kubernetes_practice$ kubectl get secrets
NAME                              TYPE                 DATA   AGE
kubeshark-saml-x509-crt-secret    Opaque               1      2d11h
kubeshark-saml-x509-key-secret    Opaque               1      2d11h
kubeshark-secret                  Opaque               2      2d11h
sh.helm.release.v1.kubeshark.v1   helm.sh/release.v1   1      2d11h
test-secret                       Opaque               1      84s
testing                           Opaque               1      12s


manoj@Ubuntu:~/kubernetes_practice$ kubectl describe secrets testing
Name:         testing
Namespace:    default
Labels:       <none>
Annotations:  <none>

Type:  Opaque

Data
====
name:  5 bytes

```


```

kubectl edit secret mysecret

echo bXlwYXNzd29yZA== | base64 --decode

it will simple display the encoded data

```


In Kubernetes, Base64 encoding is commonly used to encode and decode data, particularly for the following purposes:

1. **Secrets Management:**
   - Kubernetes Secrets are used to store and manage sensitive information such as passwords, OAuth tokens, and SSH keys. When creating a Secret, the values of the Secret data are typically Base64 encoded.
   - For example, if you have a password `mypassword`, it needs to be encoded in Base64 before being included in the Secret YAML file.
     ```sh
     echo -n 'mypassword' | base64
     ```
     This command will output:
     ```
     bXlwYXNzd29yZA==
     ```
     You can then use this encoded string in your Secret definition:
     ```yaml
     apiVersion: v1
     kind: Secret
     metadata:
       name: mysecret
     type: Opaque
     data:
       password: bXlwYXNzd29yZA==
     ```

2. **Configuration Management:**
   - ConfigMaps can also use Base64 encoding, although it is less common since ConfigMaps are generally used for non-sensitive configuration data.

### Why Base64?

Base64 encoding is used because it converts binary data into an ASCII string format. This ensures that the data can be safely transmitted over text-based protocols and included in YAML or JSON configurations without risk of data corruption. Base64 uses only alphanumeric characters and a few symbols, making it safe for use in text files.

### Decoding Base64

To decode a Base64 encoded string, you can use the following command:
```sh
echo 'bXlwYXNzd29yZA==' | base64 --decode
```
This will output:
```
mypassword
```

### Example: Creating and Using a Secret

1. **Create a Secret:**
   ```sh
   echo -n 'mypassword' | base64
   ```
   Output:
   ```
   bXlwYXNzd29yZA==
   ```
   Define the Secret:
   ```yaml
   apiVersion: v1
   kind: Secret
   metadata:
     name: mysecret
   type: Opaque
   data:
     password: bXlwYXNzd29yZA==
   ```
   Apply the Secret:
   ```sh
   kubectl apply -f mysecret.yaml
   ```

2. **Use the Secret in a Pod:**
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: mypod
   spec:
     containers:
     - name: mycontainer
       image: nginx
       env:
       - name: PASSWORD
         valueFrom:
           secretKeyRef:
             name: mysecret
             key: password
   ```

By using Base64 encoding, Kubernetes ensures that sensitive data can be securely managed and easily integrated into your configurations.
