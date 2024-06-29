---
  layout: post
  title: Ansible Facts
 ---

  Ansible facts are nothing but information about managed nodes like - os distribution, release, version, architecture, processor, python, hostname, domain name and ip address and more details.

  The task of collecting this remote system info is called as Gathering facts and collected/gathered information is called facts or variable.

  You cant gather/collect facts using setup module in Ad-hoc commands.

  NOTE:- Ansible playbookds call this setup module by default to perform Gathering facts tasks.

 ---
  - Syntax:

  ---
      $ ansible server-ip -m setup  #This will simply print the facts about the client server.
      $ ansible server-ip -m setup -a "filter=ansible_mounts" 


 **Types of Ansible facts**
   There are two types of facts or variable for managed nodes/client nodes.
   - 1. Default facts
   - 2. Custom facts

   

