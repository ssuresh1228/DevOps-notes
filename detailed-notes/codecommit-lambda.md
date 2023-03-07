Created: 2023-03-01 19:12
# CodeCommit and AWS Lambda
---

- ## Creating the Lambda Function
	- Access AWS Lambda console, then click on *Create a Function*
		- Create the function from scratch & give it a name
		- Select *Python 3.7* for runtime 
>[!Example]+ Basic Config:
>![[Pasted image 20230306163619.png]]

- ## Configuring Triggers from CodeCommit
	- After the lambda function has been created, click on *Add trigger* and select *CodeCommit* as its source:
>[!Example]+ Trigger Source Config:
>![[Pasted image 20230306163854.png]]


- ## Implementing Lamba Function
	- Example code is present in references based on runtime
>[!Example]+ Lambda Function in python
>![[Pasted image 20230306165325.png]]
> - imports boto3 - AWS client library 
> - gets Git clone URL from the events and passes it on to the Lambda handler 
> 	- then prints it into log
> - just prints the git clone URL, nothing else

>[!Example]+ Testing the Lambda Function via test event:
>![[Pasted image 20230306165715.png]]
>>[!note]+ Test Results:
>>![[Pasted image 20230306165832.png]]

- ## Testing the Lambda function in CodeCommit
	- edit some line in index.html in the [[CodeCommit-first-repo-https-config|CodeCommit repo]] then commit to master branch
	- Open CloudWatch, then access *Log Groups*
		- The Lambda function will be visible here, along with its events:
>[!note]+ Lambda log group in CloudWatch:
>![[Pasted image 20230306170348.png]]

---
# References
- [[aws-codecommit-docs#^bb89e3|Creating Trigger for Lambda Function]]

## Tags
- #lambda

---