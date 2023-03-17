Created: 2023-03-16 18:33
# CodeDeploy: rollbacks
---
## Manual Rollbacks
- just deploy a previous application version 

## Automatic Rollbacks
- Access your CodeDeploy application, then click edit
	- Scroll down until advanced options, and click on *disable rollbacks*
>[!info]+ 2 options for automatic rollbacks exist:
>![[Pasted image 20230316184501.png]]

- ### Roll back when a deployment fails
	- if any deployment fails at any point in time on any instance, automatically roll back to the previous version
		- If deployment fails on 1st instance, deployment will stop altogether
		
- ### Roll back when alarm thresholds are met
	- Suppose deployment succeeded, and application was updated across all EC2 instances
		- We're tracking the instances, and notice that CPU utilization skyrockets
		- We need to roll back
	- Option for adding an alarm in advanced options exists, but we need to create the alarm itself in CloudWatch

#### Creating an alarm in CloudWatch
- Access CloudWatch console, then create an alarm
	- Select EC2 metrics, then per-instance metrics:
			- & Per-instance metrics available:![[Pasted image 20230316185153.png]]
		- Select CPU Utilization metric
>[!info]+ 4 steps to creating a CloudWatch alarm:
>>[!example]+ Step 1: Specify Metric and Conditions:
>>![[Pasted image 20230316185508.png]]
>
>>[!example]+ Step 2: Configure actions:
>>![[Pasted image 20230316185738.png]]
>
>>[!example]+ Step 3: Add name and description:
>>![[Pasted image 20230316185958.png]]
>
>>[!example]+ Step 4: Preview and create
>>

#### Return to CodeDeploy and add this alarm
>[!info]+ Added alarm to CodeDeploy deployment group:
>![[Pasted image 20230316190303.png]]

- If *roll back when alarm thresholds are met* is enabled, the deployment will stop then automatically roll back to last working version once this alarm is triggered

## Key points
- Alarms must be set up in CloudWatch based on some metric, then added manually to a deployment group's advanced options
	- Automatic roll back based on alarm threshold is based on this 

---
# References
- [[aws-codedeploy-docs#^a942f8|Redeploying and rollbacks in CodeDeploy]]

## Tags
- #AWS-DevOps/CodeDeploy/rollback
- #AWS-DevOps/CodeDeploy/redeployment
- #AWS-DevOps/CodeDeploy/alarm
- #AWS-DevOps/CloudWatch/CodeDeploy-EC2-alarm
---