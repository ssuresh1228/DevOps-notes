# Demo: Creating an Ansible Playbook with Roles
---

## Problem Statement: Create an Apache server on Ubuntu using Roles

### 1. Create a new role
- In `/etc/ansible` there will be a [[ansible-roles#Role Directory Structure|roles directory]]. Enter it and run
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

### 3. Files, configure.yml, and handlers/main.yml
- We will setup files and resources in `/etc/ansible/roles/apache/files/` folder
	- Using a standard apache2.conf file, but only adding a comment at the top
	- During the run process, ansible will take and use this apache2.conf file and replace it on the target machine

#### 3a. Create an index.html in `/etc/ansible/roles/apache/files/` folder with the following:
 >[!note] index.html contents
 ![[Pasted image 20230213155336.png]]

#### 3b. Create configure.yml in `/etc/ansible/roles/apache/tasks` with the following:
>[!note] configure.yml contents
>![[Pasted image 20230213155951.png]]
> - Copies the resources saved in the `files` folder to the target server(s). 
> - configure.yml is used to set up the Apache configurations
> 	- uses a `notify` command, which requires a handler to be set up - this is the next step.

#### 3c. Go into `/etc/ansible/roles/apache/handlers/main.yml` and enter the following:
>[!note] Restarting the apache server
>![[Pasted image 20230213161119.png]]

### 4. Create Service.yml
- Create service.yml under `/etc/ansible/roles/apache/tasks` with the following:
>[!note] service.yml contents: starts the apache server
>![[Pasted image 20230213164003.png]]

### 5. Define site.yml
- in `etc/ansible` define the following site.yml
	- ![[Pasted image 20230213164640.png]]

### 6. Verify if all YAML files are formatted correctly
- Use `ansible-playbook site.yml --syntax-check`

### 7. Execute the apache role
- `ansible-playbook -i hosts site.yml`