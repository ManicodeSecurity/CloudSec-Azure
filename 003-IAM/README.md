## Create a Role Assignment to Add a User to our Resource Group

We will use the Azure Portal UI to add a restricted "read only" user to our Resource Group. We will use the built-in role named `Reader` to accomplish this.

### Task 1: View IAM Management in Azure Portal

In the UI, click on your Resource Group <your_last_name-moto-2019> and then click IAM.

In the upper left corner, click the `+Add` button then `Add role assignment` as follows:

![Add Role Assignment](../images/add-role-assignment.png?raw=true "Add Role Assignment")

### Task 2: Add a Read-Only User

We are going to utilize the built-in Azure role named `Reader` which allows the user or Service Principal view everything, but not make any changes. This is a useful policy to get up and running quickly. 


![Add User](../images/add-jmesta.png?raw=true "Add User")

The user should be `jmesta@manicode.com`.


## Log in as the Read-Only User
To verify that the role is being enforced, we will log in as the user `jmesta@manicode.com`.

Open up a new incognito browser window and log into the Azure Portal using a separate session.

```
The URL, and necessary credentials will be given to you in class.
```

## Attempt to Create a Resource as a Read-Only User
Now, we can log in as `jmesta@manicode.com` and verify that our user is only able to read resources.

Logged in as the `jmesta@manicode.com`, navigate to `Virtual machines`. You will see one nginx VM running that this user has access to view. Click the checkbox next to the VM and then `delete`. 

You should get an error due to your permissions. 

## Bonus
Can you create a new custom role and assign it to your Resource Group?
[Here](https://docs.microsoft.com/en-us/azure/role-based-access-control/custom-roles) is a tutorial to get you started. 

## Further Reading
Explore more about the Azure built-in roles [here](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles).