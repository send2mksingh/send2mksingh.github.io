---
 layout: post
 title: Ansible Modules
---
 - 
   Ansible Modules are predefined functions used to perform tasks on client nodes.
   Modules are discrete units of code which can be used from the command line or in a playbook task.
   It comes with several modules called as modules library.

   Users can also write their modules. These modules can control like services, system resources, files, or packages, etc. and handle executing system commands.

---

 - see how to execute three different modules from the command line.
     $ ansible webservers -m service -a "name=httpd state=started"  
     $ ansible webservers -m ping  
     $ ansible webservers -m command -a "/sbin/reboot -t now" 