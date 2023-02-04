Created: 2023-02-01 14:33
# Server Provisioning with Ansible CLI & Playbooks

---

# Automation using Ansible

## Centralizing Config Management
- Configuration management without an automation tool requires a lot of manual tasks:

 > [!note]
	> - Each server will require _its own script_ for its configuration:
	> - ![[Pasted image 20230201143826.png]]
	> - With Ansible, a _single_ script can bring all servers (managed nodes) to the desired state:
	> - ![[Pasted image 20230201144018.png]]

## Automation Using Ansible
- The desired state of servers are outlined in an automation script
- Ansible's automation engine handles differences between host servers
- 2 methods of automating:
	- [[pres-ansible-architecture#Ad-Hoc Commands|ad-hoc commands]]
	- [[pres-ansible-architecture#Playbooks|playbooks]]

---
# Playbooks

 > [!info]
 > - [[pres-ansible-architecture#Playbooks|playbooks]] are Ansible's access point for server provisioning
 > - Usually written in YAML
 > - Advanced use-cases include multi-tier layouts and load balancing

## Modules
- [[pres-ansible-architecture#Modules|Modules]] are units of code that do work
- Used to control system resources & handle system tasks
- Can use built-in modules from Ansible's built-in library or create custom modules
> [!note]
	 >- Almost all modules support taking in arguments in key-value format
	 >		- ![[Pasted image 20230201150219.png]]

---
# Playbook Structure

> [!tip]
> major components of a [[pres-ansible-architecture#Playbooks|playbook]]:
> - 3 hyphens to denote start of a playbook
> - Hosts
> - _become_ keyword
> - _vars_ keyword 
> - tasks section
> - Handlers
> - Blocks

## Hosts
- Each play begins with the host(s) that the play will execute on 
- A playbook can have multiple plays
> [!example]
> ![[Pasted image 20230201152557.png]]
> - specifies play to run on all managed nodes

## _become_ keyword
- used for privilege escalation 
> [!example]
> ![[Pasted image 20230201152107.png]]
> - 3 directives specified:
> 	- become user _desmond_
> 	- run tasks with sudo privileges

## _vars_ keyword
- Used to define variables
- must be defined before their use 
> [!example]
> ![[Pasted image 20230201152922.png]]

## Tasks section
- Defines all tasks to be executed on managed nodes
- **A single play can define multiple tasks**
- Tasks are executed sequentially
>[!example]
>![[Pasted image 20230201171110.png]]

## Handlers 
- Tasks that are based on some action/trigger
>[!example]
>![[Pasted image 20230201171235.png]]

## Blocks
- used to create groups of tasks in a playbook
- _all directives in a block apply to all tasks in the block_
>[!example]
>![[Pasted image 20230201171346.png]]

___
# Variables
- used to collect and store facts from remote systems 
>[!note]
>Variables can be defined and used anywhere in Ansible:
>- playbooks
>- ad-hoc commands
>- inventory

## Defining and Referencing simple, list, and dictionary #variables
>[!example]
>- defining & referencing a simple variable
>`region: asia`
>`server: "{{region}}"`
>
>- list variables are defined in YAML list format or in []:
>	```
>	#YAML list
>	regions_1:
>		- asia
>		- europe
>		- northamerica
>	
>	#alt syntax
>	regions_2: ['asia','europe', 'southamerica']```
>
>- defining & referencing dictionary variables
>	
>	```
>	#defining dict variables
>	sample:
>		arg1:true
>		arg2:false
>	
>	#2 methods of referencing dictionary variables
>	sample['arg1']
>	sample.arg2


## Registering Variables
- Output from other tasks can be stored and used as variables _for other variables_
>[!example]
>```
>- tasks:
>	- name: execute shell script
>	- shell: myScript.sh
>	- register: result
>	
>	- name: restart docker if result < 5
>	- service: "name=docker state=restarted"
>	- when: result.rc<5

---
# Handlers
- Tasks that execute only if a system config changes due to a task
	- Only executed if a task notifies it for execution
- Require globally unique name 
>[!example]
>```
>#Syntax
>- name: install ntp
>	apt:
>		pkg: ntp
>		state:present
>	notify:
>		- run update
>
>handlers
>- name: run update
>	apt:
>		update_cache: yes


## Controlling Handlers
- _Always_ run after a play has competed its task execution
	- Ensures that handlers only run _once_ even on multiple callings
- The `flush handlers` task allows users to execute handlers that have been notified before the play ends:
>[!example]
>```
>- name: flush handlers
>   meta: flush_handlers
 
---
# Loops
 - remove need to create multiple plays/tasks for a duplicated task
 - useful for executing a repeating task








# References
- [Ansible playbook documentation](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks.html)

## Tags
- #adhoc-commands 
- #ansible-playbook 
---