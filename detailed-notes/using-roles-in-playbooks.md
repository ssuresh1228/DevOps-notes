Created: 2023-02-03 17:34
# Using Roles in Playbooks
---
## Adding Tags to Roles
- Adding a tag to a role will apply it to all tasks in that role
- When using `vars: ` in the `roles: ` section of a [[pres-ansible-architecture#Playbooks|playbook]], variables are added to the play's variables
	- available for all tasks in the play before & after the role

## Finding and Storing Roles
- By default, Ansible looks for roles in 2 locations:
	- `roles/` directory
	- `/etc/ansible/roles`
>[!note] Storing roles in a different location
>- set `roles_path` configuration option so Ansible can find roles
>
>- Can also call a role with its path in a playbook:
> ```
> ---
> - hosts: webservers
>   roles: 
> 	- role: '/path/to/my/role'

## Using Roles

### 1. Play level with roles option
- Classic method of using roles in a play
> [!example]
	> ```
	> ---
	> - hosts:
	> # common and webservers are the roles here
	>  roles:
	>    - common
	>    - webservers
	>```
	
- Ansible treats the roles as static imports and processes them during playbook parsing
> [!note] Ansible executes [[pres-ansible-architecture#Playbooks|playbooks]] in the following order:
> 1. `pre_tasks` defined in the play
> 2. handlers triggered by `pre_tasks`
> 3. every role listed in `roles`
> 4. `tasks` defined in the play
> 5. handlers triggered by roles/tasks
> 6. `post_tasks` defined in the play
> 7. handlers triggered by post_tasks


### 2. Task level with `include_role`
- using `include_role` allows for dynamic reuse of roles anywhere in the `tasks` section of a play

### 3. Task level with `import_role`
- using `import_role` allows for statuc reuse anywhere in the `tasks` section of a play


---
# References
- [Ansible docs: using roles in playbooks](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html#using-roles)

## Tags
- #ansible-roles
- #ansible-playbook 
---