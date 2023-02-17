Created: 2023-02-14 18:58
# Automating Continuous Integration Overview
---
> [!Tip] Architectural Diagram
> ![[Pasted image 20230214203132.png]]

## Agenda
- deploy 3 AWS EC2 instances
	- Jenkins
	- Ansible
	- Tomcat
- As soon as code is pushed to GitHub, a CI job will trigger an automated build using GitHub webhooks
	- Code is written in Java and compiled with Maven plugin
- Jenkins CI job will use the *Publish over SSH* plugin to intergrate with Ansible and Tomcat servers to automate builds
	- **use various git commands to test the CI functionality**


---

- [[implementation-of-automating-CI|Implementation with steps here]]



# References


## Tags
#ansible-configuration-management 
#continuous-integration

---