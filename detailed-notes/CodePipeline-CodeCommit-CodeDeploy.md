Created: 2023-03-20 15:10
# CodePipeline: CodeCommit & CodeDeploy
---
>[!Abstract] Goal: Automate transition from CodeCommit to CodeDeploy

- Access CodePipeline UI and create a new pipeline

## Step 1: Pipeline Settings
- give the pipeline a name
- CodePipeline will perform actions on our behalf, so it requires a service role
	- automatically generated
- Advanced settings:
	- Artifact Store: 2 options
		- Default location: create a default S3 bucket
			- **creates a new bucket for every pipeline**
			- may run into a s3 bucket limit if you create many pipelines with this option
		- Custom location: choose existing S3 bucket
			- use if you want a centralized location for all pipelines
	- Encryption Key
		- Default AWS Managed Key
			- let the AWS managed key encrypt all artifacts generated from CodePipeline
		- Customer Managed Key
			- We need to create a KMS key and use it here
>[!info]+ Pipeline Settings config:
>![[Pasted image 20230320152316.png]]

## Step 2: Add Source Stage
- What is going to trigger our source in CodePipeline?
	- Available options:
		- CodeCommit
		- ECR
		- S3
		- Bitbucket
		- GitHub(v1, v2)/GitHub enterprise server
- **Pipeline is triggered by a specific branch; we need to create a CodePipeline for *every* branch in a repository**
- Change detection options:
	- CloudWatch Events (recommended)
		- Whenever we commit to the specified repository, a CloudWatch event rule will be triggered
			- The trigger for this rule will be this pipeline
		- As soon as a change occurs in CodeCommit, then the pipeline will be triggered
	- AWS CodePipeline
		- Use CodePipeline itself to periodically check for changes 
		- Unlike the CloudWatch event rule option, *the pipeline isn't triggered immediately when changes are pushed to the repo* 
>[!info]+ Source Stage config:
>![[Pasted image 20230320153137.png]]
## Step 3: Add Build Stage (optional)
- skip for now
	- Can configure Jenkins or CodeBuild here
- [[CodePipeline-adding-CodeBuild|Build stage config here]]

## Step 4: Add Deploy Stage
>[!info]+ Config:
>![[Pasted image 20230320155342.png]]
>- For *deploy region*, we can choose to deploy in **another region**
>	- CodeDeploy application must be created in that respective region along with its respective deployment groups
>- If we have multiple CodeDeploy apps in multiple regions, we can use 1 central pipeline to trigger many CodeDeploys into multiple regions

## Completed pipeline
- As soon as the pipeline is created, the source gets triggered
	- last commit is pulled from the source, (CodeCommit in this case)
- Any change in the source will be automatically deployed to the development instances deployment group
- Any change made to the files and committed to the source will instantly be detected by a CloudWatch event, then deployed to the development instances 

## EventBridge rule
>[!info]+ Event Pattern
>![[Pasted image 20230320160755.png]]
>- any reference created/updated in the master branch of the CodeCommit repository (ARN) will trigger something on target(s)
>>[!info+] target:
>>![[Pasted image 20230320161006.png]] 

---
# References


## Tags
- #AWS-DevOps/CodePipeline/create-basic-pipeline  
- #AWS-DevOps/CodePipeline/EventBridge
- #AWS-DevOps/EventBridge/rules/CodePipeline  
---