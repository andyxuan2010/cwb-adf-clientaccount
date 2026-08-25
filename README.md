# Azure Data Factory linked-template deployment

This repository contains example automation for exporting an Azure Data Factory
definition as linked ARM templates, uploading those templates to Azure Blob
Storage, and deploying the factory through a user-assigned managed identity.

## Pipeline used

The `cicd.yml` and `cicd2.yml` GitHub Actions workflows run on pushes to
`main`. Their intended pipeline is: authenticate to Azure with OIDC/UAMI,
generate linked templates, upload them to a storage container, and deploy the
main template incrementally. The Pages workflow only publishes the static
repository page. The checked-in workflows contain example placeholders, so
validate paths, variables, and secret names before enabling a deployment.

## Usage

Configure the required GitHub secrets and variables for the tenant, subscription,
resource group, Data Factory, user-assigned identity, storage account, and
container. Grant the identity Data Factory deployment and Blob Storage data
permissions, populate the Data Factory source expected by the workflow, and
push to `main` or run the workflow manually after reviewing the generated ARM
templates.

At minimum, verify `AZURE_CLIENT_ID`, `AZURE_TENANT_ID`,
`AZURE_SUBSCRIPTION_ID`, `RESOURCE_GROUP`, `ADF_NAME`,
`STORAGE_ACCOUNT_NAME`, and `CONTAINER_NAME`. Treat SAS tokens and deployment
outputs as secrets; do not store them in this repository.
