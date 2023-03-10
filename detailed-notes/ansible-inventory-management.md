Created: 2023-02-02 18:08
# Inventory Management
---
- Ansible uses [[pres-ansible-architecture#Inventory|inventory files]] to 
	- keep track of hosts making up the infrastructure
	- Reach hosts for running commands/playbooks
>[!info] How Ansible works
>- ![[Pasted image 20230202181841.png]]

- **Inventory file provides**:
	- Node on which Ansible installation was run on
	- List of hosts where Ansible modules need to be run 

- **Ansible Management Node**
	- Makes SSH connection to hosts
	- Executes modules on host machines

>[!info] Prerequisites for Inventory Management
> - 1 Control Node
> 	- Ubuntu machine with Ansible installed
> 	- Configured to connect to hosts via SSH keys
> 	
> - 2 or more remote Ubuntu servers

## Creating Inventory File
1. navigate to home directory and create ansible directory
2. navigate to ansible directory and create new inventory file
3. A list of nodes with 1 server per line is enough for a functional inventory file
	- hostnames and IP addresses are interchangable
		- ![[Pasted image 20230202184150.png]]
4. Use the ansible-inventory command to validate and get info 
	- `ansible-inventory -i inventory --list`
---
# Dynamic Host Inventory file
- A script written in python, php, or some other language
- Useful for cloud platforms like AWS where IP addresses change when servers restart
- Ansible has inventory scripts for 
	- GCP
	- RackSpace
	- AWS EC2
	- OpenStack
## Advantages
- Reduces human error
- minimal effort to manage
> [!note]
> Any programming language can be used to customize dynamic inventory, but a dynamic inventory **must return in JSON** when appropriate options are passed


---
# References
- [Ansible inventory documentation](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html)

## Tags
- #ansible/inventory/management 
---