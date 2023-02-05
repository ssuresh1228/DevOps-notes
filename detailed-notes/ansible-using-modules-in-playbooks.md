Created: 2023-02-02 18:57
# Using Modules in Playbooks
---
## Steps for [[pres-ansible-server-provisioning#Playbooks|playbook]] creation
1. Create a new file with .yaml extension
2. Convert an [[pres-ansible-architecture#Ad-Hoc Commands|ad-hoc command]] into a playbook task

> [!example] Converting an ad-hoc command to playbook task:
> - ad-hoc command: `ansible all -m shell -a "wall Hello to Ansible"`
> - Playbook equivalent:
> ```
> - hosts: all
>   tasks: 
> 	  - name: wall command
> 	    shell: "wall Hello to Ansible"
> ```
> >[!note]
> >- `hosts`: servers used used for command execution
> >- `tasks`: list of commands to be executed on hosts
> >- `name`: used to identify tasks in execution output
> >- `shell`: module being used here

3. Run the playbook
	- `ansible-playbook -s -i inventory.ini helloplaybook.yaml`
		- location of inventory file is specified with `-i`
		- this [[pres-ansible-architecture#Inventory|inventory]] file is not at default location
			- `/etc/ansible/hosts`





---
# References
- [[ansible-module-types#Module Types|Ansible module types]]
- [Ansible docs on modules](https://docs.ansible.com/ansible/latest/plugins/module.html)

## Tags
#ansible-playbook 
#ansible-modules 

---