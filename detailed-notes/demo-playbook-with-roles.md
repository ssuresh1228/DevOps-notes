# Demo: Creating an Ansible Playbook with Roles
---

## Problem Statement: Create an Apache server on Ubuntu using Roles

### 1. Create a new role
- In `/etc/ansible` there will be a roles directory. Enter it and run
	- `ansible-galaxy init apache --offline -Role apache was created `
	
>[!note] This command will create the following structure automatically:
>![[Pasted image 20230212163855.png]]
> goal is to divide the tasks we need to run into smaller parts by making main.yml point to **other YAML files**; thus, we need to create these files.

### 2. Create install.yml 
- Inside `/etc/ansible/roles/apache/tasks`, create install.yml with the following code:
>[!example] install.yml content:
>```
>#installing apache2
>- name: installing apache2 server
>apt: 
>name: apache2
>state: present

## 3. Files, configure.yml, and handlers/main.yml
- We will setup files and resources in `/etc/ansible/roles/apache/files/` folder
	- Using a standard apache2.conf file, but only adding a comment at the top
	- During the run process, ansible will take and use this apache2.conf file and replace it on the target machine
	- 

