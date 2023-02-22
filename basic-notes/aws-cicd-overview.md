Created: 2023-02-21 14:12
# General Overview: CI/CD in AWS
---
## Continuous Integration
- Devs push code to a remote repository as often as possible
	- A testing/build server checks this code as soon as it's pushed (Jenkins CI/CodeBuild, etc.)
	- Developers get immediate feedback on tests and what passed/failed
- delivers code faster since it's automatically tested and deployed often

## Continuous Delivery
- Ensure that software can be released reliably whenever needed
	- Deployments are quick and occur often; automated
		- CodeDeploy, Jenkins, etc

## Basic CICD Pipeline
>[!example] 
>![[Pasted image 20230221145640.png]]

## Continuous Delivery vs. Continuous Deployment
- Continuous Delivery
	- deploying often using automation
	- may involve a manual step to approve a deployment
		- the deployment itself is _still_ automated and repeated

- Continuous Deployment
	- Full automation from start to end
		- every code change committed is deployed *all the way into production*
		- No manual intervention for deployment approvals

## AWS Tech Stack for CICD
>[!Tip] Stages in CICD pipeline and associated tools
>![[Pasted image 20230221150306.png]]

---
# References
- [[domain-1-documentation|Domain 1 Documentation]]

## Tags
#cicd  

---