Created: 2023-03-06 17:45
# CodeBuild Overview
---
- ## General Overview
	- Fully managed build service
	- Alternative to other build tools like Jenkins
	- Continuous scaling
		- No servers to manage/provision means no build queue
	- Pay only for usage; amount of time it takes to complete a build
	- Uses Docker under the hood for reproducible builds
		- Can extend capabilities using our own base Docker images
	- Very secure
		- Integration with KMS for encryption of build artifacts
		- IAM for build permissions
		- VPC for network security
		- CloudTrail for API call logging
- ## How it's used in practice
	- Get source code
		- GitHub, CodeCommit, CodePipeline, S3, etc
	- Build instructions are defined in code
		- `buildspec.yml` file defines build instructions
	- Logs can be outputted to S3 or CloudWatch
	- Build metrics can be monitored via CloudWatch
	- Use CloudWatch Events to detect failed builds and trigger notifications
		- Use CloudWatch Alarms to notify if thresholds for failures are needed
	- CloudWatch Events and Lambda can be used as "glue" 
	- CodeBuild can send notifications though SNS using triggers


---
# References


## Tags
---