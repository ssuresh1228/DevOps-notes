Created: 2023-02-14 14:01
# Passwordless Authentication: AWS + Ansible
---
- ## Login to EC2 instance and create hosts file
	- Create [[]] file in `/Add-SSH-key-EC2-Ansible` directory
		- Create this directory if it doesn't exist: `mkdir Add-SSH-key-EC2-Ansible`
	- update hosts to which the SSH key must be copied to 
	- set `HostKeyChecking` property to 'no'
 >[!Example] Hosts file contents:
	>```
	>[hosts_add_key]
	>#hosts to copy the SSH to
	>18.191.56.95
	>18.217.65.201
	>
	>[hosts_to_add_key:vars]
	>#set HostKeyChecking to 'no'
	>ansible_ssh_common_args="-o StrictHostKeyChecking=no" 
 
  
- ## Create a new playbook named key.yml
>[!Example] key.yml contents:
>```
>---
>- name: "Add public key to EC2 instances"
>  hosts: hosts_add_key
>  vars:  
>   - status: "present"
>   - public_key: "~/.ssh/id_rsa.pub"
>     tasks:
> 
> 	- name: "Copy key file from "
> 	  authorized_key:
> 	    user: "{{ansible_user}}"
> 	    state: "{{status}}"
> 	    public_key:"{{lookup('file', '{{public_key}}')}}"	    

- variables:
	- `status` adds/removes ssh key from remote server
	- `public_key` is the public key which will be copied to the remote servers. **If no value is passed, the default value `~/.ssh/id_rsa.pub` will be copied**
	- `ansible_user` is the EC2 instance username to connect to the remote server

- ## Run the key.yml playbook with your .pem file 
	- `ansible-playbook key.yml -i hosts --user ec2-user --key-file /root/<user>/<your EC2 instance private key>-e "key=/root/.ssh/id_rsa.pub`

- ## Validate that you can login to the server using only a private key
	- `ssh -i /root/<user>/<your EC2 instance's private key>@EC2-instance-public-IP`
		- Ex) `ssh -i /root/sanju/sanjeevkey.pem ec2-user@18.191.56.95`

---
# References


## Tags
#AWS 
#ansible 
#EC2 

---