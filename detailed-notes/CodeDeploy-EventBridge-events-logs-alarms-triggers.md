Created: 2023-03-16 16:43
# CodeDeploy: EventBridge events, logs, alarms, and triggers
---
## EventBridge Events
### 1. Access EventBridge console
### 2. Create a new rule
>[!info] Creating a new rule requires:
>1. Define rule detail
>2. Build event pattern
>3. Select target(s)
>4. Configure tags (optional)
>5. Review and create

#### Define rule detail
>[!example]+ Defining rule detail:
>![[Pasted image 20230316180723.png]] 

#### Build event pattern
>[!example]+ Define event source, sample event, creation method, then event pattern:
>>[!info]+ Event source
>>![[Pasted image 20230316180938.png]]
>
>>[!info]+ Sample event (optional)
>>![[Pasted image 20230316181635.png]]
>
>>[!info]+ Creation Method + Event Pattern:
>>**Event pattern will vary based on use case and target**
>>![[Pasted image 20230316181701.png]]

#### Targets
- this depends on your use case
	- Lambda function to pass Slack notification whenever deployments fail
	- Push deployment data to kinesis stream for real-time monitoring
	- CloudWatch alarm to automatically stop/terminate/reboot/recover EC2 instance when a deployment or instance event fails
		- Event pattern will vary depending on use case

## Viewing CodeDeploy Logs in CloudWatch 
- Requires CodeDeploy and CloudWatch agents to be installed on the EC2 instance(s)
	- There's not a direct integration between CloudWatch logs and CodeDeploy
## Triggers and SNS Notifications
- Select a deployment group on CodeDeploy then edit
- Scroll down to advanced options
- & Creating a deployment trigger:![[Pasted image 20230316183006.png]]![[Pasted image 20230316183022.png]]
- The target is a SNS topic

## Key points
- CodeDeploy can integrate with EventBridge events across many different targets (services)
- CodeDeploy has built-in triggers that directly send messages through SNS

---
# References
- [[aws-codedeploy-docs#^176182|Monitoring deployments with CloudWatch events]]
- [[aws-codedeploy-docs#^533cbd|CodeDeploy logs in CloudWatch console]]
- [[aws-codedeploy-docs#^33a05d|Monitoring deployments with SNS event notifications]]

## Tags
- #AWS-DevOps/CodeDeploy/logs
- #AWS-DevOps/EventBridge/CodeDeploy
- #AWS-DevOps/EventBridge/integration 
---