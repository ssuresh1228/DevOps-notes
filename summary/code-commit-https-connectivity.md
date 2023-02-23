Created: 2023-02-22 17:26
# Creating and Configuring CodeCommit Repo
---
- ## 3 main steps:
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
# References
- [[CodeCommit-first-repo-https-config|Detailed notes]]

## Tags

---