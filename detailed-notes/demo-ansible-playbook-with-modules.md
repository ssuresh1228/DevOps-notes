# Demo: Ansible Playbook with Modules and Roles

## Problem Statement: Create, validate, and execute a playbook to install httpd

1. Create a **httpd.yml** file with the below content in the ansible controller machine:
> [!info] httpd.yml contents:
> ```
> - hosts: web1
>   tasks: 
>   - name: install httpd package
>     yum: name=httpd state=installed

2. Check the inventory file; this has the hosts on which this  playbook will run on
	- `cat inventory`

3. Validate the playbook:
	- `ansible-playbook -i inventory httpd.yml --check`

4. Execute the playbook
	- `ansible-playbook -i inventory httpd.yml`
