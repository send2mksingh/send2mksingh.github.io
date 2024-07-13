---
 layout: post
 title: Docker Port Expose
---


**How Port Mapping Works**

Imagine you have a web server running inside a Docker container on port 3000. By default, this port is only accessible 
within the Docker network and not from your host machine or the external network.

To make this server accessible outside the container, you need to forward a port from the host to the container.

Example:

- docker run -it --name container-name -p [HOST_PORT]:[CONTAINER_PORT] [IMAGE]
Here, -p is the flag used to specify port mapping.





**Accessing the Containerized Application**
After setting up port forwarding, any request sent to port 3000 on the host machine is automatically forwarded to
port 3000 in the container.

- Now, the server running inside the container is accessible via http://localhost:3000 or http://[HOST_IP]:3000.



**Best Practices for Port Forwarding**

Choose Non-Standard Host Ports: Avoid using common ports on the host to reduce security risks and conflicts.
Consistency in Development and Production: Keep port mappings consistent across development and production environments 
for simplicity.
Document Port Mappings: Maintain clear documentation of which host ports map to which container ports.


---
 **Commands to map ip of host and container-**

---

 - docker run -td --name container-name -p 80:80 ubuntu

 - docker ps

 - docker port containername

 - docker exec  -it containername /bin/bash

 - apt-get update -y

 - apt-get install apache2  -y

 - cd /var/www/html

 - echo "Hello World " > index.html

 - service apache2 restart

---
 **Example-2**

---

 - docker run -td --name myjenkins  -p 8080:8080 jenkins
  
What is the difference b/w docker exec and docker attach?
=> Docker exec creates a new process in the containers environment while the docker attach just connect the standard 
input/output of the main process inside the container corresponding  standard input/outpur error of current terminal.

Docker exec >> is specifically for running new things in a already started container, be it a shell or some other process.

What is the difference b/w expose and publish a docker?

Basically you have three options:-
1) Neither specify expose nor -p 
2) Only specify expose
3) specify exporse and -p

4. if you specify nothing then container will be accessible from inside the container only.
5. if you expose a port then it can be accessed globally.
6. if you specify -p then container can be accessed by other containers created on the same host.

