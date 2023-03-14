Created: 2023-03-13 15:56
# CodeDeploy: Application, Deployment Groups, & Deployment
---

## Step 1: Create an application
- Select *EC2/On-premises* compute type for now

## Step 2: Create a deployment group
- represents a set of EC2 instances in this case
- Create a new service role for CodeDeploy to access these EC2 servers:
	- CodeDeploy use case
		- ECS and Lambda have their own roles and must be created separately
	- Add AWSCodeDeployRole permission 
- Enter this service role on the CodeDeploy Config Page
- Select *In-place* for deployment type
- Select *Amazon EC2 Instances* for environment configuration
	- Add the tags created earlier in the [[CodeDeploy-EC2-setup#EC2 Instance Tags|EC2 setup]]
	- *Disable load balancing for now*; hasn't been configured on EC2 instance
>[!Info]+ Deployment group Configuration:
>>[!Tip]+ Application, Deployment Group Name, and Deployment Type
>>![[Pasted image 20230313164246.png]]
>
>>[!tip]+ Environment/agent config, and deployment settings:
>>![[Pasted image 20230313164402.png]]
>>![[Pasted image 20230313164432.png]]

## Step 3: Create Deployment
>[!info]+ Completed Deployment Group:
>![[Pasted image 20230313164707.png]]
- Select the deployment group configured earlier
- Revision type: Select S3 bucket; we need to upload the application to S3 now, then return here and paste the revision location
### Create and upload app to S3 bucket:
>[!tip]+ Configuring a profile in AWS CLI:
>- In IAM, create a user or select an existing user
>	- Generate new access key, and save both access and secret
>- In AWS CLI, run the following command:
>	- `aws configure --profile <profile name>`
>	- enter the access & secret keys
>	- configure other details (region, output format, etc.) as needed


>[!Example] Creating the bucket and enabling versioning in CLI:
>```
>aws s3 mb s3://my-devops-course-bucket --region us-west-1 --profile DevOps
>
> aws s3api put-bucket-versioning --bucket my-devops-course-bucket --versioning-configuration Status=Enabled --region us-west-1 --profile DevOps
>```
 

>[!Example]+ Deploying app files into the S3 bucket:
>`aws deploy push --application-name DevOps-demo-application --s3-location s3://my-devops-course-bucket/codedeploy-demo/app.zip --ignore-hidden-files --region us-west-1 --profile DevOps`
>- application name is what was configured in CodeDeploy's *Create Deployment* section
>- command must be run in project's directory; appspec.yml is necessary 
>	- This will zip all files and upload to the S3 bucket
 
### Return to CodeDeploy *Create Deployment* Configuration:
>[!info]+ in *revision location*, select the S3 bucket in the menu:
>![[Pasted image 20230313175615.png]]
- Don't override anything for now, and create the application

- In the EC2 console, add a new inbound rule for HTTP traffic (port 80)
	- Access the application by copy/pasting the instance's public IPv4 DNS
---
# References
- [[aws-cli-docs|AWS CLI Configuration docs]]

## Tags
- #AWS-DevOps/CodeDeploy/groups
- #AWS-DevOps/CodeDeploy/deployment
- #AWS-DevOps/CLI/S3
- #AWS-DevOps/S3/CLI-commands  
---