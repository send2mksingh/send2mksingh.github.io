---
 layout: post
 title: Docker Components and Relateds Terms Definition
---

**1. What is Docker ?**

You have micro services and want to create a package which you want to use it and deploy it on the local 
machine or in the data center and cloud for eg package like os, 
other apps, by using docker we can create docker image. We can use docker run time to run this specific 
image wherever we want to run it. Once we have the docker image 
in running state, that's when we call it Container.

Docker is an open source centralised platform designed to create, deploy and run applications.
Docker uses container on the host os to runs app. It allows apps to use the same linux kernels a system on the
host computer, rather than creating a whole os.

We can install docker on any os built Docker engine runs natively on linux distribution.

Docker runs on Linux distribution.

Docker written in go language.

Docker is a tool that performs os level virtualization, also known as centralization.

Before Docker many users faces the problem that a particular code is running in the developers system but not in
the users system

**Docker was first release in the march 2013 it is developed by**

Kamel Founadi
Solomon Hykes
Sebastien Pahl.

Docker is a set of platform as a service that uses os level virtulization whereas vmware uses hardware level virtualization.



********************************************************
		Advantages:-
********************************************************

No  Pre-allocation of RAM.
CI Efficiency - Docker enables you to build a container image and use that same image across every step of the deployment
process.
Less cost.
It is light in weight.
It can run on physical h/w virtual h/w or on cloud.
you can re-use the image.
it took very less time to create container. 

#When Image runs it is called container and when container stops and pause is called as image.
Running state of image is called as container.


********************************************************
		Disadvantages :-
********************************************************


Docker is not a good solution for app that requires rich GUI.
Difficult to manage large amount of containers.
Docker does not provide cross-platform compatibility means if an app is designed to run in a docker container on windows, 
then it can't run on linux or vice-versa.
Docker is suitable when the development os and testing os are same if the os id different, we should use vm.
No solution for data recovery and backup.



***************************************************************
			Components of Docker:-
***************************************************************
Docker Daemon  - Docker daemon runs on the host os. 
it is responsible for running container to manage docker services.
Docker daemon can communicate with other daemons.

Docker client - Docker users can interact with docker daemon through a client.
Docker client uses commands(CLI) and rest api to communicate with the docker daemon.
when a client runs any server command on the docker client terminal, the client terminal sends these docker commands to 
the docker daemon.
It is possible for docker client to communicate with more than one daemon.

Docker Host - Docker host is used to provide an environment to execute and run app.
It contains the docker daemon, images, containers, networks and storages.

Docker hub/Registry :- Docker registery manages and stores the docker images.
There are two type of registries in the docker.
1. Public Registry - Public registry is also called as docker hub.
2. Private Registry - It is used to share images within the enterprise.


**Docker Images: -**
Docker images are the read only binary templates used to create docker Containers.

                   or

Single file with all dependencies and configuration required to run a program.

                    Ways to create an Image:-

1. Take image from docker hub
2. Create image from docker file.   - We can create docker file and mention all the dependencies and s/w and run from
docker client then docker engine with create image
and from that image we can create Containers.
3. Create image from existing docker Containers.


**Docker Container: -**
Container hold the entire packages that is needed to run the application.
                                or
In other words, we can say that the image is a template and the Container is a copy of that template.
Container is like a Virtual Machine.
Images becomes Container when they run on docker engine.
