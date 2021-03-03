---
page_type: sample
languages:
- go
- yaml
products:
- azure
- azure-kubernetes-cluster
- secrets-store-csi
- github-actions
name: Secrets Store CSI with Azure Kubernetes and Azure KeyVault
description: Using Secrets Store CSI with Azure Kubernetes and Azure KeyVault run in Github Actions with a sample Golang application
urlFragment: secrets-store-csi-with-aks-akv
---

# Using Secrets Store CSI with Azure Kubernetes and Azure KeyVault run in Github Actions with a sample Golang application

## Overview

This repo......

## Getting Started

### Prerequisites

- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest): Create and manage Azure resources.
- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/): Kubernetes command-line tool which allows you to run commands against Kubernetes clusters.
- [Helm](https://helm.sh/docs/intro/install/): Package manager for Kubernetes
- [GitHub](https://github.com/) account

### Set up

1. Fork the repo to your github account and git clone.
2. Create a resource group that will hold all the provisioned resources and a service principal to manage and access those resources

    ```bash
    # Set your variables
    RESOURCEGROUPNAME="MyResourceGroup"
    LOCATION="MyLocation"
    SUBSCRIPTIONID="MySubscriptionId"
    SERVICEPRINCIPAL="MySPName"

    # Create resource group
    az group create --name $RESOURCEGROUPNAME --location $LOCATION

    # Create a service principal with Contributor role to the resource group
    az ad sp create-for-rbac --name $SERVICEPRINCIPAL --role contributor --scopes /subscriptions/$SUBSCRIPTIONID/resourceGroups/$RESOURCEGROUPNAME --sdk-auth
    ```

3. Use the output of the last command as a secret named `AZURE_CREDENTIALS` in the repository settings (Settings -> Secrets -> Add New Secret).

    Also add a secret named `AZURE_SUBSCRIPTIONID` for the subscription id and a secret named `AZURE_TENANTID` for the tenant id.

    ![action-secrets](./assets/action_secrets.png)

    For more details on generating the deployment credentials please see [this guide](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/deploy-github-actions#generate-deployment-credentials).

4. [Github Actions](https://docs.github.com/en/actions) will be used to automate the workflow and deploy all the necessary resources to Azure. Open the [.github\workflows\devops-starter-workflow.yml](.github\workflows\devops-starter-workflow.yml) and change the environment variables accordingly. Update the `RESOURCEGROUPNAME` variable and set the value that you created above.

5. Commit your changes. The commit will trigger the build and deploy jobs within the workflow and will provision all the resources to run the sample application.

## Validate the Secrets

TBD

## Further Configuration

- [Use a different Access Mode](https://azure.github.io/secrets-store-csi-driver-provider-azure/configurations/identity-access-modes/)
- [Microsoft Docs Tutorial](https://docs.microsoft.com/en-us/azure/key-vault/general/key-vault-integrate-kubernetes)

## License

See [LICENSE](LICENSE).

## Contributing

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
