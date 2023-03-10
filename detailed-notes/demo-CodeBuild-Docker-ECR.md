Created: 2023-03-07 19:09
# CodeBuild + Docker + ECR demo
---
>[!Abstract]+ Objective: Produce a build output as a Docker image and push to ECR image repository

## Configure existing CodeBuild service role to add ECR permissions
- Access IAM console
	- [Working with in-line policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_manage.html#AddingPermissions_Console)
- Click on *Roles* under *Access Management*, then the policy name associated with the CodeBuild service role created when running the [[CodeBuild-basic-build#Creating CodeBuild project|basic build]]
>[!Info]+ Configuring ECR permissions for CodeBuild service role:
>![[Pasted image 20230307195824.png]]
>- This policy allows this service role to create ECR repositories

## Create a new image repository in ECR
- Make sure that the repository is created **in the same region** where the build environment is created
	- [Creating a repository in ECR](https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-create.html)
>[!Info]+ Creating ECR repo:
>![[Pasted image 20230307193750.png]]

## Edit CodeBuild service role's inline policy to allow uploading of Docker images
>[!info]+ Updated service role JSON:
>![[Pasted image 20230307200202.png]]

## Create the required files and upload to S3, CodeCommit, or some other version control
>[!tip]+ Assume/create the following directory structure:
>![[Pasted image 20230307204522.png]]

### Buildspec.yml in root directory
>[!example]+ buildspec.yml contents:
>```
version: 0.2
>phases:
>   pre_build:
>    commands:
>      - echo Logging in to Amazon ECR...
>      - aws ecr get-login-password --region $AWS_DEFAULT_REGION | docker login --username AWS --password-stdin $AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com
>  build:
>    commands:
>      - echo Build started on `date`
>      - echo Building the Docker image...          
>      - docker build -t $IMAGE_REPO_NAME:$IMAGE_TAG .
>      - docker tag $IMAGE_REPO_NAME:$IMAGE_TAG $AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com/$IMAGE_REPO_NAME:$IMAGE_TAG      
>  post_build:
>    commands:
>      - echo Build completed on `date`
>      - echo Pushing the Docker image...
>      - docker push $AWS_ACCOUNT_ID.dkr.ecr.$AWS_DEFAULT_REGION.amazonaws.com/$IMAGE_REPO_NAME:$IMAGE_TAG
>```

#### Environment Variable setup in CodeBuild project 
- this buildspec.yml uses some environment variables that must be set up in order for the build to succeed:
>[!important]+ Set up the following environment variables in this CodeBuild project:
>1. AWS_DEFAULT_REGION: `region-id`
>2. AWS_ACCOUNT_ID: `account-id`
>3. IMAGE_TAG: `latest`
>4. IMAGE_REPO_NAME: `Amazon-ECR-repo-name`
>- These can either be added *directly* to the buildspec file as shown in [[aws-codebuild-docs#^859eea|buildspec reference]], or overridden/created in the CodeBuild console

### Dockerfile in root directory
>[!example]+ Dockerfile contents:
>```
>FROM golang:1.12-alpine AS build
#Install git
RUN apk add --no-cache git
#Get the hello world package from a GitHub repository
RUN go get github.com/golang/example/hello
WORKDIR /go/src/github.com/golang/example/hello
># Build the project and send the output to /bin/HelloWorld 
>RUN go build -o /bin/HelloWorld
>
>FROM golang:1.12-alpine
>#Copy the build's output binary from the previous build container
>COPY --from=build /bin/HelloWorld /bin/HelloWorld
>ENTRYPOINT ["/bin/HelloWorld"]

---
# References
- [Written guide](https://docs.aws.amazon.com/codebuild/latest/userguide/sample-docker.html#sample-docker-running)

## Tags 
- #docker 
- #AWS-DevOps/ECR/push-codebuild-image
- #AWS-DevOps/demo/codebuild/ECR 
---