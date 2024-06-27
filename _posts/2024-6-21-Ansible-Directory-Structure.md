---
layout: post
title: Ansible Basics
---

**Ansible Directory Structure**
Default directory is /etc/ansible, it contains below files-
- ansible.cfg
- hosts (inventory file)
- roles

**/etc/ansible/ansible.cfg**is the configuration file for ansible we can do setting in the file that used by ansible while running playbooks or ad-hoc commands.
- define path and name of inventory file
- update host_key_checking value as false or true
- set forks values and more.

**/etc/ansible/hosts**is the inventory file we can define servers, hostname(FQDN)name, group and group of groups on which we want to apply playbook.

**/etc/ansible/roles**this directory use to write playbooks or yaml files it provides separate and inbuild files and directory that works as repository from there we can use playbook again and again.

