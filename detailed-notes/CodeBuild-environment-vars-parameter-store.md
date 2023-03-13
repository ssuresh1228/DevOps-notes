Created: 2023-03-08 14:36
# CodeBuild: Environment Variables & Parameter Store
---
## Drawbacks of using environment variables directly
- Can define environment variables in the buildspec file itself, or override them in the CodeBuild console as shown [[demo-CodeBuild-Docker-ECR#Environment Variable setup in CodeBuild project|here]], but it leaves these variables exposed
	- This is fine for variables such as DB_URL, but we don't want to add things like DB_PASSWORD as plaintext.
>[!note]+ Example environment variables in CodeBuild console:
>![[Pasted image 20230308151650.png]]

## Enter AWS SSM: Systems Manager Parameter Store
- Used for storing secrets and configuration data management 
>[!tip]+ We can create a parameter directly in the CodeBuild console:
>![[Pasted image 20230308151937.png]]

### Creating a new parameter in SSM's UI: 
- Access *Parameter Store* on the left-side menu on SSM UI
	- Click on *Create Parameter*
>[!info]+ Example parameter configuration:
>![[Pasted image 20230308153202.png]]
>- CodeBuild can retrieve this parameter directly for its build project at runtime:
>>[!note]+ updated CodeBuild Environment Variables Override:
>>![[Pasted image 20230308153350.png]]
>>When a build is run, CodeBuild will access SSM and retrieve this parameter, but IAM permissions for SSM are not yet configured for CodeBuild

### Adding SSM Policy for CodeBuild in IAM:
>[!note] Access IAM Console, then the CodeBuild role
>- Attach the following policy; read-only is enough to provide access to the parameters
> ![[Pasted image 20230308153816.png]]

## Key Points
- Environment variables are plaintext
- Using Parameter Store is the secure way to provide CodeBuild projects with access to sensitive environment variables 
- Both the plaintext environment variables and the parameter_store variables will be accessed at CodeBuild project's runtime by the buildspec.yml for use
- ---
# References
- [[aws-codebuild-docs#^e0a0d1|Environment variables reference]]

## Tags
- #AWS-DevOps/CodeBuild/environment-variables
- #AWS-DevOps/SSM/parameter-store
---