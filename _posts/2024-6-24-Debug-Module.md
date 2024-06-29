---
 layout: post
 title: Debug Modules
---
  
  Ansible provides a debug module option that makes the tasks more manageable. It is a handy tool to figure out any problem areas.
  
  This module prints statements during execution and can be useful for debugging variables or expressions.

   - This accepts 3 parameters :
     1. msg   # If you want to print any msg then use debug module with msg parameter.
     2. var   # Create variable and prints the values. 
     3. verbosity  # Shows the execution progress.

   ---
     Debug module with msg parameter with example:
     
   ---

   ---
    - name: ansible debug module with msg parameter
      hosts: all
      tasks:
      - name: Printing simple statement
        debug:
           msg: "hello world this is Manoj Kumar"


    --- 
     When running the playbook you will get below output:
    
    ---
      [root@master playbook]# ansible-playbook msg_module.sh 

       PLAY [ansible debug module with msg parameter] *******************************************************************************

       TASK [Gathering Facts] *******************************************************************************************************
       ok: [192.168.152.135]
       ok: [192.168.152.130]

       TASK [Printing simple statement] *********************************************************************************************
       ok: [192.168.152.135] => {
       "msg": "hello world this is Manoj Kumar"
         }
       ok: [192.168.152.130] => {
      "msg": "hello world this is Manoj Kumar"
         }

       PLAY RECAP *******************************************************************************************************************
       192.168.152.130            : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
       192.168.152.135            : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  

    ---
       Printing variable using var parameters:
     
    --- 
      
    ---
     - name: Ansible debug module in action
       hosts: all
       vars:
          greetings: Hello World!
          site: Linuxtechi
       tasks:
       - name: Print the value of a variable
         debug:
              msg: "{{ greetings }}, Welcome to {{ site }}."