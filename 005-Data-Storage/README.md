1. Create a storage account

az storage account create \
    --name mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --sku Standard_LRS \
    --encryption blob

Enforce RBAC Policies to Your Storage

Secure Access to the Data

Ensure Data is Encrypted at Rest Using Storage Service Encryption (SSE)



https://docs.microsoft.com/en-us/azure/storage/common/storage-security-guide