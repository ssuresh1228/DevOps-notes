Created: 2023-03-09 19:19
# CodeBuild: Validating CodeCommit Pull Request
---
>[!Abstract]+ Objective: testing branches and pull requests
>- Have CodeBuild test the pull request for us befre merging it to master branch

## How it works
- In CodeCommit, we add features in a development branch, then open a pull request to merge into the master branch
- This pull request triggers an EventBridge event, which then triggers a lambda function and a CodeBuild job (target)
	- This lambda function will add a comment to the pull request comment saying a build has started
	- CodeBuild will start a build 
		- This build will either succeed or fail 
- Build result invoke another EventBridge event
	- This event will invoke another lambda function
	- lambda function will post another comment on create/update pull request with build outcome (success/fail)

## Why do this?
- Opens up automation every time a pull request is opened
	- it is built and tested, and the build result is added in a comment in that pull request

---
# References
- [[aws-codebuild-docs#^099a43|AWS DevOps blog - Validing CodeCommit Pull Requests with CodeBuild and Lambda]]
- 

## Tags
- #AWS-DevOps/CodeBuild/codecommit-lambda 
- #AWS-DevOps/lambda/pull-request 
- #AWS-DevOps/EventBridge/integration 
---