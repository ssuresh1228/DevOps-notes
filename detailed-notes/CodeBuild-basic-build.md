Created: 2023-03-06 18:18
# CodeBuild Basic Build
---
- Code is in version control (CodeCommit); now we move onto the next step in the CI/CD pipeline
	- Building and testing code (CodeBuild)

>[!Tip]+ CodeBuild and Docker
>- CodeBuild will launch Docker containers, provision them, then shut them down after building/testing the code
>- Serverless; just need to specify how we want the code to be built/tested 

## Creating CodeBuild project

>[!Example]+ Basic Project Configuration
>- ### Source Section
>	- Select code source provider, then reference type
>		- Branch, Git tag, or commit ID
>	- Select branch that contains code to build, and commit ID (optional)
>		- **Testing multiple branches requires multiple CodeBuild projects**
>		
>	>[!Info]+ CodeBuild Source Section Config:
>	>![[Pasted image 20230307135601.png]]
>	
>- ### Environment Section
>	- Environment Image
>		- Can use AWS CodeBuild managed image, or custom Docker image if the image has some specific software installed to build/test the code
>	- Service Role
>		- Allows CodeBuild to actually run
>	- Additional Config
>		- Can specify timeout & queued timeout
>			- Max = 8 hours, min = 5 mins
>		- Can specify VPC and setup environment variables
>	> [!info]+ Environment Section Config
>	> ![[Pasted image 20230307140343.png]]
>	
>- ### Buildspec section 
>	- CodeCommit repo already has a buildspec.yml file
>> [!info]+ Buildspec config
>> ![[Pasted image 20230307140537.png]]
>- ### Artifacts and Logs Section
>	- Leave Artifacts section default for now
>	- Can configure logs to output to S3
>		- Keeps logs altogether; if not enabled, we will lose the logs after the Docker container shuts down
>> [!info]+ Artifacts and Logs config
>> ![[Pasted image 20230307141915.png]]

## Starting the build
- Creates and provisions a Docker container
- CodeBuild will look for instructions in Buildspec.yml
>[!info]+ Full logs can be viewed in CloudWatch for debugging
>![[Pasted image 20230307142954.png]]

>[!tip]+ Build Succeeded; passes test suite in buildspec.yml:
>![[Pasted image 20230307143129.png]]
>- **The build succeeded, so now the Docker container is gone**
>	- Elastic component of CodeBuild; all resources are created in an elastic + serverless manner

## Key Points
- CodeBuild is serverless and resources are created/provisioned in an elastic manner. 
	- When a build is completed, the provisioned Docker container is gone; no longer paying for it and its associated compute resources

---
# References


## Tags
- #codebuild 
---