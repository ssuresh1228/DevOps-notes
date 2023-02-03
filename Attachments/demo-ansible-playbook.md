Created: 2023-02-02 14:45
# Demo: Basic Ansible Playbook
---
1. Navigate to Ansible directory
	- `cd /etc/ansible`
2. Create a YAML file at this location
>[!example]
>Write the tasks for the play
>```
>---
>- hosts: all
>  become: true
>  vars:
> 	 ansible_become_pass: myPassword
>  tasks:
> 	 - name: install ntp
> 	 apt:
> 		 pkg: ntp
> 		 state: present
> 	notify:
> 		- run update
> 		
> 	- name: install vim 
> 	apt: 
> 		pkg: vim
> 		state:present
> 		
> 	- name: start ntp service
> 		service: 
> 			name: ntp
> 			state: started
> 			enabled: true
> 			
> 	handlers:
> 	- name: run update
> 	  apt: 
> 		  update_cache: yes

3. To run the playbook, use the `ansible-playbook <playbookName>` command
>[!info]
>Running the above playbook:
>![[Pasted image 20230202145937.png]]


---
# References
- [[pres-ansible-architecture#Playbooks|Playbook overview]]

## Tags
- #playbook 
- #ansible 
---