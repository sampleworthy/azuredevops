# GitHub Action for Checking Azure Access

This GitHub Action is designed to check the access to Azure by logging in and out using the Azure CLI. It can be triggered either by a push to the master branch or manually from the GitHub Actions tab.

## Workflow

The workflow consists of the following jobs:

1. **Checkout code**: This step checks out your repository so the workflow can access it.

2. **Login to Azure**: This step logs into Azure using the credentials stored in the `AZURE_CREDENTIALS` secret.

3. **Logout of Azure**: This step logs out of Azure to ensure that the login session is properly closed.

The job runs on an Ubuntu machine and uses the `azuredevops` environment.

## Setup

To use this action, you need to set up the `AZURE_CREDENTIALS` secret in your repository settings. This secret should contain the JSON output of the following Azure CLI command:

```plaintext
az ad sp create-for-rbac --name "azuredevops" --role contributor \
                            --scopes /subscriptions/{subscription-id}/resourceGroups/{resource-group} \
                            --sdk-auth
```

Replace `{subscription-id}` and `{resource-group}` with your Azure Subscription ID and Resource Group name.

## Triggering the Action

You can trigger this action by pushing to the master branch of your repository. You can also manually trigger it from the Actions tab in your GitHub repository.

---

This action does not perform any operations in Azure, it simply logs in and out to check the access.