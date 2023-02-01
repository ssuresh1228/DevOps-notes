Created: 2023-01-31 18:23

# Architecture Overview
- ![[Pasted image 20230131185930.png]]
----
# Control and Managed Nodes
>[!INFO]
>_Control Node_: any machine in which Ansible is installed to **manage** other nodes
>
>_Managed Node_: Any machine managed with ansible

---
# Inventory
- File that contains a list of _all_ managed nodes
	- Users can group machines as requires
- Common file formats: ini, YAML
>[!tip]
>Ansible can work on _multiple systems at the same time by selecting *portions* of hosts_ in the inventory
 
---
# Playbooks 
- Used to implement changes by users
> [!info]
> - Playbooks contain plays
> - plays contain tasks
> - tasks call modules
> 	- modules are the individual unit of work (programs) executed on the servers

---
## Variables
- Used to manage/represent differences between systems
	- Can be lists and dictionaries (key:value pairs)
> [!example]
> ![[Pasted image 20230131193406.png]]

---

## Tasks
- A unit of action; executed sequentially by default
- executable with **ad-hoc commands**
> [!example]
> ![[Pasted image 20230131193834.png]]
> 		- 1st play targets web servers
> 		- 2nd play targets database servers

---
## Modules
- Ansible connects to managed nodes and pushes out small programs called _modules_
	- These modules bring the system to its desired state
- Ansible uses SSH to execute modules and remove them when execution is finished
---
# CMDB
- Configuration Management Database
- Keeps a record of all changes made to the system
---
# Ad-Hoc Commands
- Uses command line to run a task on 1 or more managed nodes
> [!info]
> Syntax: `ansible [pattern] -m [module] -a "[module options]"`

---
# Ansible Facts
- Variables containing info on remote systems
	- Eg. OS, IP addresses, file systems, etc.
>[!example]
>To see all available facts, add this task to a play:
>	- `ansible <hostname> -m ansible.builtin.setup`

---


---
# References
- [[Basic Intro to Config Management]]
- [Edureka Ansible Presentation 1](https://learning.edureka.co/classroom/presentation/1483/12387/1479293?tab=CourseContent)

## Tags
#ansible
#configuration-management
#playbook
#variables
#modules
#tasks
#adhoc-commands

---