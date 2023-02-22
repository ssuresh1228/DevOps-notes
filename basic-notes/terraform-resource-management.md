Created: 2023-02-19 19:11
# Managing resources in terraform
---

## Modifying resources
- modifying an existing resource can be done by making changes to the existing terraform configuration and executing the `apply` command
	- changes are marked with `~` in the execution plan

## Deleting resources
- can be done via the `destroy` command to delete *all* resources
	- can pass parameters to delete a specific resource

## Referencing resources
- Terraform has the option to replicate infrastructure by referencing existing resources

---
# References
- [terraform docs: managing resources in state](https://developer.hashicorp.com/terraform/tutorials/state/state-cli)

## Tags
#terraform-resources

---