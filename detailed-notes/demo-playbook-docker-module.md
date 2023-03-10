Created: 2023-02-14 16:46
# Demo: Ansible Playbook & Docker Module
---
## Install and Manage a Docker Container using Ansible

### 1. Login to EC2 instance

### 2. Create a new directory 'docker_project'
- This is where we will write a new playbook
	- `mkdir docker_project`

### 3. Define the hosts in the `hosts` file
- open the hosts file with some text editor
	- In the `[webserver]` section, 
		- add the public IP addresses of your other nodes
	- Create a `[webserver:vars]` section
		- add `ansible_python_interpreter=usr/bin/python3`
			- ![[Pasted image 20230214173535.png]]

### 4. Create a new playbook 'ubuntu_playbook.yml'
- Has code to install
	- dependencies
	- docker repos
	- docker python module
	- pull official ubuntu image
	- create 4 containers on the newly pulled image
- #### ubuntu-playbook.yml
	```
	---
	- hosts: all
	  become: true
	  vars:
	   create_containers: 4
	   default_container_name: docker
	   default_container_image: ubuntu
	   default_container_command: sleep 1d
	
	tasks:
	 - name: install aptitude via apt
	   apt: name=aptitude state=latest update_cache=yes force_apt_get=yes
	 
	 - name: add docker repository
	   apt_repository:
	    repo: deb https://download.docker.com/linux/ubuntu xenial stable
	    state: present
	
	- name: update apt and install docker community edition
	  apt: update_cache=yes name=docker-ce state=latest
	
	- name: install docker module for python
	  pip:
	   name: docker
	```   

### 5. Run the playbook 
- `ansible-playbook -i hosts ubuntu_playbook.yml`

### 6. Login to the EC2 node machine 
- Use your *public and private* EC2 keys and verify if the containers were successfully created from the playbook
	- `docker ps -a` to list all containers

---
# References
- [[demo-ansible-playbook|basic playbook example]]

## Tags
- #docker
- #ansible/demo/playbook/docker  
---