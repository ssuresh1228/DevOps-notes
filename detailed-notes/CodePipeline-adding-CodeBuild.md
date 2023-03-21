Created: 2023-03-20 16:12
# CodePipeline: adding CodeBuild
---
- Access the [[CodePipeline-CodeCommit-CodeDeploy|pipeline]] configured earlier and edit
- Add a new test stage to run CodeBuild
	- Add an action group, and give it a name
	- Action provider: select Test - CodeBuild
- Input artifact comes from the previous stage in CodePipeline (source stage)
>[!info]+ Action config:
>![[Pasted image 20230320170805.png]]

![[Pasted image 20230320171633.png]]
- we can add multiple actions per action group; these are **parallel stages**
- Adding sequential items **per stage**: action group 
- Save the pipeline, then click *Release change* to trigger the new pipeline 
	- Add S3 resource permission for CodeBuild role so it can obtain the artifact from CodePipeline
---
# References


## Tags
- #AWS-DevOps/CodePipeline/build-stage/CodeBuild-test  
---