Created: 2023-03-08 15:48
# CodeBuild: Artifacts and S3
---
## Artifacts overview
- Build artifacts (eg. JAR, WAR files) from CodeBuild need to be uploaded somewhere else (S3) for other programs to be able to use/deploy 
	- When CodeBuild is used to build these artifacts, new files are generated
	- Build output is an artifact

>[!example]+ builspec.yml artifacts block:
>```
>artifacts:
>  files:
>    # Save all files	 
>    - '**/*'
>  name: myArtifactName-$(date +%Y-%m-%d)
>```
>- example of an artifact name with the artifact date's creation
> 
>>[!info]+ updated buildspec file in CodeCommit repo:
>>![[Pasted image 20230309114423.png]]

## Uploading artifacts to S3 bucket
### Artifacts config in CodeBuild
- Access your CodeBuild project, then select *Edit* on the dropdown menu, and select *Artifacts*
> [!info]+ Dropdown Menu:
> ![[Pasted image 20230309120612.png]]
>> [!info]+ Basic config:
>> ![[Pasted image 20230309121005.png]]
>> - We need to create a S3 bucket now to add to the *Bucket name* section 

### Creating S3 bucket
- Access S3 UI, and click on *Create bucket*
>[!info]+ basic bucket config:
>![[Pasted image 20230309121852.png]]
>- bucket namespaces are defined on a global level; your bucket name must be unique to be created 
- After bucket creation, add this bucket name to the *Artifacts* config in CodeBuild
	- Refresh the CodeBuild page to make the bucket show up

### Updated Artifacts Config
>[!info]+ Basic CodeBuild artifacts config:
>![[Pasted image 20230309122517.png]]
>>[!tip]+ Service Role Permissions
>>- we haven't yet configured any S3 permissions for the CodeBuild service role, but this checkbox adds this IAM policy to the CodeBuild service role for us
>> 
>>>[!tip]+ Ran into an issue with the role versions:
>>>`codebuild.amazon.com did not create the default version (V4) of the codebuild-RWBCore-managed-policy policy that is attached to the codebuild-RWBCore-service-role role. To continue, detach the policy from any other identities and then delete the policy and the role.`
>>>- Solution was to delete all *versions* of the role, leaving only V1 

### Running the Build
- Run the build again, then access S3 console
>[!info] S3 console with uploaded artifacts:
>![[Pasted image 20230309124109.png]]
>- Name is the Build ID
>
>- Select and downloading the object allows us to download the zip of all artifacts as configured in CodeBuild's artifacts section:
> ![[Pasted image 20230309124310.png]]
> 
>- This bucket is encrypted using AWS KMS:
>![[Pasted image 20230309124457.png]]

## Key points
- Build artifacts must be uploaded somewhere to be used by other programs/next stage of CI/CD
	- In this case, the build artifacts generated from the CodeBuild job were uploaded to S3 and were downloadable as a zip archive

---
# References
- [[aws-codebuild-docs#^859eea|Buildspec reference]]
- [Troubleshooting IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/troubleshoot_roles.html)

## Tags
- #AWS-DevOps/S3/upload-artifacts
- #AWS-DevOps/CodeBuild/artifacts 

---