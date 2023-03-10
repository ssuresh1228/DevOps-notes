Created: 2023-03-09 13:49
# CodeBuild: CloudWatch logs, metrics, and triggers
---
## Logs
- when [[CodeBuild-basic-build#Starting the build|Configuring the build job]], CloudWatch logs were enabled, and the option to upload logs to S3 was also available (not enabled)
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
>>- Alarm when failed builds crosses a certain number
>>- Alarm for when build duration average suddenly spikes
>>- Alarm for when too many builds are occurring; might be a bug or configuration error



---
# References


## Tags
- #AWS-DevOps/cloudwatch/cloudwatch-events

---