Created: 2023-02-16 17:41

___
# Tomcat Setup/Config on EC2
---
- ## 2nd of 3 EC2 Instances for automating CI: Configuring Webserver Environment 

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
			- Add some users and roles to login to tomcat server on the browser
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
				
		7. Access Jenkins UI on the [[EC2-jenkins-setup|first EC2 instance created]] 
			- Navigate to *Manage Jenkins*, then *Manage Credentials*, then *Add Credentials*
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

---
# References


## Tags
#tomcat 
#EC2 
#AWS 

---