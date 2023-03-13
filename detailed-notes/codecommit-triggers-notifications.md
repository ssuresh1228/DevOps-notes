Created: 2023-02-24 15:42
# CodeCommit: Triggers and Notifications
---
## Notification Rule
### Create Notification Rules
- Access your [[CodeCommit-first-repo-https-config|CodeCommit repo]], then click on the *Source* tab, then *Settings*, then *Notifications.* 
	- & Notifications tab on repository![[Pasted image 20230301163014.png]]
#### Configure your *Events that trigger notifications* as needed
>[!note]+ Configured trigger notifications:
> ![[Pasted image 20230301165831.png]]

#### Targets section
> [!Note]+ Targets Section
> ![[Pasted image 20230301170655.png]]
>>[!info]+ Creating a new target:
>>- ![[Pasted image 20230301171459.png]]
>>- ![[Pasted image 20230301171526.png]] 


### Configured Notification Rule
>[!Example]+ Notification rule has been created: 
>![[Pasted image 20230301171638.png]]
> - this notification belongs to CodeCommit service, all notification rules can be accessed by clicking on *Settings*, then *Notification rules* on the left menu



---

## Triggers
### Creating a trigger on CodeCommit repo
>[!Note]+ Accessing *triggers* section:
>![[Pasted image 20230301172045.png]]
> - In the lefthand menu, click on *Source*, then *Repositories*, then your configured repository, then its *Settings* tab as shown highlighted

>[!Example]+ Creating a trigger:
>- ![[Pasted image 20230301181408.png]]
>	- Select the SNS topic configured in the notification rule section

## Notifications vs. Triggers
- Don't need to know the exact differences b/w notifications and triggers
	- CodeCommit has a facility with notification rules and triggers to invoke a SNS topic/lambda function which can be used to create many different types of automation into workflows
		- Eg. Having CodeCommit trigger a Lambda function

## CloudWatch
- Centerpiece of all DevOps automation
>[!info]+ Click on *Events*, then *Rules*
>![[Pasted image 20230301184413.png]]
>>[!note]+ The notification rule created earlier is present
>>![[Pasted image 20230301184552.png]]
>>>[!note]+ Clicking on the rule gives us this:
>>>![[Pasted image 20230301184630.png]]
>>>This CloudWatch rule allows the CodeCommit notification rule configured above to actually work

### Creating a new rule in CloudWatch
- Click on *Rules* then *Create rule*
>[!Example] CloudWatch rule config
>![[Pasted image 20230301185819.png]]
>- Targets can be virtually *anything,* including CodeBuild projects
By creating notification rules/triggers  

## The Big Picture
- By creating notification rules/triggers in your CodeCommit repos, we can automate whatever's happening in the repository straight into an automation platform
	- Eg. SNS, SQS, Lambda, etc
- From CodeCommit, we can set up notifications, triggers, CloudWatch events/rules to build automation directly into SNS and Lambda
- **The exam will be more focused on this, not the minute differences between notifications and triggers**

___
# References
- [AWS docs: creating a notification rule](https://docs.aws.amazon.com/dtconsole/latest/userguide/notification-rule-create.html?icmpid=docs_acn_console)
- [AWS docs: understanding notification contents/security](https://docs.aws.amazon.com/dtconsole/latest/userguide/security.html#security-notifications)

## Tags
- #AWS-DevOps/CloudWatch/triggers-notifs 
- #AWS-DevOps/CodeCommit/cloudwatch-triggers-notifs 
---