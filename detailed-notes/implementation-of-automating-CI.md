Created: 2023-02-14 20:49
# Automating Continuous Integration: Jenkins, Tomcat, and Ansible
---
# 1. Set up EC2 instances
>[!info] Each EC2 instance will have its own installation:
> - 1 with Jenkins (controller node for CI) + Maven + Git
> - 1 with Tomcat (application server)
> - 1 with Ansible (Deployment tool)

- ## 1st EC2 Instance: Jenkins Setup, Installation, & Configuration

	- ### EC2 instance setup, Jenkins Prerequisites + Installation
		1. On AWS Management Console, go to EC2 and launch a *Red Hat Enterprise (RHEL) 7 (HVM)* AMI
	
		2. Click _Next: Configure Instance Details_
		- make sure _port 8080_ is allowed on inbound security groups
	
		3. Click *Review and Launch*
	
		4. Create a new key-pair and save the public key to your local system
	
		5. Select the newly created instance in EC2 console and SSH to it
	
		6. After logging in to that server, run these commands in sequence:
			- become root user
				- `sudo su -` 
			
			- update all packages on the server
				- `apt-get update -y`
		
			- install java
				- `apt-get -y install java-1.8`
		
			- check default java version
				- `java -version`
		
			- check java path to be added to user profile 
				- `find /usr/lib/jvm/java-1.8* | head -n 3`
				- `export JAVA_HOME=<result of previous command>`
		
			- make this change persist across reboots
				- `nano .bash_profile`
				- Enter the JAVA_HOME path here
		
			- save the .bash_profile 
				- `source .bash_profile`
		
			- verify the updated path
				- `echo $PATH`
		
			- Install Jenkins
				- `apt-get -y install wget`
				- `wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo`
				- `rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key`
				- `apt-get -y install jenkins`
			
			- Start and enable Jenkins
				- `systemctl enable jenkins`
				- `systemctl start jenkins`

	- ### Setup Jenkins UI
		- login to jenkins UI
			- **don't install any plugins**
	
		- initially login with the initialAdminPassword
			- `cat /var/lib/jenkins/secrets/initialAdminPassword`
		
		- #### Java Configuration: Jenkins UI
			- click on *Manage Jenkins* then *Global Tool Configuration*
		
			- click *Add JDK* and enter the details
				- for `JAVA_HOME` run `find / -name javac` on CLI
		
			- click *Apply*
	
	- ### Testing Jenkins Functionality
		- On Jenkins UI, click *New Item*
			- Enter a name, and select *Freestyle Project* then click *OK*
			- In the *General* tab of the job configuration, scroll down to the *Build* Section
				- select *execute shell* and write the following command: `echo "Jenkins installation verified"`
	
		- Go to the home page, and run this job
			- Console output should print the above command

	- ### Configure Maven Build Tool
		- Create a new directory for Maven and move into it
			- `mkdir /opt/maven`
			- `cd /opt/maven`
			
		- Get and install the Maven package
			- `wget https://mirrors.estointernet.in/apache/maven/maven-3/3.8.1/binaries/apache-maven-3.8.1-bin.tar.gz`
			- `tar -xvzf apache-maven-3.8.1-bin.tar.gz`
		
		- Move into the `apache-maven-3.8.1` directory and copy the path
			- `cd apache-maven-3.8.1`
			- `pwd`
				- Copy this path
		
		- Add the maven path to .bash_profile
			- `nano /root/.bash_profile`
			- Add the maven path, and save the file
		
		- Apply the changes
			- `source /root/.bash_profile`
			- If the changes aren't applied, logout and log back in

	- ### Configure Git
		- `apt-get -y install git`

	- ### Configure Maven in Jenkins UI
		- Open Jenkins UI and click *Manage Jenkins,* then *Manage Plugins*
		
		- Under *Available Plugins,* install without restart:
			- *Maven Integration Plugin*
			- *GitHub Plugin*
			- *Deploy to Container*
			- *Publish over SSH*
		
		- Navigate to *Manage Jenkins* then *Global Tool Configuration*
			- Add the Maven configuration, and save + apply
				- maven path: `/opt/maven/apache-maven-3.8.1`
				
			- Verify Git Installation, and save + apply 
				- Name: `default`
				- Path to Git Executable: `git`
	
	- ### Verify Jenkins, Git, and Maven Configuration
		- Create a new job; select *New Item*
			- Give the job a name, and **select Maven Project**
		
		- In the *General* tab
			- Give the project a description
		
		- In the *SCM* tab, select git and give a maven project's remote repository URL
		
		- *Build* Section
			- Give the root `pom.xml` location
			- *Goals and Options:* `install package`
			
		- Save then apply
		
		- Run the job, and verify the job was successful with its console output 

