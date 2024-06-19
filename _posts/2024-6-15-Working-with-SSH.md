---
layout: post
title: How SSH works
---

**What is SSH?**
Secure Shell one of the Network protocol used to communicate and share data among the network linux based machines.
The only prequisite there should be network connectivity between devices means they should ping by IP at least.

**Packages and services required**
Package - openssh-server
daemon - sshd
port - 22
config file - /etc/ssh/sshd_config

**Usage syntax**

ssh user@server_ip_address


Here I am giving one scenario through which we are going to understand the process and how it works--
**Machine-1**

- Do ssh to the server
- ssh manoj@192.168.152.140
- here it is going to ask for password first time just enter

Then at first login this will create .ssh/ hidden directory in local machine, this will contain one file name known_hosts 
- known_hosts - this file contains all the servers detail on which you have done ssh


**Password less or Key Based Authentication**
- Generate the key
- ssh-keygen      - this commmand will generate the key file that will be shared or imported on server machine 
- Above command is going to create two other files in .ssh/ directory 1. id_rsa, 2. id_rsa.pub
- Id_rsa - Contains private key
- Id_rsa.pub - Contains public key

- ssh-copy-id -i /root/.ssh/id_rsa.pub   manoj@192.168.152.140

here -i for import, we are simply sending the public key to the server machine so that next time i will not ask for password.
It will verify the login details with key only.

**Machine-2**
When we share ssh key then server side .ssh/ hidden directory is created and it contains one file authozired_hosts.
-Authorized_hosts - contains the details about the server which has made it password less or key based login.



**@WARNING: Remote host identification changed**
Someone could be eavesdropping on your right now (man in the middle attack)

Because of server side other machine is available of same IP and same name that is not matching from the fingerprint key.

- We can resolve this problem by using mac add of server.
- We can contact to server side regarding this type of error.


