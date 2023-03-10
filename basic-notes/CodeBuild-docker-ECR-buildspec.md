Created: 2023-03-07 18:30
# CodeBuild: Docker, ECR, and buildspec samples
---
- more examples of buildspec files are located [here](https://docs.aws.amazon.com/codebuild/latest/userguide/use-case-based-samples.html)
- CodeBuild [Docker sample](https://docs.aws.amazon.com/codebuild/latest/userguide/sample-docker.html) 
	- outlines how to use CodeBuild to build a Docker image, then push that image to Elastic Container Registry (ECR) image repository
	- Verify whether the service role attached to CodeBuild has the permissions to access ECR
		- Access IAM Console, then click on *Roles*, then find the role created for CodeBuild.
		- Attach a policy for ECR if not configured
			- **Better for login related things to fail early; ALWAYS place these commands in the `pre_build` phase!**
	- The docker image created here must be pushed somewhere, otherwise it will be lost
		- images are destroyed after building
---
# References
- [CodeBuild use case based samples](https://docs.aws.amazon.com/codebuild/latest/userguide/use-case-based-samples.html)
- [[demo-CodeBuild-Docker-ECR|Implementation here]]

## Tags
- #docker
- #AWS-DevOps/ECR/codebuild-image
- #AWS-DevOps/codebuild/buildspec   
---