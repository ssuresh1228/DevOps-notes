Created: 2023-03-16 14:40
# CodeDeploy: hooks and environment variables
---
## Hooks 
- Hooks section varies on deployment environment; changes based on deployments to
	- ECS
	- Lambda
	- EC2/on-premises
	
 >[!info] So far, only EC2 deployment (no load balancer) has been covered

- Enabling load balancer enables the use of the following event hooks:
	- `BeforeBlockTraffic`
	- `BlockTraffic`
	- `AfterBlockTraffic`
	- `BeforeAllowTraffic`
	- `AllowTraffic`
	- `AfterAllowTraffic`

>[!tip]+ Lifecycle event hook availability based on deployment type:
>![[Pasted image 20230316145521.png]]
>>[!example]+ event hook run order: in-place deployment:
>>![[lifecycle-event-order-in-place.png]]
>>- **blue blocks are accessible for creation in appspec.yml**

- Not necessary to remember all these hooks; just know
	- Some hooks are available, some aren't
	- Certain hooks are only available when using a load balancer
	- Remember the general order
		- Stop application
		- download bundle
		- do something before installing (like installing dependencies)
		- install something
		- after install, do something
		- start the application
		- validate service (make sure everything is fine)

## Environment variable availabity for hooks
- Every time a deployment is done, some environment variables are available for use in hooks:
>[!info]+ Environment variables in hooks:
>- `APPLICATION_NAME`
>	- application name in CodeDeploy
>- `DEPLOYMENT_ID`
>	- Unique ID for the current deployment
>- `DEPLOYMENT_GROUP_NAME`
>	- Instances are aware of which group name they're part of
>- `DEPLOYMENT_GROUP_ID`
>	- Unique ID of current deployment group
>- `LIFECYCLE_EVENT`
>	- name of current lifecycle event (eg `AfterInstall`)
- We can use these 5 environment variables to customize deployments
	- For the *development* `DEPLOYMENT_GROUP_NAME`, we want to do something, and for the *production* `DEPLOYMENT_GROUP_NAME`, we want to do something else 
		- **So instead of having multiple appspec.yml files, we can use an if-statement in our scripts that checks whether or not the `DEPLOYMENT_GROUP_NAME` is *development* or *production* then customize what to do for each**

## Key Points
- All we really need to do is create a CodeDeploy application and deployment groups, then use the hooks and environment variables available to customize the deployments in **one appspec.yml file**  

---
# References
- [[aws-codedeploy-docs#^7dcfbf|CodeDeploy docs: appspec hooks section]]
- [[aws-codedeploy-docs#^8d4231|CodeDeploy docs: environment variable availability for hooks]]

## Tags
- #AWS-DevOps/CodeDeploy/appspec/hooks
- #AWS-DevOps/CodeDeploy/appspec/environment-variables
---