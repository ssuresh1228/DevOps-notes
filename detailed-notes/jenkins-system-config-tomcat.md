Created: 2023-02-17 19:01
# Jenkins System Config: Tomcat Server
---
- ## On the [[EC2-jenkins-setup|Jenkins UI]], add the [[EC2-tomcat-setup|tomcat server]]
	- Navigate to *Manage Jenkins*, then *Configure System*
	- Scroll down until the *SSH Servers* section, and add the following details of the ansible server configured during setup:
		- `Name: tomcat-server`
		- `Hostname: <server's-private-ip>`
		- `username: tomcat`
		- `Password: myPassword`

---
# References
- [[EC2-tomcat-setup|EC2 tomcat setup/config]]

## Tags
- #jenkins 
- #tomcat 
---