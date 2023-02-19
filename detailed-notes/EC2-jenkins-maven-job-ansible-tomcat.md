
1. Created: 2023-02-18 15:04
# Configuring Jenkins Maven job with Ansible, Tomcat, and GitHub Web Hook
---
- This is the next step after [[implementation-of-automating-CI#2. Configuring Ansible & Tomcat Servers in Jenkins UI|configuring and adding the tomcat and ansible servers in Jenkins UI]]

- Return to the maven job configured [[EC2-jenkins-setup#Verify Jenkins, Git, and Maven Configuration|here]]
	- Click *Configure*
	- Scroll down to *Post-build* Actions
		- click on *Add post-build step*
			- select `Send files or execute commands over SSH`
			- Add the [[jenkins-system-config-ansible|ansible details configured in Jenkins UI]]
			- *Transfers* Section
				- in *Source Files* add `maven-project/webapp/target/*.war*`
				- in *Remote Directory* add `/opt/playbooks`
		
		- Add Another Build Step
			- click on *Add post-build step*
				- select `send files or execute commands over SSH`
				- Add the [[jenkins-system-config-ansible|ansible details configured in Jenkins UI]]
				- *Transfers* Section
					- in *Exec Command,* add
						- `ansible-playbook /opt/playbooks/copyfile.yml`
		
		- Add another post-build step
			- Deploy war/ear to a container
				- enter `**/*.war` 
				- *Containers* Section
					- Give the [[jenkins-system-config-tomcat|Tomcat credentials + URL]]
		
		- Add another build step to work with the [[EC2-ansible-architecture-setup#Log in as the *ansibleMaster* user, and create the following playbooks/roles:|ansible roles]] 
			- Will install curl package on the ansible server to test if Apache webserver is able to be reached
				- `curl <public-ip-apache-webserver:8090>`
				- Ansible will identify the server's OS and run the necessary command to install the curl package
			- *Exec Command* Section
				- enter `ansible-playbook /opt/playbooks/ansible-role.yml`
				- save + apply
		
  - Build the Job to test the configuration

- In the remote repository, generate an access token
	- Add this token to Jenkins through *Manage Jenkins* --> *Configure System*
	- Select the maven job, and click on configure
		- in *Build Triggers* Section, select `GitHub hook trigger for GitSCM polling`

---
# References


## Tags
---