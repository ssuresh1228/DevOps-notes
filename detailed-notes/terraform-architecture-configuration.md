Created: 2023-02-19 17:56
# Terraform Architecture/Config
---

> [!info] Terraform Architecture has 2 main components:
> - core
> - provider plugin
> 	 ![[Pasted image 20230219180508.png]]


## Architecture

### Core component

#### Terraform Core
- Statically compiled binary written in Golang
	- compiled binary is the terraform CLI
- Takes terraform configuration as user input and info from state
- Creates a plan to bring system to desired state using this configuration + state file information

#### Configuration and State files
- user must write configuration to define what must be done
	- declares resources that represent the infrastructure's objects
	
- State file contains up-to-date info on the current infrastructure's setup 
	- Terraform updates the state file *before any new operation* 

### Provider plugins
- Defines which provider(s) to use for a setup
- adds resources which can be managed via terraform
- most major providers can be found on terraform registry
	- eg. AWS, Azure, GCP, Kubernetes, Fastly, etc.
- **Primary responsibilities of provider plugins**
	- initialization of any included libraries to used make any API calls
	- Authentication with infrastructure provider
	- Define resources that map specific services


---

## Configuration
- primary method of provisioning/managing infrastructure
- written in terraform language (HCL: HashiCorp Configuration Language)
	- Declarative language
### Syntax Elements
- #### Resource
	- Resource blocks are used to define infra objects
	- resource behavior defines how terraform handles resource declarations
	- meta-arguments provide special arguments that can be used with each resource type
		- & Example 
			- ![[Pasted image 20230219184601.png]]
- ##### Blocks
	- act as containers for config of objects
	- Can hav a block type, 0 or more labels, and any number of arguments
- ##### Arguments
	- assigns a value to a particular name
	- an argument's value type depends on the context in which it's used
- ##### Expressions
	- represent values
	- can be direct, referenced, or a set of values

---
# References
- [Terraform docs on core & providers](https://developer.hashicorp.com/terraform/plugin/how-terraform-works)
- [Terraform docs on configuration](https://developer.hashicorp.com/terraform/language) 

## Tags
- #terraform-architecture
- #terraform-configuration

---