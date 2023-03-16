Created: 2023-03-13 19:29
# CodeDeploy: deployment configurations
---
- access the [[CodeDeploy-application-deployment-groups#Step 3: Create Deployment|deployment]] created earlier, then click on *edit deployment*
- **in-place deployment was used in this example**
	- servers go down to be updated, then come back online when updated with latest application version
	- We can define *how* we want these servers to go offline to recieve the application update:
		- one at a time
		- half at a time
		- all at once

>[!info]+ 3 predefined deployment types exist:
>![[Pasted image 20230313194009.png]] 
> - these specify *how many* servers you want to go down at a time to recieve an application update

>[!tip]+ Custom deployment configurations can also be created:
>![[Pasted image 20230313194230.png]]
>- can define a percentage/number of EC2 instances that must be up during a (in-place) deployment

- **When dealing with blue-green deployment, we need EC2 auto scaling grops for the sake of automation and the load balancer enabled**
	- The only other option is to manually provision more EC2 instances (painful)

---
# References
- [[CodeDeploy-application-deployment-groups|Creating a CodeDeploy app, deploy groups, then deploying onto EC2 instance(s)]]

## Tags
- #AWS-DevOps/CodeDeploy/deployment/configuration
- #AWS-DevOps/CodeDeploy/deployment/deployment-groups
---