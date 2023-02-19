Created: 2023-02-16 17:43

---
# Jenkins Setup & Configuration on EC2 (Maven & Git)
---

### EC2 instance setup, Jenkins Prerequisites + Installation
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

### Setup Jenkins UI
- login to jenkins UI
	- **don't install any plugins**
	
- initially login with the initialAdminPassword
	- `cat /var/lib/jenkins/secrets/initialAdminPassword`
		
- #### Java Configuration: Jenkins UI
	- click on *Manage Jenkins* then *Global Tool Configuration*
		
	- click *Add JDK* and enter the details
		- for `JAVA_HOME` run `find / -name javac` on CLI
		
	- click *Apply*


### Testing Jenkins Functionality
- On Jenkins UI, click *New Item*
	- Enter a name, and select *Freestyle Project* then click *OK*
		- In the *General* tab of the job configuration, scroll down to the *Build* Section
			- select *execute shell* and write the following command: `echo "Jenkins installation verified"`
	
	- Go to the home page, and run this job
		- Console output should print the above command

### Configure Maven Build Tool
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

### Configure Git
- `apt-get -y install git`

### Configure Maven in Jenkins UI
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
	
### Verify Jenkins, Git, and Maven Configuration
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



---


# References


## Tags
#EC2 
#jenkins 
#AWS 
#maven 

---