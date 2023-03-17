Created: 2023-03-15 17:06
# CodeDeploy: appspec.yml deepdive
---
- Just like CodeBuild has [[CodeBuild-buildspec-deepdive|buildspec.yml]], CodeDeploy has appspec.yml
	- represents how a deployment will be handled
>[!info]+ appspec.yml in CodeCommit repo:
>```
>version: 0.0
> os: linux
>files:
>  - source: /index.html
>    destination: /var/www/html/
>hooks:
>  ApplicationStop:
>    - location: scripts/stop_server.sh
>      timeout: 300
>      runas: root
>
>  AfterInstall:
>    - location: scripts/after_install.sh
>	  timeout: 300
> 	 runas: root
>
>  BeforeInstall:
>    - location: scripts/install_dependencies.sh
>	  timeout: 300
>	  runas: root
>
>  ApplicationStart:
>    - location: scripts/start_server.sh
>	  timeout: 300
>	  runas: root
>
>  ValidateService:
>    - location: scripts/validate_service.sh
>	  timeout: 300
- `files` block defines a source and destination to where files defined in the source are copied to in the destination directory
- `hooks` section defines scripts that are run as deployment is occurring across instances
	- & Corresponds with CodeDeploy's lifecycle events:![[Pasted image 20230316142720.png]]

---
# References
-  [[aws-codedeploy-docs#^efe08b|Appspec file reference]]

## Tags
- #AWS-DevOps/CodeBuild/appspec 

---