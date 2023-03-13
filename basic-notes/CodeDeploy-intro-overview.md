Created: 2023-03-13 13:45
# CodeDeploy: Intro & Overview
---
## CodeDeploy Function
- We want to deploy an application automatically to multiple EC2 instances
	- Deployments can be handled through Ansible, Terraform, Chef, Puppet, etc.
- AWS CodeDeploy handles this 

## How it works
- Each EC2/on-premise machine must be running a CodeDeploy agent
	- Agent on each machine will continuously poll CodeDeploy for work to do
- CodeDeploy sends an `appspec.yml` file to the instances
- Application will be pulled from S3/GitHub/CodeCommit
- EC2/on-premise server(s) will run the deployment instructions in the `appspec.yml` file
- CodeDeploy agent in each instance will report on success/failure of the deployment
>[!info]+ Overview diagram:
>![[Pasted image 20230313135840.png]]

## Advantages
- Can create and group EC2 instances based on deployment environment
	- dev, test, prod groups
- Very flexible for defining deployment types
	- Can even define subgroups 
- Can be chained into CodePipeline and use artifacts from there
- Can reuse existing setup tools, works with any application, and has auto-scaling integration
- Supports Lambda deployments, and EC2/ECS
- **Does not provision resources**
	- must provision instances in advance, then CodeDeploy will manage deployments on these instances

>[!tip] Blue-Green deployment **only** works on EC2 instances; can't create on-demand instances on premises



---
# References


## Tags
- #AWS-DevOps/CodeDeploy/overview 
---