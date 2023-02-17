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