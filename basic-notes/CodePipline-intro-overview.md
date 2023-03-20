Created: 2023-03-20 14:52
# CodePipline: overview
---
## Overview
- Continuous delivery tool
- visual workflow
	- visually orchestrate pipelines 
- can define multiple code sources
	- GitHub, CodeCommit, S3, etc
- can build using CodeBuild, Jenkins, etc
- Can load test using 3rd party tools 
- deploy using CodeDeploy, Elastic Beanstalk, CloudFormation, ECS, etc
- Made of stages
	- Each stage can have sequential and/or parallel actions
		- Build, Test, Deploy, Load Test, etc
	- manual approval can be defined at *any* stage
- Meant to orchestrate the entire CICD pipeline:
![[Pasted image 20230320145552.png]]

## Artifacts
- each pipeline stage can create artifacts
	- passed and stored to S3, then passed on to the next stage in the pipeline
![[Pasted image 20230320145750.png]]

---
# References


## Tags
- #AWS-DevOps/CodePipeline/overview 

---