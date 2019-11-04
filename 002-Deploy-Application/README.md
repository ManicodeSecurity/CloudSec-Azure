# Lab 002 - Deploying a Cloud Application
The goals of this lab are as follows:

- Use the CLI to create a VM in Azure
- Create a VPC
- Lock Down the VM using Security Rules

## Spin up Virtual Machine Manually Using the CLI


### Task 2: Spin up the VM
We will use the `az` cli to create a Virtual Machine in our previously created resource group. The following command will create a simple publicly available Ubuntu Linux image that is running NGINX (you are free to experiment with others).

The NGINX image is located in a different resource group that we need to provide to the `az vm create` command.
```
az vm create --generate-ssh-keys --resource-group <your_resource_group_name> --name myFirstVM --image /subscriptions/15d6ea41-1e70-425e-84cf-ca13e92a7443/resourceGroups/manicodePackerWest/providers/Microsoft.Compute/images/nginxPackerImage
```

Now, take a look at the resources that were created in the Azure UI. If you click on `Resource groups -> Your resource group` you will see a list of resources:
```
Virtual Machine: The running Ubuntu Linux Virtual Machine

Disk: The storage that was automatically attached to the Virtual Machine

Network Security Group: The default Security Groups that were created to allow / deny network traffic to the Virtual Machine

Public IP address: The randomly assigned public IP address that is tied to the Virtual Machine

Network interface: The Network Interface Card (NIC) attached to the VM needed to begin routing traffic to/from the machine

Virtual Network: Provides an isolated networking environment for the VM
```

The output should be a JSON blob that will look similar to the following:
```
{
  "fqdns": "",
  "id": "/subscriptions/586b8dda-9e70-41dc-8d96-3590deff4451/resourceGroups/MESTA_MANICODE/providers/Microsoft.Compute/virtualMachines/nginxVM",
  "location": "westus2",
  "macAddress": "00-0D-3A-1E-ED-D8",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.121.145.131",
  "resourceGroup": "MESTA_MANICODE",
  "zones": ""
}
```

## Modify the Network Security Group
### Task 1: Review the Default Network Security Groups
If you try to visit the public IP address of the NGINX Virtual Machine you will get a `503` error. This is due to our default Network Security Group that was created. A rule called `DenyAllInBound` ensures no traffic other than SSH is allowed to this box.

In your Resource Group, click on the Network Security Group called `myFirstVMNSG` then click `Inbound security rules`.

![Inbound](../images/inbound-rules.png?raw=true "Inbound Rules")

### Task 2: Allow traffic to port 80
We need to create a new inbound security rule as follows:
![Inbound Allow 80](../images/inbound-allow.png?raw=true "Inbound Allow 80")

With the new inbound security rule created, you should now be able to hit the provided external IP address and see that NGINX is running and accessible.

### Bonus
Can you add another inbound security rule to allow access to port 8080 of the VM from only your public IP address instead of the entire internet? Use the Azure `az` cli to build this rule instead of the GUI.
