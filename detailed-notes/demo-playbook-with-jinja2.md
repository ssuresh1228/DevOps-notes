Created: 2023-02-13 17:14
# Create a Playbook with a Jinja2 Template
---
## Problem Statement
- A monitoring server has been newly introduced in your environment. The `agents.conf` file must be updated with a list of the environment's servers & their details using a Jinja2 template.

## 1. Create `generate-agent-info.yml`
- Used to update `agents.conf`
>[!info] generate-agent-info.yml contents:
>![[Pasted image 20230213172003.png]]

## 2. Navigate to `~/playbooks/monitoring-server`
- List of servers is in the **inventory file** under the group `lamp_app` as shown below:
	- ![[Pasted image 20230213172222.png]]

## 3. Update `agent.conf.j2` using jinja2 template
- ![[Pasted image 20230213172859.png]]

## 4. Run the playbook
- `ansible-playbook -i inventory generate-agent-info.yml`
- This will update `agents.conf` for all hosts in the inventory file

---
# References


## Tags
#ansible-jinja2 
#ansible-playbook 

---