Created: 2023-02-19 18:59
# Terraform Commands
---

## Basic Commands

- ### Init
	- prepares the current working directory for follow-up commands
	- 1st command that is run after writing a new configuration
	- working directory *must* have a configuration to run this command
	
- ### Plan
	- displays the changes made by the configuration
	- **creates an execution plan by refreshing the state and comparing it with the required configuration**
	
- ### Apply
	- applies a newly created configuration
	- can also be used to deploy a predetermined set of actions generated in the execution plan

## State Commands

- can be used to maniplate terraform state instead of changing it directly
	- `list`: lists all resources in the current state
	- `show`: displays details about a deployed resource
	- `rm`: removes a deployed resource
	- `pull`: displays current state on stdout
	- `push`: updates state from local state file
	- `replace-provider`: changes provider of the current state

---
# References
- [terraform docs: CLI commands](https://developer.hashicorp.com/terraform/cli/commands)

## Tags
- #terraform-commands
---