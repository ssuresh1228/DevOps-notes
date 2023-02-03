Created: 2023-02-02 15:17
# Module Overview
---
- Modules are programs which executed on hosts when a playbook is run

- Ansible has integration with Python to write/create custom modules

## Example: Custom Hello World Module

### 1. Create a new playbook `hello_world.yml` to call your new module
>[!info] Sample playbook
	>```
	># a simple playbook to demonstrate custom modules
	>- hosts: localhost
	>  tasks:
	>  - name: test that hello_world module works
	>    hello_world:
	>    register: result
	>   
	>  - debug: var=result
	> ```	

### 2. Create a library directory with a python file in the root of the defined project
>[!example] File/directory structure
> ![[Pasted image 20230202163238.png]]

### 3. Add the following code to `hello_world.py`
> [!example] `hello_world.py` contents:
> ![[Pasted image 20230202163554.png]] 
> 
> >[!note] Details
> > - must use `#!/user/bin/python`
> > - must import `ansible.module_utils.basic` to use `AnsibleModule`
> > 	- Used for passig params in/out of the module
> > 	- Only passing _data out of the module_ here with the value *theReturnValue* 
> > - must define program content in `main()`
> > 

### 4. Run the `hello_world.yml` playbook
> [!tip] Syntax to run a playbook
> ```
> ansible-playbook hello_world.yml
> ```
> > [!info] Running this playbook returns 'hello world' as metadata:
> > ![[Pasted image 20230202164917.png]]

---
# Module Types
- [[pres-ansible-server-provisioning#Modules|Modules]] in Ansible are standalone scripts used in a [[pres-ansible-server-provisioning#Playbooks|playbook]]
> [!info] Ansible has 5 types of modules:
> 1. Setup Module
> 2. Command Module
> 3. Shell Module
> 4. User Module
> 5. Copy Module

## Setup Module
- Used to get system info of the target machine(s)
>[!example] Running setup module on a managed node:
> - On the controller node, change directory to `Ansible_project` and run the following command:
>	- `ansible target2 -m setup -i inventory.txt`
> - Shows system related info of the machine _target2_ 

## Command Module
- Used to execute a specific command on a target machine and display its output
>[!example] Running command module on a managed node:
> - On the controller node run the following command:
>	- `ansible target2 -m command -a "free -m" -i inventory.txt`
> - Shows memory info on machine _target2_

## Shell Module
- Used to execute any command in the shell
	- These commands are ran in `/bin/sh` shell
	- Can use operators like `<, |` and environment variables in this module
>[!example] Running shell module on a managed node:
> - Run `free -m` command on *target2* machine and store its output in memory.txt:
>	- `ansible target2 -m shell -a 'free -m > memory.txt' -i inventory.txt`

## User Module
- Used to create and delete a user account in the system
>[!example] Creating and deleting a user
>- creating a new user:
>	- `ansible web -m ansible.builtin.user -a "name=newUser uid=1041 group=admin"`
>- deleting a user:
>	- `ansible target1 -m user -a 'name=newUser state=absent' -i inventory.txt`

## Copy Module
- Used to copying files to target machine(s)

>[!example] 
>- Run the below command to copy a file "fstab" from controller to target2 machine
>	- `ansible target2 -m copy -a "src=/etc/fstab dest=/mnt/" -i inventory.txt` 

---
# References
- [[pres-ansible-server-provisioning#Playbooks|Playbook/module overview]]
- [User module examples](https://adamtheautomator.com/ansible-create-user/) 
- [User module article](https://www.ansiblepilot.com/articles/create-user-account-ansible-module-user/#ansible-create-a-user-account)

## Tags
- #ansible-modules
- #ansible-playbook
- #ansible-module-types
---