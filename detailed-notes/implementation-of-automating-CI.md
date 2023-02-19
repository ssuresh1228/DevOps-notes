Created: 2023-02-14 20:49
# Automating Continuous Integration: Jenkins, Tomcat, and Ansible
---
# 1. Set up EC2 instances

>[!info] Each EC2 instance will have its own installation:
> - 1 with Jenkins (controller node for CI) + Maven + Git
> - 1 with Tomcat (application server)
> - 1 with Ansible (Deployment tool)

- [[EC2-jenkins-setup|Setting up and Configuring Jenkins on EC2]]
- [[EC2-tomcat-setup|Setting up and Configuring Tomcat on EC2]]
- [[EC2-ansible-architecture-setup|Setting up and Configuring master/slave architecture with Ansible on EC2]]

# 2. Configuring Ansible & Tomcat Servers in Jenkins UI
- After setting up the EC2 servers, now we must these 2 servers in the Jenkins UI

> [!info] Must integrate servers in Jenkins UI:
> - Tomcat Server
> - Ansible Server

- [[jenkins-system-config-tomcat|Configuring tomcat server in Jenkins system config]]
- [[jenkins-system-config-ansible|Configuring Ansible server in Jenkins system config]]
- After configuring these 2 servers, return to the [[EC2-jenkins-setup#Verify Jenkins, Git, and Maven Configuration|job]] created to verify the maven/git configuration.
	- [[EC2-jenkins-maven-job-ansible-tomcat|Configuring the maven project with Ansible and Tomcat]]

# 3. Test Final CI Configuration
- SSH to the [[EC2-jenkins-setup|Jenkins server]] and run the following commands:
	- `git clone <remote-repo-link>`
	- `nano maven-project/webapp/src/main/webapp/index.jsp`
		- make any changes, then save and exit
	- `git init`
	- `git add .`
	- `git remote add origin <remote-repo-URL>`
	- `git commit -m "CI Test"`
	- `git push origin main`
	
- After the build completes, check the webapp for your new changes at 
	- `http://<tomcat-server-public-ip>:8090/webapp`

---
# References
- [Guide with Pictures](https://s3.amazonaws.com/module-non-videos/demo_1%20-%20automating%20continous%20integration_v1_r6m_fblu1s5.pdf)

## Tags
#AWS 
#EC2 
#continuous-integration 
#jenkins
#ansible 
#tomcat
#maven

---