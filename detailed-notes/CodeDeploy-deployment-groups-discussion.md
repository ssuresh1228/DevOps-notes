Created: 2023-03-13 18:21
# CodeDeploy: deployment groups discussion
---
- To automate CodeDeploy agent installation on EC2 instances, add [[CodeDeploy-EC2-setup#Install CodeDeploy agent on EC2 instance|this]] to the *user data* section under *advanced details* when setting up the EC2 instances
	- Launch more EC2 instances like the one [[CodeDeploy-EC2-setup#Create the EC2 instance|configured here]], and add tags for environment and name for every instance
		- environment: production
		- name: webserver
- Return to CodeDeploy, then the application
	- Create a new deployment group
	- follow the same [[CodeDeploy-application-deployment-groups#Step 2: Create a deployment group|steps for configuring a deployment group]], but change *Environment Configuration* section's *tag group* to match the environment and name tags configured above

>[!tip]+ Key point:
>Use tags to separate/classify your EC2 instances into deployment groups. This is how we create different environments for deployment (dev, test, prod, etc.)
>

---
# References


## Tags
- #AWS-DevOps/CodeDeploy/groups
- #AWS-DevOps/CodeDeploy/deployment 
- #AWS-DevOps/CodeDeploy/EC2
- #AWS-DevOps/EC2/tags
---