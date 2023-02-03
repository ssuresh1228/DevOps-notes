Created: 2023-01-31 17:57
# Configuration Management
- Enables users to manage/configure infrastructure and its environment
---
# Infrastructure as Code
- Enables automation of building/deploying/managing via code
> [!note]
> 2 approaches exist: 
> 
> 	1. Imperative: defines a series of steps for infra to reach desired result
> 	
> 	2. Declarative: "declares" desired outcome; doesn't outline steps needed to reach result 

___
# Ansible Overview
 - Deployment Automation tool
 - Default mode: push-based
 - Manages servers with a controller node
---
# Ansible Push Approach
- Ansible client nodes **do not** have agents installed
>[!NOTE]
Ansible's push based approach eliminates the need for polling with central servers

>[!TIP]
> Pull Architecture works in master-slave format; slaves have agents installed, and scales better than push architecture

---

# References
- [Edureka Ansible Presentation 1](https://learning.edureka.co/classroom/presentation/1483/12387/1479293?tab=CourseContent)

## Tags
#ansible-configuration-management