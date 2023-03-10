Created: 2023-02-04 19:01
# Ansible Facts
---
## Overview
- Ansible collects info on remote hosts when a playbook is run
	- "gathering facts"
	- details collected are **facts or variables**
- Facts are _manually obtained_ by Ansible [[pres-ansible-architecture#Ad-Hoc Commands|ad-hoc commands]]
	- all playbooks call this [[ansible-module-types#Setup Module|setup module]] by default to gather facts

## [[ansible-module-types#Setup Module|Setup Module]]
- ad-hoc command to invoke setup module:
	- `ansible <hostname or groupname> -m setup`
- Can stop gathering facts by mentioning `gather_facts: no` in a playbook
- Can run the setup module and register output to a variable
	- whole set of facts will be in JSON format

## Types of Facts
Facts gathered from remote hosts can be divided into 3 main categories:
1. **List**
	- List of items/interfaces
	- info is enclosed in `[]`
2. **Dictionary**
	- Collection of key-pair values
	- info is enclosed in `{}`
3. **Ansible Unsafe Text**
	- variable that doesn't have any subpart; _stores data directly_
	- can be accessed directly by using the fact's name

> [!example]
> 1. run `ansible app -m setup -i ansible-hosts`
> 	- ![[Pasted image 20230204194347.png]]
> 	
> 	> [!info]
> 	> - gathered info from hosts are placed in the `ansible_all_ipv4_addresses` variable
> 	> 	- contains info in `[]` so it is a **list**
> 	> - the `ansible_apparmor` variable contains info in `{}`
> 	> 	- this is a **dictionary**
> 	> - the `ansible_architecture` variable is putting values after its `:`
> 	> 	- this is **ansible unsafe text**

## Using Facts in a Playbook
- all variables can be used in playbooks by calling them in [[ansible-jinja2-templates|jinja2]] syntax 
- These variables can be used in many cases/requirements:
	- conditional based execution
		- when remote hostname is "serverA" or a server's OS is redhat
	- When mount point used percentage > 80%
	- When gettingn remote box info
		- hostname
		- fqdn
		- mac address
		- IP address
		- etc
## Accessing Facts
- use the name (without the _ansible_ keyword) to access variables from the facts in a playbook
>[!example] 
>`ansible_facts["system"]`

>[!example] Accessing facts using a playbook
>- Fetch the facts ad display them using a playbook:
> ```
>	- hosts: all
>	  tasks:
>	  - debug:
>	      var: ansible_facts

> [!example] Accessing a _specific_ fact using a playbook
> ```
> - hosts: all
>   tasks:
>   - debug:
>       var: anisble_facts["cmdline"]
 

 
--- 
# References
- [ansible docs on facts](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_vars_facts.html)
- [ansible facts & how to use them](https://www.middlewareinventory.com/blog/ansible-facts-list-how-to-use-ansible-facts/)
- [redhat docs on facts](https://www.redhat.com/sysadmin/playing-ansible-facts)
- [facts and examples](https://www.educba.com/ansible-facts/)

## Tags
#ansible/facts

---