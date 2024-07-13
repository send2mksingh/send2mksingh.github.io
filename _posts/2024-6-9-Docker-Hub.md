---
 layout: post
 title: Docker Hub
---

How to push docker image in docker hub?

- yum install docker.io -y  #install docker
- systemctl start docker  #start docker services
- docker run -it --name containername ubuntu /bin/bash    #create and run container

Now create some files and create image of this Container.

- docker commit Containername  imagename    - to create image

now create account in hub.docker.com


**docker login**
- enter username
- password 

now give tag to your image -

- docker tag image1  dockerid/newimagename

- docker push dockerid/newimage



**Now you can see this image in docker hub account -**

--Now create one instance in tokyo region and pull image from hub.

- docker pull dockerid/newimage
- docker run -it --name mycon dockerid/newimage  /bin/bash


Some Important Commands ---

1. Stop all running Containers : docker stop $(docker ps -a  -q)

2. Delete all stopped Containers : docker rm $(docker ps -a -q)

3. docker rmi -f $(docker images -q)