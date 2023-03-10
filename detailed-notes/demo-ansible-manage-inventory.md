Created: 2023-02-13 17:33
# Add/Remove Host from Inventory
---
## Problem Statement:
- Adding and removing a host from the inventory file

## 1. Access home directory and create a new folder to hold Ansible's files
- `mkdir ansible_demo`
- `cd ansible_demo`

## 2. Create a _new_ inventory file
- `nano inventory`

## 3. Enter a list of your nodes, 1 server per line
- Use node's **public IP address**
- Once the inventory is set up, use this command to list all present nodes
	- `ansible-inventory -i inventory --list`
	- Although we haven't explicitly set up groups in this inventory, output shows 2 groups
		- _all_ refers to all nodes in the inventory
		- *ungrouped* refers to servers that aren't listed in a group
	
## 4. Remove hosts from inventory
- Remove the entries from `~/ansible/inventory`
	- ![[Pasted image 20230213175223.png]]

---
# References


## Tags
#ansible/inventory/hosts 

---