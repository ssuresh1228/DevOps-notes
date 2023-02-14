Created: 2023-02-13 19:43
# Module Support for Docker Interaction
---
## Ansible and Docker

- ### Ansible
	- configuration management system written in Python
	- describes configurations using a declarative markdown language
	- Used to Automate software configuration and deployment

- ### Docker
	- Software for deployment automation and app management 
	- virtualizes an environment at the OS level

- ### Ansible & Docker
	- Ansible doesn't require much infrastructure to run
	- Running Ansible inside a container is like building a container image and copying it across other environments as needed
		- Makes updates/lifecycle management for Ansible deployments very easy
			- Just build a new container image, and run it to update/use newer versions, components, etc.
	- #### Benefits
		- Flexibility
			- Ansible playbooks are compact and portable
		- Auditability
			- Can easily trace deployment stats of the container
		- Ubiquity
			- Using Ansible allows managing of complex environments & containers easily
			- Ansible controls containerized apps and non-containerized apps simultaneously
				- Controller node deploys host environments, containers, and services
		- Similar Syntax
			- Ansible playbooks use YAML, and docker has its own non-YAML scripts

## Docker Overview & Basic Commands

>[!Note] Basic Docker Commands
> 1. Installing Docker on Ubuntu 18.04
> 	- `sudo apt-get update`
> 	- `sudo apt install docker.io -y`
> 	
> 2. Verify installation by checking Docker version
> 	- `docker --version`
> 	
> 3. Start and enable Docker for use
> 	- `sudo systemctl start docker`
> 	- `sudo systemctl enable docker`
> 	
> 4. Build an image using directives in dockerfile
>	 - `docker build -t ansible:latest`
>		 - After running this command, Ansible is successfully built under Docker
> 
> 5. Run newly built Docker Image with Ansible (Interactive Mode)
> 	- `docker build -t ansible:latest`


---
# References


## Tags
- #docker

---