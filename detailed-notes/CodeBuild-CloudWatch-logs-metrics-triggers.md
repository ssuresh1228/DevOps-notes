Created: 2023-03-09 13:49
# CodeBuild: CloudWatch logs, metrics, and triggers
---
## Logs
- when [[CodeBuild-basic-build#Starting the build|Configuring the build job]], CloudWatch logs were enabled, and the option to upload logs to S3 was also available (not enabled)
- When CodeBuild finishes its build job, the underlying Docker container it uses is destroyed; only trace remaining is in CloudWatch/S3 logs 
>[!Info]+ Accessing CloudWatch Logs:
>![[Pasted image 20230309161508.png]]
>- *Every* time a build is run, a new log stream is created with a build ID

## Metrics
>[!Info]+ Cloudwatch automatic dashboard for CodeBuild:
>![[Pasted image 20230309162610.png]]
>- main categories:
>	- Succeeded builds
>	- Failed builds
>	- Builds (total number of builds)
>	- Build duration
>- Can create alarms on any of these parameters:
>>[!example]+ Sample alarms
>>- number failed builds crosses a certain number
>>- build duration average suddenly spikes
>>- when too many builds are occurring; might be a bug or configuration error

## Events
- EventBridge can connect with many other AWS services to set up many different types of automation and integration
	
### Scheduling builds using EventBridge rules
- CloudWatch events was replaced with EventBridge:
>[!Example]+ Scheduling CodeBuild project with EventBridge rule:
>>[!info]+ Step 1: Define rule detail:
>>![[Pasted image 20230309183258.png]]
>
>>[!info]+ Step 2: Define schedule:
>>![[Pasted image 20230309183339.png]]
>>>[!tip]+ Event patterns can also be used to specify event types:
>>>![[Pasted image 20230309190832.png]]
>
>
>>[!info]+ Step 3: Select target(s):
>>![[Pasted image 20230309185612.png]]
>>- An execution role hasn't been set up for EventBridge; it must be created as shown here
>
>>[!info]+ Step 4: Configure tags - *optional*
>>![[Pasted image 20230309190038.png]]
>
>>[!tip]+ Created EventBridge rule:
>>![[Pasted image 20230309190456.png]]


---
# References
- [CodeBuild resources/operations doc: Project ARN](https://docs.aws.amazon.com/codebuild/latest/userguide/auth-and-access-control-iam-access-control-identity-based.html#arn-formats)

## Tags
- #AWS-DevOps/cloudwatch/cloudwatch-events
- #AWS-DevOps/cloudwatch/metrics
- #AWS-DevOps/cloudwatch/triggers
- #AWS-DevOps/codebuild/cloudwatch-integration
- #AWS-DevOps/eventbridge/rules
---