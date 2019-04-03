# Lab 5 - Data Storage
In this lab we will create a simple data storage location in Azure and apply security controls around it.

## Task 1. Create a Storage Account
An Azure storage account contains all of your Azure Storage data objects: blobs, files, queues, tables, and disks. We first need to create a Storage Account before storing any files in Blob or File-based storage. 

We need to create a storage container to begin using our new Storage Account.

In the navigation on the left, click `Storage accounts`.

Now, create our Storage container as follows:
![Create Container](../images/create-container.png?raw=true "Create Container")

Now, fill in some details about your new Storage Container:
![Create Container](../images/create-storage-1.png?raw=true "Create Container")

![Create Container](../images/create-storage-2.png?raw=true "Create Container")

## Task 3: Create a Shared Access Signature for the Storage Account
A shared access signature (SAS) is a URI that grants restricted access rights to Azure Storage resources. You can provide a shared access signature to clients who should not be trusted with your storage account key but whom you wish to delegate access to certain storage account resources.

![SAS](../images/sas-setup.png?raw=true "SAS")

## Task 4: Encrypt the Data with a Key Vault Key
Azure Storage Service Encryption for data at rest helps you protect your data to meet your organizational security and compliance commitments. With this feature, the Azure storage platform automatically encrypts your data before persisting it to Azure Managed Disks, Azure Blob, Queue, or Table storage, or Azure Files, and decrypts the data before retrieval. 

In this task we will use a customer supplied key to perform the encryption instead of an Azure-provisioned key. 

First, create an [Azure Key Vault](https://azure.microsoft.com/en-us/services/key-vault/) to house our keys securely:
```
az keyvault create --name "Secret-Vault-<your_last_name>" --resource-group "<your_resource_group>" --location eastus
```
Now create a key to use. We are using default parameters but many more options for key creation can be found [here](https://docs.microsoft.com/en-us/cli/azure/keyvault/key?view=azure-cli-latest#az-keyvault-key-create):
```
az keyvault key create --name encryptallthethings --vault-name <Secret-Vault-<your_last_name>
```
Now, in the Storage Account settings page click on `Encryption`. Select the `Use your own key` box. 

Select your recently created Key Vault and generated key as follows:
![Encrypt](../images/encrypt.png?raw=true "Encrypt")

Your Storage Account data is now being encrypted using a customer controlled key stored in Azure Key Vault!

## Bonus
Using IAM, give the user `jmesta@manicode.com` read-only access to the newly created Storage Account. Remember, use built-in roles when possible and where applicable. 

## Further Reading
It is also easy to create storage accounts using the CLI as follows:
```
az storage account create \
    --name <your_last_name> \
    --resource-group <your_resource_group> \
    --location eastus \
    --sku Standard_LRS \
    --encryption blob
```
