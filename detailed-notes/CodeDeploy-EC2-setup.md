Created: 2023-03-13 14:06
# CodeDeploy: EC2 Setup
---
## Create the EC2 instance
- Amazon Linux 2 AMI
- IAM Role
	- Create a new role for EC2 to call AWS services (S3 or CodeCommit in this case)
>[!info] IAM Service Role for EC2
>- ![[Pasted image 20230313152426.png]]
>- ![[Pasted image 20230313152615.png]]
>- ![[Pasted image 20230313152705.png]]

- Apply this newly created role to EC2 config
- Create new key-pair if one doesn't exist, then connect to the EC2 instance
>[!tip] Use EC2 Instance Connect to SSH via browser:
>![[Pasted image 20230313153402.png]]


## Install CodeDeploy agent on EC2 instance
>[!example] Commands to install CodeDeploy agent:
> ```
> sudo yum update
> sudo yum install -y ruby wget
> wget https://aws-codedeploy-eu-west-1.s3.eu-west-1.amazonaws.com/latest/install
> chmod +x ./install
> sudo ./install auto
> sudo service codedeploy-agent status

## EC2 Instance Tags
>[!info] CodeDeploy uses these tags to determine which deployment groups to deploy applications on:
>![[Pasted image 20230313154853.png]]


---
# References
- [Getting Started with CodeDeploy](https://docs.aws.amazon.com/codedeploy/latest/userguide/getting-started-codedeploy.html)

## Tags
- #AWS-DevOps/CodeDeploy/setup 
---