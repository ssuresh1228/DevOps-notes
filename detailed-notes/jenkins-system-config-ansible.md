Created: 2023-02-18 14:08
# Jenkins System Config: Ansible Server 
---
- ## On the [[EC2-jenkins-setup|Jenkins UI]], add the [[EC2-ansible-setup|Ansible server]]
	- Navigate to *Manage Jenkins*, then *Configure System*
	- Scroll down until the *SSH Servers* section, and add the following [[EC2-ansible-architecture-setup|details]] of the ansible server configured during setup:
		- `Name: ansible-server`
		- `Hostname: <server's-private-ip>`
		- `username: ansibleMaster`
		- `Password: ansibleMaster`


---
# References


## Tags
---