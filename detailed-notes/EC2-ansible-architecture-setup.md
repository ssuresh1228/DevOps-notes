Created: 2023-02-16 17:46

---
# Setting up and Configuring Ansible Master/Slave Architecture on EC2
---
- **This server will be the ansible master, and the [[EC2-tomcat-setup|Tomcat server]] configured on the 2nd EC2 instance will be the slave node**

### Setting up the EC2 Instance
1. On AWS Management Console, go to EC2 and launch a *Red Hat Enterprise (RHEL) 7 (HVM)* AMI
	  
2. Click _Next: Configure Instance Details_
	- Make sure port 22 (SSH) is allowed on inbound security group
	  
3. Click *Review and Launch*
	  
4. Create a new key-pair and save the public key to your local system
	  
5. Select the newly created server and SSH into it
	  
6. After logging in, run the following commands:
	- Become root user
		- `sudo su -`
				 
	- update all packages on this server
		- `sudo apt-get update -y`
				
	- install ansible prerequisites
		- `apt install rpm`
		- `rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm`
				
	- Install ansible and verify its version
		- `apt-get install ansible -y`
		- `ansible --version`
			
	- Create a new user + password
		- `useradd ansibleMaster`
		- `passwd ansibleMaster`
				
	- Add this user to sudoers
		- `visudo`
		- Scroll down to the end of the file (Shift + G) and add
			- `ansibleMaster    ALL=(ALL)    NOPASSWD:ALL`
					
	- Enable password authentication
		- `nano /etc/ssh/sshd_config`
		- enable password authentication and save
			
	- restart sshd for changes to take effect
		- `systemctl restart sshd`
			
	- Login as *ansibleMaster* on **this** server
		- `su -ansibleMaster`
			
	- Generate ssh key-pair
		- `ssh-keygen`
			
	- copy the **private IP address** of the [[EC2-tomcat-setup|tomcat server]] (ansible slave node)
		- `ssh-copy-id <EC2-tomcat-private-ip>`
			
	- Test passwordless auth by connecting to the tomcat server
		- `ssh <EC2-tomcat-private-ip>`
			
	- **To add more slave machines as hosts on this ansible controller, login as root user and run the following:**
		- `chown ansibleMaster:ansibleMaster /etc/ansible/hosts`
		- `nano /etc/Ansible/hosts`
			- delete all lines using "dd" and enter the slave node's *private IP* then save and quit
			
	- test connection to slave node(s)
		- `ansible all -m ping`
			
	- while still logged in as root user, create a directory for playbooks
		- `mkdir /opt/playbooks`
		- `chown -R ansibleMaster:ansibleMaster /opt/playbooks`
			
### Log in as the *ansibleMaster* user, and create the following playbooks/roles:
- `su - ansibleMaster`
- `cd /opt/playbooks`
	- `touch copyfile.yml`
	- `touch debian.yml`
	- `touch redhat.yml`
	- `touch ansible-role.yml`
- [[EC2-ansible-architecture-playbooks|Playbook contents here]]  

### Set up SSH servers on the [[EC2-jenkins-setup|Jenkins UI]] 
- Navigate to *Manage Jenkins*, then *Configure System*
	- Scroll down until the *SSH Servers* section, and add the [[EC2-tomcat-setup|tomcat server]] and this Ansible server's details:
	
#### ansible server details:
- name: `ansible-server`
- hostname: `<ansible server's private ip address>`
- username: `ansible-master`
- password: `<password set for this user>`
				
#### tomcat server details
- name:`tomcat-server`
- hostname: `<tomcat server's ip address>`
- username: `tomcat`
- password: `myPassword`
			
- Click on *Test Configuration* and check the resulting message
	- If successful, then apply and save
---

# References
- [Setting up Ansible master/slave config](https://blog.programster.org/setting-up-ansible)

## Tags
#ansible/setup/EC2 

---