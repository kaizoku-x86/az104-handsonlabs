## Basics commands 
>az deployment -h

>Group \
    az deployment : Manage Azure Resource Manager template deployment at subscription scope. 
    >>Subgroups: \
        ```group  : Manage Azure Resource Manager template deployment at resource group.``` <- We will use the ```deployment group``` \
        mg        : Manage Azure Resource Manager template deployment at management group.\
        operation : Manage deployment operations at subscription scope. \
        sub       : Manage Azure Resource Manager template deployment at subscription scope. \
        tenant    : Manage Azure Resource Manager template deployment at tenant scope. 

>az deployment group -h

>Group
    az deployment group : Manage Azure Resource Manager template deployment at resource group. \
>>Commands: \
    cancel   : Cancel a deployment at resource group. \
    create   : Start a deployment at resource group. \
    delete   : Delete a deployment at resource group. \
    export   : Export the template used for a deployment. \
    list     : List deployments at resource group. \
    show     : Show a deployment at resource group. \
    validate : Validate whether a template is valid at resource group. \
    wait     : Place the CLI in a waiting state until a deployment condition is met. \
    what-if  : Execute a deployment What-If operation at resource group scope.

## Create a Resource Group to deploy in
The following command will create a ResourceGroup called ```lab-rg-0```
>az group create -n lab-rg-0 --location westeurope

>Get-AzResourceGroup \
>>ResourceGroupName : lab-rg-0 \
Location          : westeurope \
ProvisioningState : Succeeded \
Tags              : \
ResourceId        : /subscriptions/.../resourceGroups/lab-rg-0

After our ResourceGroup is created we can deploy our ARM template [../arm-templates/lab-rg-0.json](../arm-templates/lab-rg-0.json)
>az deployment group create  \\ \
--name az104-handsonlab-basicdp \\ \
--resource-group lab-rg-0 \\ \
--template-file ./arm-templates/lab-rg-0.json \\ \
--no-wait 

It will deploy a basic environment with:
- Storage Account
- Network Security Group
- Public IP Address
- Network Interface
- Virtual Network
- Virtual Machine
- Disk
