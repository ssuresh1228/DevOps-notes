# Ansible Setup on AWS EC2
Created: 2023-02-02 13:08

# Install Ansible 
1. Before installing the ansible package, add the ansible repository on the ubuntu system
  >[!info]
  >`sudo apt-add-repository ppa:ansible/ansible`

2. Run the update command before installation to update existing packages
>[!info]
>`sudo apt-get update`

3. Install the Ansible package
>[!info]
>`sudo apt-get install ansible`
>
>Check installed version with 
>`anisble --version`

---
# Setting up Hosts
1. Edit the [[pres-ansible-server-provisioning#Hosts|hosts]] file in the ansible directory
	- default location: `/etc/ansible/hosts`
>[!note]
>In the hosts file, add the server as shown:
>![[Pasted image 20230202142832.png]]

2. Test connection 
- `cd /etc/ansible`
>[!note]
>Use Ansible's ping module to check connection with hosts:
>`ansible -m ping <hosts>`

---

# References
- [[pres-ansible-server-provisioning#Hosts|Ansible hosts overview]]

## Tags
- #ansible 
- #AWS
- #EC2
---