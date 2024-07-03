---
 layout: post
 title: Use Of Ansible Vault
---
  
  Ansible vault is useful to encrypt your playbook (including roles and values).

  **Why we need to encrypt playbook?**
    We know that ansible is being used for automation there is a possibility that playbooks contain certain credentials, ssl certifications or other sensitive data and to save such data in simple 
    plain text is the risky task.
    - So we can use ansible vault to simply encrypt our data in secure manner.


 ---
   To encrypt playbook-

 ---
    $ ansible-vault encrypt playbook-name
    $ enter password 

 ---
   To Run Playbook   
  
  ---
     $ ansible-playbook playbook-name --ask-vault-pass  
     # this will prompt for password now

 ---
   To decrypt the playbook file-
  
  ---
     $ ansible-vault decrypt playbook-name
     # this will prompt will password    