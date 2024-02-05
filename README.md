***Containerised Neo4J Demo***

__Deps__

* Setup a storage account container and put the backend details in `terraform-setup-step.yaml`
* Create a Service Principal called `terraform-agent` using the Azure CLI and pass `$(AZURE_SUBSCRIPTION_ID)`, `$(AZURE_TENANT_ID)`, `$(SPA_APP_ID)`, `$(SPA_PASSWORD)` as Pipeline Secrets.
* Also create a service connection called `terraform-agent` referencing the same Service Principal

__Notes__

* `/modules/azure-container-instances` is a generic Terraform module for deploying Azure Container Instances. NB// it accepts a `list(number)` for open TCP ports.
* `/templates` passes params to the generic Terraform module to configure TCP and Image for a Neo4J deployment and then teardown operation. NB// there is a placeholder for tests (cf. parameter `testSteps`) 
* `azure-pipleines.yaml` configures two hypothetical environments.

__Usage__

* clone the repo and update the backend details and auth variables.
* `git push` and on successful completion of the pipeline the `Terraform Apply` step in the `Neo4J Demo` Job reveals an IP. Navigate to that `HTTP://<insert the IP>:7474` the web browser to view in the Demo environment.
