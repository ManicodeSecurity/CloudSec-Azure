# Lab 004 - Terraform
[Terraform](https://www.terraform.io/intro/index.html) is a tool for building, changing, and versioning infrastructure safely and efficiently. Terraform can manage existing and popular service providers as well as custom in-house solutions. 

This lab will deploy the following resources to your Azure resource group using Terraform:
```
A virtual network with the CIDR 10.0.0.0/16

Two public IP addresses
An Azure load balancer

A virtual machine scale set attached to the vnet

A virtual machine connected to the vnet
```

## Task 1: Clone this Repository
In Cloud Shell run the following commands to ensure the correct files are available:
```
git clone https://github.com/ManicodeSecurity/CloudSec-Azure

cd Cloudsec-Azure/004-Terraform/terraform
```

Now, review the Terraform files in the repository and make sure you understand what is about to be deployed. 

## Task 2: Add your Resource Group to variables.tf
In Cloud Shell, use a text editor such as vim or nano, add your Resource Group name `<your_last_name-moto-2019> to the following field below in the `variables.tf` file:

![add resource](../images/variables.png?raw=true "add resource")



## Task 2: Run the Terraform Commands

Now run the following Terraform commands. Make sure you are in the correct directory where the `.tf` files are located.

```
terraform init
terraform plan
terraform apply
```

You will be asked to type `yes` during the `terraform apply`.

If everything is successful, a domain name will be printed to the terminal. Visit it and you should be able to see that NGINX is running.

Take a few minutes to see what happened under the hood and what was created. If you vist your Resouce Group screen you can now see several infrastructure objects have been created using Terraform.

### Task 3: Delete our Infrastructure using Terraform

Now that everything is Infrastructure as Code, we are able to destroy all of the assets with a single command:
```
terraform destroy
```
(This may take several minutes, seriously...it takes forever)