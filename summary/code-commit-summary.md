Created: 2023-02-22 17:26
___
## Creating and Configuring CodeCommit Repo

- ### 3 main steps:
	1. Create the CodeCommit repo
	2. Set up IAM User to connect to this repo
		- Needs Username and a user group
			- give this user permissions to AWS Management Console, and AdministratorAccess in *Create User Group*, then add this user to that group  
		- Save the credential `.csv` file
		- Configure HTTPS Git Credentials for this user
			- Click on this IAM User then security tab
	3. Clone the CodeCommit repo on your local machine
		- On CodeCommit, click on *Clone URL*, then *Clone HTTPS* for the repo url
			- then `git clone <url>`
---

## Using branches and PRs
- Git best practices:
	- Create a new branch, and develop a new feature on that branch
	- Commit and push this new branch & its new code to the remote repo
	- Open a pull request
		- This will show others your changes; allows others to review your code and see what changed
		- If satisfied, your branch will be merged to main


# References
- [[CodeCommit-first-repo-https-config|CodeCommit configuration detailed notes]]
- [[CodeCommit-branches-pull-requests|Branches & pull requests detailed notes]]

## Tags
#summary

---