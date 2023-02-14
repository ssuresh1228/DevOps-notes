Created: 2023-02-13 19:06
# Ansible on AWS
---
## EC2 and EBS 

### EC2
- Elastic Compute Cloud
- Virtual server in AWS cloud 

### EBS
- Elastic Block Store
- EC2 instances come with an EBS volume
	- This is where the OS is installed/configured

## Preparing Ansible to Work with AWS

### Passwordless Authentication

#### Benefits
- Strengthens security by eliminating password management
- Improves UX by providing unified access 
- Simplifies IT operations by eliminating password management
	
#### Add EC2 instance without password in hosts file
- By default, EC2 linux instances use SSH key files for authentication instead of SSH usernames/passwords
	- Advantage: no need for password
	- Disadvantage: connecting to instances in private subnets requires a private key; **do not store private keys on controller**
		- Overcome this disadvantage by using **SSH agent forwarding (ssh-agent) on client**
			- Enables an admin to connect from controller to a host *without storing the private key on the controller*

---
# References


## Tags
#EC2
#AWS 

---