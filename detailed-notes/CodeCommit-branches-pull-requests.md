Created: 2023-02-22 18:39
# Branches and Pull Requests
---
## Creating a new branch
- `git checkout -b <new-branch-name>`

>[!info] When pushing to a new branch, this command needs to be run once
>- `git push --set-upstream origin <new-branch-name>`
>	- We want to push the `new-branch-name,` and create it on the remote repo 


- & new branch is created on remote CodeCommit repo: ![[Pasted image 20230223140545.png]]

> [!tip] Master the concept of branching for the DevOps exam
> - There will be many questions around handling different environments/features
> 	- The answer to this is to use branches to handle multiple different environments/features

## Merge my-feature Branch to Master
- & handled in CodeCommit with pull requests![[Pasted image 20230223141521.png]]
- Create a pull request as a way to tell other devs that some changes have been made in another branch; if everyone else is okay with these changes, then the changes can be merged to master.
	- & Changes tab![[Pasted image 20230223142609.png]]
	- & Clicking on *Merge*: ![[Pasted image 20230223142817.png]]

>[!tip] Git best practices 
> - Process of creating a branch, developing a new feature on that new branch, and then merging back to master/main branch. 
> 
> - Creating a pull request for this change allows others to review the changes made to the code *before* merging it to master/main branch
>  

---
# References
- [[aws-codecommit-docs#^de4e84|Atlassian guide on branches]]

## Tags
#AWS-DevOps/CodeCommit/branch 
#AWS-DevOps/CodeCommit/pull-request 

---