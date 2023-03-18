Created: 2023-03-16 19:08
# CodeDeploy: on-premises setup
---
>[!important]+ Deploying a CodeDeploy application to an on-premises instance has 2 major steps:
>1. Configure each on-premises instance, register it with CodeDeploy, and tag it (deployment-group)
>	- **Tagging on-premises instances is only available with CodeDeploy**
>2. Deploy application revisions to the on-premises instance

## Registering an on-premises instance with CodeDeploy
- There are 3 methods of doing this:
	- Use an **IAM user** ARN to authenticate requests *(create a new IAM user per instance)*
		- use the `register` command for a more or less automated registration process
			- best for registering a single instance
		- use `register-on-premises-instance` command to manually configure most registration options
			- best for registering a small amount of instances at a time
			
	- Use an **IAM role** ARN to authenticate requests:
		- use `register-on-premises-instance` command and refresh temp credentials periodically via AWS STS (Security Token Service) to manually configure registration options
			- best for registering many instances at once
			- most secure option
			
- Once the instances are registered, they must be tagged in CodeDeploy console or AWS CLI in order for deployment groups to work correctly
	- Eg) key:value
		- `Name: on-premises`
		- `Environment: development`
		
## Key points
- In order to register an on-premises instance for use with CodeDeploy:
	- Set up a CodeDeploy agent on that instance to use a specific IAM user (for small number of instances; doesn't scale very well)
	- Then we register the instances, then tag them appropriately for use with CodeDeploy's deployment groups

---
# References
- [[aws-codedeploy-docs#^5bdd78|Working with on-premises instances for CodeDeploy]]
- [[aws-codedeploy-docs#^aa9e7f|register-on-premises-instance command: IAM user ARN]]
- [[aws-codedeploy-docs#^954070|register-on-premises-instance command: IAM session ARN]]

## Tags
- #AWS-DevOps/CodeDeploy/on-premise-instances

---