- ## 2nd EC2 Instance: Configure Webserver Environment

	- ### EC2 Instance setup, Tomcat Server Setup/Installation

		1. On AWS Management Console, go to EC2 and launch a *Red Hat Enterprise (RHEL) 7 (HVM)* AMI
	
		2. Click _Next: Configure Instance Details_
			- make sure _port 8090 **and** 8080_ are allowed on inbound security groups
	
		3. Click *Review and Launch*
	
		4. Create a new key-pair and save the public key to your local system
	
		5. Select the newly created instance in EC2 console and SSH to it
	
		6. After logging into this server, run these following commands:
			- become root user
				- `sudo su -`
			- update all packages on the server
				- `apt-get update -y`
			- install java
				- `apt-get -y install java-1.8`
			- check java default version
				- `java --version`
			- install wget
				- `apt-get -y install wget`
			- use wget to install Tomcat package
				- `wget https://mirrors.estointernet.in/apache/tomcat/tomcat-8/v8.5.65/bin/apache-tomcat-8.5.65.tar.gz`
				- `tar -xvzf apache-tomcat-8.5.65.tar.gz`
			- navigate to the newly created tomcat directory
				- `cd apache-tomcat-8.5.65`
				- `cd bin`
				- `chmod +x startup.sh`
				- `chmod +x shutdown.sh`
			- copy the command directory
				- `echo $PATH`
				- `ln -s /opt/apache-tomcat-8.5.65/bin/startup.sh /usr/local/bin/tomcatup`
				- `ln -s /opt/apache-tomcat-8.5.65/bin/shutdown.sh /usr/local/bin/tomcatdown`
				- `tomcatup`
				- `ps -ef | grep -i tomcat`
			- Search for connector port and change it to *8090* then save
				- `nano /opt/apache-tomcat-8.5.65/conf/server.xml`
				- `tomcatup`
				- `tomcatdown`
			- Tomcat server is now available at *(server-public-ip):8090*
				- `nano opt/apache-tomcat-8.5.65/webapps/host-manager/META-INF/context.xml`
				- `nano /opt/apache-tomcat-8.5.65/webapps/manager/META-INF/context.xml`
				- `tomcatdown`
				- `tomcatup`
			- Add some users and roels to login to tomcat server on the browser
				- `nano /opt/apache-tomcat-8.5.65/conf/tomcat-users.xml`
					- `<role rolename="manager-gui"/>`
					- `<role rolename="manager-script"/>`
					- `<role rolename="manager-jmx"/>`
					- `<role rolename="manager-status"/>`
					- `<user username="admin" password="admin" roles="manager-gui, manager-script,  manager-jmx, manager-status"/>`
					- `<user username="deployer" password="deployer" roles="manager-script"/>`
					- `<user username="tomcat" password="myPassword" roles="manager-gui"/>`
				- `tomcatdown`
				- `tomcatup`
			- Open your browser and browse to *(server-public-ip):8090* and click on *Manager App*
				- login with `myPassword` and `tomcat` user
				
		7. Access Jenkins UI on the **first EC2 instance created** 
			- Navigate to *Manage Jenkins*m, then *Manage Credentials*, then *Add Credentials*
			- Use the *deployer* username and password set up in step 6
				- Give this credential an ID, and a description for reference
	
	- ### Test Configuration in Jenkins (1st EC2 Instance)
		- Create a new job named *maven-project* and select *Maven Project* as the job type
		
		- *General* Section
			- Give this job a description 
		
		- *SCM* Section
			- Give a remote GitHub repo link for a Maven project
		
		- *Build* Section
			- In *Root POM,* specify the path to the application's `pom.xml`
			
			- In *Goals and Options,* specify `clean install package`
			
			- In *Post Steps,* add a post-build step and select *Deploy war/ear to a container*
			
		- *Post-build Actions* Section 
			- In the *Deploy war/ear to a container* section, under *WAR/EAR files* add `**/*.war`
				- Leave *Context Path* empty
			- In the *Containers* section, click *Add Container* and select *Tomcat 8.x Remote* 
				- In the newly created *Containers* sub-menu, add the *Deployer* credentials, and the public IP of the tomcat server on port 8090 as configured earlier
				
			- Save then apply
		
		- Build the project
			- On the tomcat server's CLI, the compiled *(webapp-name).war* will be found under `/opt/apache-tomcat-8.5.65/webapps`
				- To access the webapp itself, use the following URL
					- `http://<public-ip-tomcat-EC2-server>`
					
- ## 3rd EC2 Instance: Configure Ansible servers (Master/Slave Architecture)
> [!info] This server will be the master, and the tomcat server will be the slave node

	
  - ### Setting up the EC2 Instance
	  1. On AWS Management Console, go to EC2 and launch a *Red Hat Enterprise (RHEL) 7 (HVM)* AMI
	  
	  2. Click _Next: Configure Instance Details_
		  - Make sure port 22 (SSH) is allowed on inbound security group
	  
	  3. Click *Review and Launch*
	  
	  5. Create a new key-pair and save the public key to your local system
	  
	  6. Select the newly created server and SSH into it
	  
	  7. After logging in, run the following commands:
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
			
			- 


	

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