Created: 2023-03-18 17:26
# CodeDeploy: deploying to lambda
---
- Create a new application in CodeDeploy
	- Create a new Service Role in IAM for CodeDeploy to use Lambda
## Deployment settings:
- The way CodeDeploy with Lambda works is that there's an existing version, and then a new version is deployed
- We have the option of specifying how to *shift traffic from the old version to the new version* 
	- **All At Once**: all traffic immediately shifts from old to new version once deployment of new lambda function is completed
	
	- **Linear**: Traffic shifts in equal increments at a specified number of mins between each increment
		- Can specify percentage of traffic to shift in each increment and time (mins) between each increment	
		
	- **Canary**: Traffic is shifted in 2 increments; 
		- *both lambda functions versions coexist for 1 increment*
		- Can specify percentage of traffic to shift to updated lambda function in the first increment
		- Can specify number of mins before remaining traffic (on older lambda function) is shifted to the new lambda function in the 2nd increment
	- **Linear vs. Canary**
		- Linear is gradual; step by step
			- *Use when you want to gradually shift traffic in equal increments*
		- Canary is one, then all; 
			- some traffic goes to the new lambda function, then *all* remaining traffic on old function shifts to the new one 
			- *Use when you need to shift traffic in 2 increments* 

## Appspec for Lambda functions
- Much simpler to use
- Lifecycle event hooks:
	- `BeforeAllowTraffic`
		- used to run tasks *before* traffic is shifted to the new (deployed) lambda function version
	- `AfterAllowTraffic`
		- used to run tasks *after* traffic is shifted to the new (deployed) lambda function version
- Hook run order in Lambda function version deployment
	1. Start
	2. `BeforeAllowTraffic` (available for use)
		- can run another lambda function here (eg. to see if everything is fine before traffic is allowed) 
	3. `AllowTraffic` (not available)
	4. `AfterAllowTraffic` (available for use)
		- can run another lambda function here (eg. to test if everything is working after traffic has been allowed) 
	5. End

>[!Example]+ Since all these run in lambda, we have to specify lambda functions for the 2 available hooks:
>![[Pasted image 20230320143213.png]]
>- This is all there really is in an appspec.yml for lambda deployment

### Possible use cases
- BeforeAllowTraffic
	- make sure database connectivity is working, migration is complete, etc
- AfterAllowTraffic
	- What should we do after the function has started (traffic is passing through)
	- How do we verify that everything is working properly?
	- health checks and monitoring

## Key Points
- We have 3 available deployment types:
	- All at once
		- shifts all traffic from old lambda function to new one immediately once new version's deployment is completed
	- Linear
		- Used when we want to gradually shift traffic in increments
		- can specify percentage of traffic to shift per increment, and time (in mins) between each increment 
	- Canary
		- used when we need to shift traffic in 2 increments
		- both new and old versions exist for the 1st increment
		- Increment 1
			- specify percentage of traffic to shift to new lambda function
		- increment 2
			- specify number of mins before all traffic on older version is shifted to new version
- Appspec.yml 
	- We only have 2 hooks available for use to invoke other lambda functions
		- `BeforeAllowTraffic`
			- perform checks/setup before traffic is allowed
		- `AfterAllowTraffic`
			- use for running health checks/monitoring after traffic is allowed 
---
# References
- [Deploying updated Lambda function with CodeDeploy (SAM - serverless application model)](https://docs.aws.amazon.com/codedeploy/latest/userguide/tutorial-lambda-sam.html)

## Tags
- #AWS-DevOps/CodeDeploy/lambda-deployment
- #AWS-DevOps/lambda/CodeDeploy
- #AWS-DevOps/CodeDeploy/lambda-appspec
---