Created: 2023-02-03 18:41
# Defining, Executing, and Managing Roles
---
## 1. Define the Role
- Creating a [[ansible-roles-in-playbooks#Using Roles|role]]
>[! note] Command for creating a role
>- use [[ansible-roles#Ansible Galaxy|ansible galaxy]] init command to create an ansible role named 'motd'
>- `ansible-galaxy init motd`
>- this role will be created in `<project>/roles/<role-name>`
>	- i.e. `base/roles/motd` in this case

- Run `tree motd` to view the directory structure
	- ![[Pasted image 20230203191728.png]]

## 2. Create Tasks for the Role
- Create tasks to update `/etc/motd` file using ansible playbook roles
	- main.yml is inside the tasks folder
		- ![[Pasted image 20230204160548.png]]

## 3. Create Ansible Role Playbook to Execute the Role
- Create a playbook file `motd-role.yml` under the base project directory
	- ![[Pasted image 20230204160659.png]]
		- Only role info is specified here; no tasks

## 4. Deploy Ansible Playbook Roles
- After creating the role and playbook file, deploy the playbook roles to execute the motd role on managed host(s)
	- syntax: `ansible-playbook <playbook-name>`
	- ![[Pasted image 20230204160928.png]]

---
# References


## Tags
- #ansible/roles/managing 
---