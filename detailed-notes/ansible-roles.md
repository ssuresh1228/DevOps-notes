Created: 2023-02-02 19:49

---
# Purpose of Roles
- provide a framework of independent/interdependent collections of variables, tasks, files, templates, and [[ansible-module-types#Module Types|modules]]
> [!note]  Why use roles?
> 1. Roles are the primary mechanism for breaking down a [[ansible-using-modules-in-playbooks#Steps for pres-ansible-server-provisioning Playbooks playbook creation|playbooks]] into multiple files
> 2. Breaking down a playbook into parts allows use of reusable components
> 3. Roles simplify playbooks; makes it easier to reuse
---

---
# Ansible Galaxy
- Role and collection manager 
- repository of roles for steamlining tasks and playbooks
- Hosts community createdAnsible roles and collections

>[!info] 
>Instead of writing/rewriting roles from scratch, you can directly install these roles using **Ansible Galaxy command line tool** and use them in playbooks

## Installing a Role from Ansible Galaxy
> [! tip] Searching for a role in Galaxy:
> - `ansible-galaxy search <role>`

> [!example] Example: Searching for a MySQL role:
> - `ansible-galaxy search mysql` 

___
# Role Directory Structure

>[!info] Directory Structure
>- ![[Pasted image 20230203150428.png]]
>	- defaults, files, [[pres-ansible-server-provisioning#Handlers|handlers]], meta, [[pres-ansible-architecture#Tasks|tasks]], templates, and [[pres-ansible-architecture#Variables|vars]] are subdirectories in the role's directory
>	- Each role's directory must include _at least one of these subdirectories_
>	- Each subdirectory must contain at least one main.yml file

## Defaults Subdirectory
- contains data on role
- ideally the default variables for the role

## Files Subdirectory
- contains regular files that are deployed by this role
- any scripts to be run on target [[pres-ansible-server-provisioning#Hosts|host(s)]] or files to be transferred should be placed in this directory

## Handlers Subdirectory
- Contains handlers used by a role

## Meta Subdirectory
- Contains files that establish role dependencies
- Has info on role and its author:
	- name, company, etc.

## Templates Subdirectory
- holds all dynamic files/templates that use variables
	- variables can be substituted during role's execution

## Tasks Subdirectory
- Contains all tasks to be executed by the role that would usually be in a playbook

## Vars Subdirectory
- Contains a role's variables
- Default variables in the default directory are _overwritten_ by the same variables defined here 
- ---
# Benefits of Using Roles

- Consider 8 tasks to be run on 2 remote nodes
	- **Approach 1**: 
		- Define all tasks in a _single_ playbook file
			- tedious and complicated
	- **Approach 2**:
		- Create 8 separate roles where each role will perform a single task
			- Call these roles in the playbook 

> [!tip] Major benefits of using roles
> - Each role is independent of other roles
> 	- Execution of any role doesn't depend on another role's execution
> 	
> - Roles can be modified and reused
> 	- eliminates the need for rewriting plays/tasks in playbooks

---
# References
- [Ansible roles documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html#role-directory-structure)
- [Ansible Galaxy user guide](https://docs.ansible.com/ansible/latest/galaxy/user_guide.html)

## Tags
#ansible/roles/galaxy

---