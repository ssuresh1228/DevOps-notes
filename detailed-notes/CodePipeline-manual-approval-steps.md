Created: 2023-03-20 18:55
# CodePipeline: manual approval steps
---
## Add a new stage to deploy to production
- Edit the [[CodePipeline-CodeCommit-CodeDeploy#Step 4: Add Deploy Stage|existing pipeline's deploy stage]]
	- Add a new stage after dev deployment for deploying to production instances
		- Create additional EC2 instance(s) and configure the [[CodeDeploy-EC2-setup#EC2 Instance Tags|tags]] if needed to identify them as production instances
		- Create a [[CodeDeploy-application-deployment-groups#Step 2: Create a deployment group|new deployment group in CodeDeploy]] for production instance(s)
>[!info]+ production deployment stage:
>![[Pasted image 20230321145117.png]]
>> [!info]+ updated pipeline:
>> ![[Pasted image 20230321150805.png]]

## Configure a manual approval stage *before* deploying to production instance(s)
- As of now, after deployment to development instances succeeds, the pipeline will immediately deploy to the production instances
	- we want to configure a step for manual approval in order to deploy to production instances
	- This is a **sequential action**; manual approval comes before production deployment
>[!info]+ configuring manual approval:
>- add an action group *before* the prod-deployment action:
>![[Pasted image 20230321151147.png]]
>>[!info]+ updated pipeline:
>>![[Pasted image 20230321151215.png]] 
- ### Approval:
	- ![[Pasted image 20230321152114.png]]
	- ![[Pasted image 20230321152133.png]]
	- ![[Pasted image 20230321152158.png]]

---
# References

## Tags
- #AWS-DevOps/CodePipeline/manual-approval  
---