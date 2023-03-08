Created: 2023-03-07 14:38
# Buildspec.yml Deep Dive
---
- CodeBuild looks at `buildspec.yml` for instructions on building/testing

>[!info]+ Example buildspec.yml in CodeCommit repo:
>![[Pasted image 20230307171225.png]]
>>[!tip]+ buildspec parts:
>>- phases:
>>	- install: installs nodejs10 runtime on Docker image
>>	- pre_build
>>		- handles setup eg. config files
>>	- build
>>		- what we actually want to do to build/test code
>>	- post_build
>>- Each phase can have its own set of *command*s
>>	- eg. to install external packages like `curl`

>[!Tip]+ CodeBuild's phase details tab:
>- displays *all* phases 
>![[Pasted image 20230307173503.png]]
>- SUBMITTED: 
>	- build was started
>- QUEUE: 
>	- shows how long the build request was queued
>- PROVISIONING: 
>	- how long it took for the Docker container to arrive
>- DOWNLOAD_SOURCE: 
>	- how long it took to download source code (from CodeCommit repo in this case)
>- Hooks (in buildspec.yml)
>	- PRE_BUILD
>	- BUILD
>	- POST_BUILD
>- final phases:
>	- UPLOAD_ARTIFACTS
>	- FINALIZING
>	- COMPLETED

## Buildspec.yml reference docs

### buildspec syntax
>[!abstract]+ complete buildspec file:
>```
>version: 0.2
>run-as: Linux-user-name
>env:
>  shell: *shell-tag*
>  variables:
>	*key*: "*value*"
>	*key*: "*value*"
  >parameter-store:
>	*key*: "*value*"
>	*key*: "*value*"
  >exported-variables:
>	- *variable*
>	- *variable*
  >secrets-manager:
>    key: secret-id:json-key:version-stage:version-id
>  git-credential-helper: no | yes
  >
>proxy:
>  upload-artifacts: no | yes
>  logs: no | yes
  >
>batch:
>  fast-fail: false | true
>  # build-list:
>  # build-matrix:
>  # build-graph:
  >
>phases:
>  install:
>	run-as: Linux-user-name
>	on-failure: ABORT | CONTINUE
>	runtime-versions:
>	  runtime: version
>	  runtime: version
>	commands:
>	  - *command*
>	  - *command*
>	finally:
>	  - *command*
>	  - *command*
>  pre_build:
>	run-as: Linux-user-name
>	on-failure: ABORT | CONTINUE
>	*command*s:
>	  - *command*
>	  - *command*
>	finally:
>	  - *command*
>	  - *command*
  >build:
>	run-as: Linux-user-name
>	on-failure: ABORT | CONTINUE
>	*command*s:
>	  - *command*
>	  - *command*
>	finally:
>	  - *command*
> 	 - *command*
  >post_build:
>	run-as: Linux-user-name
>	on-failure: ABORT | CONTINUE
>	commands:
>	  - *command*
>	  - *command*
>	finally:
>	  - *command*
>	  - *command*
>reports:
>  report-group-name-or-arn:
>	files:
>	  - *location*
>	  - *location*
>	base-directory: *location*
>	discard-paths: no | yes
>	file-format: report-format
>artifacts:
>  files:
>	- *location*
>	- *location*
>  name: artifact-name
>  discard-paths: no | yes
>  base-directory: *location*
>  exclude-paths: excluded paths
>  enable-symlinks: no | yes
>  s3-prefix: prefix
>  secondary-artifacts:
>	artifactIdentifier:
>	  files:
>		- *location*
>		- *location*
>	  name: secondary-artifact-name
>	  discard-paths: no | yes
>	  base-directory: *location*
>	artifactIdentifier:
>	  files:
>		- *location*
>		- *location*
>		discard-paths: no | yes
>		base-directory: *location*
>cache:
>  paths:
>	- *path*
>	- *path*

### blocks in buildspec syntax:
- each block can have its own `run-as` command to run as a specified user

- `finally` block
	- run commands defined in `commands` block, whether or not they succeed
	- then run whatever is defined in the `finally` block below it
	- Every phase can have a `finally` block (e.g. used for cleanup commands)
	
- `artifacts` block
	- what is kept after a build is done
	- need to specify which files to keep and their locations
	- since the docker image is destroyed after the build, we have to specify the files we want to keep (e.g. save to S3)
	
- `cache` block
	- can cache certain paths to speed up CodeBuild deployments

### buildspec key points
- Can specify different phases for install, pre_build, build, and post_build
- can specify different environment variables and parameters from the parameter store
	- e.g. specifying a password/secret in a file path 
- `finally` block is used in case a command in the `commands` block goes wrong, and can be used as *cleanup commands*

### example buildspec file
>[!example]+ working buildspec file:
>```
version: 0.2
>env:
>  variables:
>    JAVA_HOME: "/usr/lib/jvm/java-8-openjdk-amd64"
>  parameter-store:
>    LOGIN_PASSWORD: /CodeBuild/dockerLoginPassword
>phases:
>  install:
>    commands:
>      - echo Entered the install phase...
>      - apt-get update -y
>      - apt-get install -y maven
>    finally:
>      - echo This always runs even if the update or install command fails 
>  pre_build:
>    commands:
>      - echo Entered the pre_build phase...
>      - docker login -u User -p $LOGIN_PASSWORD
>    finally:
>      - echo This always runs even if the login command fails 
>  build:
>    commands:
>      - echo Entered the build phase...
>      - echo Build started on `date`
>      - mvn install
>    finally:
>      - echo This always runs even if the install command fails
>  post_build:
>    commands:
>      - echo Entered the post_build phase...
>      - echo Build completed on `date`
>reports:
>  arn:aws:codebuild:your-region:your-aws-account-id:report-group/report-group-name-1:
>    files:
>      - "**/*"
>    base-directory: 'target/tests/reports'
>    discard-paths: no
>  reportGroupCucumberJson:
>    files:
>      - 'cucumber/target/cucumber-tests.xml'
>    discard-paths: yes
>    file-format: CUCUMBERJSON # default is JUNITXML
>artifacts:
>  files:
>    - target/messageUtil-1.0.jar
>  discard-paths: yes
>  secondary-artifacts:
>    artifact1:
>      files:
>        - target/artifact-1.0.jar
>      discard-paths: yes
>    artifact2:
>      files:
>        - target/artifact-2.0.jar
>      discard-paths: yes
>cache:
>  paths:
>    - '/root/.m2/**/*'



---
# References
- [[aws-codebuild-docs#^859eea|AWS Docs: Buildspec file reference]]

## Tags
- #codebuild 
- #buildspec
---