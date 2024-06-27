---
layout: post
title: Brief Info about Ansible
---

**What is Ansible**

Ansible is an open source configuration management tool used to automate infrastructure management configuration. 
Using Ansible we can configure hundreds and thousands of servers with just a single command.

**How does Ansible works**

Ansible uses something knownn as playbook written in in yaml syntax where we can define all tasks and targets.
Along with the playbook we also need a hostfile or inventory file where we can update servers name, ip, group and we can also create group of groups.

After having playbook and defining servers in the inventory files user can run ansible commands to executes tasks on the client's nodes with the help of ssh protocal.

**Ansible engine/Controller/Master**
This is the system or server from where we configure all tasks and targets which we want to apply on the client's system.

**Ansible node/client/Manage nodes**
System where we applied playbooks and executes commands to perform desired tasks.

**Why Ansible**
- It is a free and open source congiguration tool and easy to use.
- Using openssh-server package to communicate with client machines.
- Agentless no need to install any other software on the client side.
- Well known python/yaml syntax using.
- Large no. of modules are available to use and work.

**Steps to configure Ansible**
- Create at min two servers, one for the Master node and second for the client node.
- Prerequisite - client nodes should have python installed (otherwise we can't use copy and fetch modules for all work we have to use raw modules).
- Network connection between the master and client nodes.
- Ansible master uses ssh connection to connect and work with client node.
- Check openssh-server package and configure if it is not installed.

- SSH password authentication steps follow -
- ssh user@server-ip 
- it will then ask for client server password same proceed. 

- SSH password less or key based authentication steps follow-
- ssh-keygen    # it will create .ssh directory in user's home directory.
- ssh-copy-id -i  /root/.ssh/id_rsa.pub  user@server-ip   # this import the public from .ssh directory to the client's machine.

- ssh user@server-ip   # now this will not ask for password

