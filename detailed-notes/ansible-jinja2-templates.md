Created: 2023-02-04 16:55
# Configuring Jinja2 Templates
---
## Jinja2 Overview

- Creating standard config files for each node is too much work
	- templating solves this problem

> [!Info] What is Jinja2?
> - python based templating engine
> - comes with multiple servers in IT environment 
> 	- Configurations vary each time
> - Jinja2 templates are simple text files that store variables that change over time
> 	- When playbooks are executed, these variables get evaluated and replaced with their actual values defined in the playbook
> 		- provides an efficient/versatile solution to make/alter configuration file

## Templates
- jinja2 templates are often used to create files/replace config files on servers
- Can perform conditional statements:
	- loops
	- if-else
	- transform data using filters, etc
- use the `.j2` file extension

## Template Architecture
 > [!note] 
> - tags in a jinja2 template file
> 	- `{{}}` 
>		- embeds variables and prints their value during execution
> 	- `{% %}`
>		- used for control statements (e.g. loops and if-else statements)
>	- `{# #}`
>		- used for comments

## Why use Jinja2?
- Templates reduce the requirement for each file we write
	- Hence Ansible uses this for its templating language
- Helps to minimize requirements on the target host
	- Passes minimum info needed for executing the task
	- Target machines don't need a copy of all data from controller machine

## Template workflow
- **Templating only takes place on the controller node before the command is sent and executed on target machine(s)**
	- Comprises of all configuration parameters with variables defined with dynamic values
		- On playbook execution, the variables are replaced with updated relevant values based on situation/condition
			- ![[Pasted image 20230204172848.png]]

## Accessing variables
1. Template file directory
	- Ansible looks for template files in 
		- `project` directory
		- `templates` directory in `project` directory
			- **create a templates directory for organization**

2. Creating a jinja2 template
>[!example] creating a template named `index.j2`:
>- create the file (with j2 extension) and add the following:
>```
>A message from {{ inventory_hostname }}
>{{ webserver_message }}

3. Creating a playbook using a jinja2 template
>[!info] Create a playbook named `check-apache.yml` with the following:
>```
>---
>- name: check if apache is working
>  hosts: webservers
>  vars:
>    webserver_message: "Hello, this is a webserver message"
>  tasks:
>  
>    # make sure apache is running	 
>    - name: start httpd
>      service: 
>        name: http
>        state: started
>        
>    # process/transfer index.j2 template to index.html  
>    - name: create index.html with jinja2
>      template:
>        src: index.j2
>        dest: /ver/www/html/index.html

	- note that httpd package was already installed
4. Run the playbook
 - syntax: `ansible-playbook check-apache.yml`
> [!note] Playbook output:
> ![[Pasted image 20230204185247.png]]

---
# References
- [Ansible docs: templating with jinja2](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_templating.html)
- [How to use jinja2 template in a playbook](https://www.linuxtechi.com/configure-use-ansible-jinja2-templates/)

## Tags
- #ansible/playbook/jinja2
---