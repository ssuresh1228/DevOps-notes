Created: 2023-03-20 17:42
# CodePipeline: Artifacts, S3, and encryption
---
- in the pipeline creation, we had to [[CodePipeline-CodeCommit-CodeDeploy#Step 1: Pipeline Settings|choose where to store artifacts, and select encryption key type]] 
	- create a default S3 bucket, or choose an existing S3 location (same region and account as pipeline)
	- Encryption key:
		- Default AWS managed key
			- sets up a AWS KMS (Key Management Service) encryption key for us
		- Customer managed key
			- we have to manually create our own KMS key and apply it 
- ***Every* stage of the pipeline creates artifacts, which are then stored in the specified S3 location and passed on to the next stage of the pipeline**
	- Artifacts are the method in which CodePipeline's stages communicate between each other 
	- **S3 is the backbone of CodePipeline**
	- In the [[CodePipeline-CodeCommit-CodeDeploy#Step 4: Add Deploy Stage|deploy stage]], we can add a parallel action to upload to another S3 bucket
		- Make sure another S3 bucket exists
			- ![[Pasted image 20230320184331.png]]
- CodeBuild itself also generates its own artifacts, as shown in its buildspec.yml
	- ![[Pasted image 20230320185233.png]]
	- The artifacts generated here are *different* than the artifacts generated in CodePipeline
		- These artifacts generated in CodeBuild are more or less reused for CodePipeline's purposes
 

---
# References


## Tags
- #AWS-DevOps/CodePipeline/S3-artifacts  
---