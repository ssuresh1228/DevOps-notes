# Demo: Ansible Modules & Ad-Hoc Commands
---
## Part 1: Installing & Configuring Ansible on CentOS 7

1. Make sure that CentOS 7 is updated with the latest packages and EPEL repository is installed:
	- `yum update -y`
	- `yum install epel-release -y`

2. After EPEL is installed, install Ansible with yum:
	- `yum install ansible -y`
	- Check Ansible version with `ansible --version`

3. Set up Ansible's `hosts` file; must be set up for communication with other machines:
	- Open the file with root privileges:
		- `sudo nano /etc/ansible/hosts`

4. Add the Public IP Address(es) of your node(s) to the `hosts` file
>[!example] Example IP addresses in a hosts file:
>![[Pasted image 20230212153844.png]]
>

## Part 2: Running Simple Modules

>[!note]
>Passwordless authentication with remote servers must be enabled before running these modules

1. Ping all servers you've configured in the hosts file:
	- `ansible -m ping all`
	- Basic test to make sure that Ansible has a connection to all its host nodes

2. The [[ansible-module-types#Shell Module|shell module]] lets us send a terminal command to the host node and retrieve its results
	- Viewing memory usage on a node: `ansible -m shell -a 'free -m' all`
		- Arguments can be passed into a script by using `- a` switch. 