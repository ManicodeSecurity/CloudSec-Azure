# Lab 001 - Lab Setup
The goals of this lab are as follows:

- Successfully authenticate to Azure
- Explore Azure Cloud Shell
- Use the `az` CLI to interact with Azure
- Create a Resource Group

## Authenticate to Azure
1. Visit [https://portal.azure.com](https://portal.azure.com)

Use your corporate AD credentials to authenticate to the Azure web portal. After entering your email address you will be redirected to a page to enter your corporate AD username and password.

2. After logging in, you will be redirected to the Home page which will give you a rundown of you Azure infrastructure at a glance.

3. We will use an Azure Subscription for the remainder of the labs called `MANICODE_SECURITY`. Do not perform any labs outside of this subscription.

## Open Cloud Shell
Cloud Shell offers a browser-accessible, pre-configured shell experience for managing Azure resources without the overhead of installing, versioning, and maintaining a machine yourself on your local machine. Azure Cloud Shell is assigned per unique user account and automatically authenticated with each session.

We will use Cloud Shell exclusively for the remainder of the labs.

1. In the upper-right of the Azure Portal, click the button below:

![Cloud Shell Button](../images/azure-cloud-shell.png?raw=true "Cloud Shell Button")

2. This will open up a terminal in your browser. Choose `bash` as your shell. You are free to use `Powershell` if you are more comfortable with it but these labs will only support `bash`.

![Cloud Shell Bash](../images/azure-bash.png?raw=true "Cloud Shell Bash")

## Explore the Azure CLI
The Azure CLI is a command-line tool providing a simple to use experience for managing Azure resources. The CLI is designed to make scripting easy, query data, support long-running operations, and more.

When using Azure Cloud Shell, we are logged in automatically to the appropriate account.

### Ensure the appropriate account ID is set:

1. View a list of Azure accounts:
```
az account list --output table
```
2. Choose the account with the `"name": "MANICODE_SECURITY"` and copy the `id` value to your clipboard.

3. Now, set your account to the subscriptionId from the above command:
```
az account set --subscription 586b8dda-9e70-####-##########
```
4. Ensure you are using the correct account:
```
az account show --output table
```

## Create a Resource Group
We need an an isolated location to perform the labs for class within our Subscription. We will use the `Resource Group` feature in Azure to carve out an isolated location to spin up infrastructure. Resource Groups are used to create a logical collection of cloud-based assets such as Virtual Machines or Networks.

### Create an Azure Resource Group using the CLI

1. First, let's use the `az` cli to show a list of Resource Groups already existing in our Subscription:
```
az group list --output table
```
2. Create a Resource Group to use for your lab activities.

(!!) *REPLACE <YOUR_LAST_NAME> WITH....YOUR ACTUAL LAST NAME* (!!)
```
az group create -n <YOUR_LAST_NAME>_MANICODE -l eastus
```

### Ensure the Resource Group was Created in the UI
Now, go back to the Azure Portal and click `Resource Groups` in the navigation. You should see your newly created group in the list:
![Resource Group](../images/resource-groups.png?raw=true "Resource Group")

You may need to apply a filter to only show Resource Groups whic are part of the `MANICODE_SECURITY` subscription.