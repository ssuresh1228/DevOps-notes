Created: 2023-02-04 16:10
# Managing Inclusions
---
## Playbook Roles and 'Include' Statements
- Including task files allows us to break down configuration policy into smaller files
	- Task also includes pull in tasks from other files
	- Since handlers are also tasks, handler files can be included in the `handler` section

- Playbooks can contain plays from other playbook files
	- PLays can be inserted into the playbook to create a list of plays

- Ansible roles include files
	- These can be combined to create clean and reusable abstractions

## Using "Include" Statements
- `task` includes are static when the include statement meets the following:
	- include doesn't use any loops
	- included file name doesn't use any variables
	- static option isn't explicitly disabled
	- ansible.cfg options to force static includes are disabled
>[!note] 2 options in ansible.cfg config for static include statements:
>- **task_includes_static**
>	- Forces all include statements in `tasks` section to be static
>- **handler_includes_static**
>	- Forces all include statements in `handlers` section to be static 

## Using "include" Roles
- Roles are automation around `include` directives
	- Automatically load certain vars_files, tasks, and handlers based on known file structure
- Grouping content based on roles allows easy sharing with other users
>[!example] In a playbook, a role looks like this:
> ```
>#example playbook
>---
>- hosts: webservers
>  roles:
>    - myRole
>    - webservers
> ```
>>[!info]  Behaviors for role `myRole`:
>> 	- if `roles/myRole/tasks/main.yml` exists
>> 		- tasks listed in this `main.yml` will be added to the playbook
>> 	- if `roles/myRole/handlers/main.yml` exists
> >		- handlers listed in this `main.yml` will be added to the playbook
>> 	- if `roles/myRole/vars/main.yml` exists
>> 		- variables in this `main.yml` will be added to the playbook
>> 	- if `roles/myRole/defaults/main.yml` exists
>> 		- variables in this main.yml will be added to the playbook

---
# References
- [Ansible docs: Playbook Roles & Include Statements](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_roles.html#playbook-roles-and-include-statements)

## Tags
- #ansible-playbook 
- #ansible-includes  
---