# Demo: Ad-hoc Commands
Created: 2023-02-02 14:36

# Adding a user to a host
-  `ansible -b -K -m user -a 'name=<username>' <hostname or groupname>`
>[!example]
>![[Pasted image 20230202143810.png]]

---
# Starting a service on a host
- `ansible -m service -a ‘name=<serviceName> state=<requiredState>’ <hosts>`
>[!example]
>![[Pasted image 20230202144225.png]]

---
# Checking host facts
- `ansible -m setup <hostNames or groupNames>`
>[!example]
>![[Pasted image 20230202144422.png]]

---
# References
- [[pres-ansible-architecture#Ad-Hoc Commands|ad-hoc commands]]

## Tags
- #ansible 
- #adhoc-commands 
- #configuration-management 
---