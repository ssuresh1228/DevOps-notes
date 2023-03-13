Created: 2023-02-23 15:04
# Securing the Repo and its Branches via IAM policy
---
- Master/main branch is considered the **working version of code**
	- *Never* push directly to master; this is bad practice since it could potentially break the working version 
	- To enforce [[code-commit-summary#Using branches and PRs|best practices]], we can set limit pushes/merges to branches in CodeCommit

>[!abstract]+ Objective: Protect master branch from unwanted commits via IAM policy
>- Create 2 IAM groups; junior devs and senior devs
>	- *only senior devs have permission to merge and push into master branch*

## Creating junior-dev Group & denying Permissions
- Access IAM console and create a new user group named *junior-devs*
	- skip adding any permission policy for now and just create the group
- Click on the group, then the *Permissions tab*

### Configuring IAM inline policy
> [!example]+ IAM incline policy:
>```
> {
>   "Version": "2012-10-17",
>   "Statement": [
>        {
>            "Effect": "Deny",
>            "Action": [
>                "codecommit:GitPush",
>                "codecommit:DeleteBranch",
>                "codecommit:PutFile",
>                "codecommit:MergePullRequestByFastForward"
>            ],
>            "Resource": "arn:aws:codecommit:*:*:*",
>            "Condition": {
>                "StringEqualsIfExists": {
>                    "codecommit:References": [
>                        "refs/heads/master"   
>                   ]
>                },
>                "Null": {
>                    "codecommit:References": false
>                }
>            }
>        }
>    ]
>}
>```

- #### Important Sections
	- *Action* section 
		- defines `service:action` on a _resource_
	- *Resource* section
		- In this case, defines the CodeCommit repo
			- We are blanket covering *all possible repos* here:
				- 1st star: AWS region
				- 2nd star: AWS Account
				- 3rd star: CodeCommit repo
	- *Condition* Section:
		- Defines what _exactly_ to apply these actions on
			- master branch of _all CodeCommit repos_ as defined in the resource section


- #### Explicit Deny Precedence
	- In IAM, _explicit deny_ effect takes precedence over everything else
		- This is why we create a _deny policy_ for the junior devs rather than an _allow policy_ for the senior devs
	- If there's an explicit allow and explicit deny, the explicit deny is what goes into effect

- This IAM policy just denies pushing, deleting branch, put file, and merging branches on the *master* branch for *all* CodeCommit repos

- Review the policy name it *cannot-push-to-master-branch*, and then create it 

>[!info]+ After creating and saving the group:
>![[Pasted image 20230223182258.png]]
>![[Pasted image 20230223182407.png]]


## Testing the junior-dev user group
- Go to *Users,* then the DevOps user created earlier in [[CodeCommit-first-repo-https-config#2. Setting up the IAM User|setup of the first repo]] 
	- Click on *Add user to groups,* then select the `junior-dev` user group created above
>[!info]+ DevOps IAM user
>![[Pasted image 20230223181833.png]]
>- explicit deny of the junior-devs group takes precendence over the admin permissions of the previous group 

- open terminal and run `git checkout master`
	- `git pull` to get master branch's changes after the merge from approving this [[CodeCommit-branches-pull-requests#Merge my-feature Branch to Master|pull request]]
	- make some changes to `index.html` and commit, then try to push
		- & If the IAM Policy was successful, the following error should show: ![[Pasted image 20230223183230.png]]
- Create a new pull request, and have the "senior dev" merge into master branch for you

---
# References
- [[aws-codecommit-docs#^2a9403|Configuring an IAM policy to limit pushes and merges to a branch]]

## Tags
- #AWS-DevOps/CodeCommit/access-and-security 
- #AWS-DevOps/IAM/setup-groups-permissions  
---