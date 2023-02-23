Created: 2023-02-22 14:20
# Creating a CodeCommit Repo & Configuring HTTPS Connectivity
---
## 1. Creating the CodeCommit Repo
- After creating a CodeCommit repo as a root user, the following warning will be displayed:
	- `You are signed in using a root account. You cannot configure SSH connections for a root account, and HTTPS connections for a root account are not recommended. Consider signing in as an IAM user and then setting up your connection.`
		- This is true; don't want to compromise root account's credentials

## 2. Setting up the IAM User
- ### Creating the user that will connect to the CodeCommit Repository:
	- After Accessing the IAM Management Console, click on *Users*
	- Add a user
		- Give this user a name
		- This user will need *programmatic access* and *AWS Management Console* access
			- Enables an **access key ID and secret access key** for AWS API, CLI, SDK, and other dev tools
	- & IAM User Details:![[Pasted image 20230222162836.png]]
	
		- & IAM User Permissions:![[Pasted image 20230222163104.png]]
			- Click on *Create group*
				- & create a new group name `admin` with *AdministratorAccess* permission policy, then click *Create user group* ![[Pasted image 20230222163535.png]]
				- **Add this new IAM User to this group**
 
	 - Keep clicking on *Next* (not adding tags for now) 
		 - & ![[Pasted image 20230222163925.png]]
	- Download the `.csv` file, this as the IAM user's access key ID, secret access key, and password
- ### Creating HTTPS Git Credentials
	- Click the user in the IAM Users list, and then the *Security Credentials* tab
		- & Scroll down to *HTTPS Git credentials for AWS CodeCommit* and generate credentials. **Save these credentials, they'll never be viewable again after closing**![[Pasted image 20230222165251.png]] 

## 3. Configuring CodeCommit Repo HTTPS Connectivity  
- Click on *Clone URL*, then *Clone HTTPS*
	- & Clone confirmation message:![[Pasted image 20230222171240.png]]
- Open up the terminal and `git clone` this URL
	- & Cloning the repo: enter the IAM HTTPS Git Credentials  ![[Pasted image 20230222171656.png]]
		- The repository is currently empty; no code has been pushed to it yet
		
---
# References
- [IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_identity-management.html?icmpid=docs_iam_console#intro-identity-users)
- [IAM Identities: users, user groups, and roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id.html?icmpid=docs_iam_console)
- [Setup for HTTPS users using Git Credentials](https://docs.aws.amazon.com/codecommit/latest/userguide/setting-up-gc.html?icmpid=docs_acc_console_connect_np)

## Tags
#codecommit-config
#IAM-config

---